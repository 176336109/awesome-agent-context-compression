# Awesome Agent Context Compression

> 六大 AI Agent 上下文管理机制深度对比

---

## 导航

### 总览 & 对比

→ **[overview](overview.md)** — 一句话 + 一张图 + 一张表，30 秒看懂  
→ **[comparison](comparison.md)** — 六系统 10+ 维度横向对比  
→ **[patterns](patterns.md)** — 自己做压缩引擎从哪借鉴什么  
→ **[glossary](glossary.md)** — 防抖、冷却期、Repo Map、缓存经济学… 术语速查

### 流程描述（flow/）

> 每个 Agent 的压缩/上下文管理流程，逐步拆解。

| Hermes | OpenCode | Reasonix | OpenClaw | Aider | Cline |
|--------|----------|----------|----------|-------|-------|
| [5阶段流水线](flow/hermes.md) | [6步+溢出恢复](flow/opencode.md) | [缓存经济学裁剪](flow/reasonix.md) | [双轨+内存冲刷](flow/openclaw.md) | [Repo Map预防式](flow/aider.md) | [双策略引擎](flow/cline.md) |

### 源码分析（agent-code/）

> 每个 Agent 的源码级分析，精确到文件+函数+行号。

| Hermes | OpenCode | Reasonix | OpenClaw | Aider | Cline |
|--------|----------|----------|----------|-------|-------|
| [agent-code/hermes](agent-code/hermes.md) | [agent-code/opencode](agent-code/opencode.md) | [agent-code/reasonix](agent-code/reasonix.md) | [agent-code/openclaw](agent-code/openclaw.md) | [agent-code/aider](agent-code/aider.md) | [agent-code/cline](agent-code/cline.md) |

---

## 一句话记住

> **Aider** 不让涨 · **Cline** 双模切 · **Hermes** 剪最细 · **OpenClaw** 护最全 · **Reasonix** 算最精 · **OpenCode** 恢复最稳

---

**mocklab** · 个人研究项目
