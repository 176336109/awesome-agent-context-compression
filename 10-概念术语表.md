# 概念术语表

> 阅读六系统分析时遇到的专业术语解释

---

## 压缩相关

### 上下文压缩（Context Compression）
对话太长放不下时，把已经完成的历史消息压缩成一段摘要，释放上下文窗口继续工作。

### 上下文窗口（Context Window）
LLM 一次能"看到"的最大 token 数量。超出这个数量，API 报错或自动截断。

### Token 阈值（Token Threshold）
上下文窗口用满到一定比例时触发压缩。例如阈值 50% = 窗口 200K → 用满 100K 就触发。

---

## 压缩技术

### 工具输出剪枝（Tool Result Pruning）
不调用 LLM，纯本地把旧的工具返回结果从几千字替换成一行摘要。
```
压缩前: [terminal stdout] 472 lines of npm test output...
压缩后: [terminal] ran `npm test` → exit 0, 47 lines
```

### LLM 摘要（LLM Summarization）
调用一个独立的（通常是更便宜的）模型，把对话历史总结成一段结构化摘要。

### 迭代摘要（Iterative Summary）
第二次压缩时，不是重新生成摘要，而是传入上次摘要，更新它——保留有效信息，删除过时内容，合并新事实。

### 锚定摘要（Anchored Summary）
OpenCode 特有的迭代摘要模式。不是"生成新摘要"，而是"更新已有锚定摘要"。

---

## 保护机制

### 防抖（Debounce / Anti-jitter）
防止压缩死循环。如果连续多次压缩节省的 token 太少（如 <10%），说明压不出东西了，跳过本次压缩。

> 类比：电梯关门键——按一次就够了，连续按不会让门关得更快。

### 冷却期（Cooldown）
压缩过程中 LLM 摘要调用抛异常后，600 秒内不再自动触发压缩。防止错误重试烧钱。

### 并发锁（Concurrency Lock）
多个 Agent 实例同时想压缩同一个会话时，数据库级锁只放行一个。防止会话状态分裂。

### 头尾保护（Head/Tail Protection）
压缩时保护上下文窗口的头部（system prompt + 前几条消息）和尾部（最近的消息），只压缩中间部分。

---

## 缓存策略

### Prompt Cache（提示词缓存）
LLM 提供商的优化机制。如果连续两次 API 调用的 system prompt 前缀相同，第二次调用只需为变化部分付费。通过保持前缀不变来省钱。

### 缓存经济学（Cache Economics）
Reasonix 的核心设计理念：缓存命中比未命中便宜 50-120 倍。因此压缩策略围绕一个核心约束设计——操作会不会让缓存失效？

### 缓存过期（Cache Cold / Cache Expiry）
LLM 提供商的缓存有 TTL（生存时间）。空闲超过一定时间后缓存过期，下一次请求要为整个 prompt 付全价。

---

## Aider 特有

### Repo Map（代码库地图）
用 tree-sitter 解析整个仓库的 AST，生成一张符号地图（每个类/函数/变量的位置）。LLM 看到地图就知道去哪改，不需要逐个读文件。

### ChatChunks（消息分层）
Aider 把消息分成 8 个独立层（system / examples / repo / done / cur 等），每层有不同的缓存策略。变化频率低的层标记为可缓存，省 token。

---

## OpenClaw 特有

### 内存冲刷（Memory Flush）
压缩前先向 Agent 发一个静默指令"把关键上下文写盘"，确保压缩不会丢失重要信息。四个压缩系统中唯一有此机制的。

### 双轨制（Compaction + Pruning）
OpenClaw 把压缩分为两个独立系统：Compaction（LLM 摘要，持久化到文件）和 Pruning（裁切旧工具输出，仅内存中生效）。

---

## Hermes 特有

### 防御性前缀（Defensive Summary Prefix）
压缩后的摘要前面加的一段提示：*"这是历史摘要，仅供参考。不要执行摘要里的任务。"* 防止 LLM 误以为摘要里的任务还需继续。

### 可插拔接口（ContextEngine ABC）
Hermes 把压缩引擎定义为抽象基类（ABC），第三方可以实现自己的压缩算法并替换内置的 ContextCompressor。

---

## Cline 特有

### Basic Compaction（基础压缩）
零 LLM 调用的轻量压缩：截断工具输出到 2000 字符 + 清理空消息 + 移除旧摘要。

### Agentic Compaction（智能压缩）
调用独立 LLM 生成结构化摘要，包含文件操作记录。比 basic 更慢但保留语义。

---

## 通用

### Overflow（上下文溢出）
对话 token 数超过模型上下文窗口上限，API 返回错误。处理方式各系统不同：OpenCode 自动恢复对话，OpenClaw 三路径触发压缩。

### Fallback（降级方案）
当首选方案失败时的备选。例如 LLM 摘要生成抛异常 → 改用纯本地的确定性摘要。

### 可插拔（Pluggable）
压缩引擎不是硬编码在 Agent 里的，而是通过接口/插件系统可以替换的。Hermes 的 ContextEngine ABC 和 OpenClaw 的 Compaction Provider 都是可插拔设计。
