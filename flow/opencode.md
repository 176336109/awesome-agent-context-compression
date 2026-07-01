# OpenCode 压缩流程

> 6 步压缩 + 溢出自动恢复

---

## 总流程

```mermaid
graph TB
    S1["Step 1: create()<br/>创建 compaction part"] --> S2["Step 2: prune()<br/>标记旧工具结果"]
    S2 --> S3["Step 3: processCompaction()<br/>找父消息+截断历史"]
    S3 --> S4["Step 4: completedCompactions()<br/>取 previousSummary"]
    S4 --> S5["Step 5: select()+splitTurn()<br/>计算头尾边界"]
    S5 --> S6["Step 6: LLM 摘要生成<br/>调用 buildPrompt()"]
```

---

## 各步骤

| 步骤 | 做什么 | 关键参数 |
|------|--------|---------|
| **1. create** | 创建 compaction part，标记 auto/overflow | — |
| **2. prune** | 标记旧工具结果 `part.state.time.compacted = Date.now()` | PRUNE_PROTECT=40K, PRUNE_MINIMUM=20K |
| **3. processCompaction** | overflow 时截断历史到上一个普通 user 消息 | — |
| **4. completedCompactions** | 提取上一次压缩的锚定摘要 | — |
| **5. select + splitTurn** | tail_turns(默认2) 累积 token 预算 | preserve_recent_tokens = min(8000, max(2000, usable×25%)) |
| **6. LLM 摘要** | 调用 buildPrompt() 生成锚定摘要 | 失败且 auto=true → 自动继续 |

---

## 触发机制

硬编码 **75% 上下文窗口**触发。社区 issue #11314 要求可配置化。

---

## 溢出自动恢复

```mermaid
sequenceDiagram
    Note over LLM: 返回 "context too long"
    OpenCode->>OpenCode: 向上找引发溢出的 user 消息
    OpenCode->>OpenCode: 截断历史
    OpenCode->>OpenCode: 压缩完成
    OpenCode->>LLM: "Continue if you have next steps..."
    Note over LLM: 用户无感知
```

---

## 独特设计

- **锚定摘要**：不是重新生成，而是更新已有摘要
- **auto-replay**：溢出后自动恢复对话
- **时间戳标记**：用 `Date.now()` 标记而非删除消息
