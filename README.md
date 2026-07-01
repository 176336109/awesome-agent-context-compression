# Awesome Agent Context Compression

> 六大主流 AI Agent 上下文管理机制深度对比 — Hermes · OpenClaw · Reasonix · OpenCode · Aider · Cline

---

## 导航

### 🌳 总览
→ **[00-总览](00-总览.md)** — 一句话 + 一张图 + 一张表，30 秒看懂

### 🌿 对比 & 流程
→ **[01-Hermes压缩流程](01-Hermes压缩流程.md)** — 5 阶段逐步拆解，每步有图  
→ **[02-六系统对比](02-六系统对比.md)** — 10+ 维度横向对比 + 各自独门绝活

### 🍂 综合结论
→ **[03-可复用设计模式](03-可复用设计模式.md)** — 自己做压缩引擎从哪借鉴什么  
→ **[10-概念术语表](10-概念术语表.md)** — 防抖、冷却期、Repo Map、缓存经济学… 术语速查

### 🍂 逐系统源码分析
→ **[04-OpenCode 源码分析](04-OpenCode源码分析.md)** — TypeScript · 181K⭐ · 锚定摘要 + auto-replay  
→ **[05-Reasonix 源码分析](05-Reasonix源码分析.md)** — Go · 25K⭐ · 缓存经济学 + cold resume  
→ **[06-OpenClaw 源码分析](06-OpenClaw源码分析.md)** — TypeScript · 381K⭐ · 内存冲刷 + 双轨制  
→ **[07-Hermes 源码分析](07-Hermes源码分析.md)** — Python · 5 阶段流水线 + 三重防抖  
→ **[08-Aider 上下文管理](08-Aider上下文管理.md)** — Python · Repo Map 代码库地图 + 分层缓存  
→ **[09-Cline 上下文压缩](09-Cline上下文压缩.md)** — TypeScript · 双策略（basic 截断 / agentic LLM摘要）

---

## 覆盖系统

| 系统 | 语言 | Stars | 核心机制 |
|------|------|-------|---------|
| Aider | Python | — | ⭐ Repo Map 代码库地图 · 预防式上下文管理 |
| Cline | TypeScript | — | 双策略压缩（basic 截断 / agentic 摘要） |
| Hermes Agent | Python | — | 5 阶段压缩流水线 · 每种工具一行智能摘要 |
| OpenClaw | TypeScript | 381K | 压缩前内存冲刷 · 双轨压缩+裁切 |
| Reasonix | Go | 25K | 缓存经济学驱动 · 仅在缓存过期时压缩 |
| OpenCode | TypeScript | 181K | 锚定摘要 · 溢出自动恢复 |

---

**mocklab** · 个人研究项目
