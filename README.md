# Awesome Agent Context Compression

> 四大主流 AI Agent 上下文压缩机制深度对比 — OpenCode · Reasonix · OpenClaw · Hermes Agent

---

## 导航

### 🌳 总览
→ **[00-总览](00-总览.md)** — 一句话 + 一张图 + 一张表，30 秒看懂

### 🌿 对比 & 流程
→ **[01-Hermes压缩流程](01-Hermes压缩流程.md)** — 5 阶段逐步拆解，每步有图  
→ **[02-四系统对比](02-四系统对比.md)** — 10 维度横向对比 + 各自独门绝活

### 🍂 综合结论
→ **[03-可复用设计模式](03-可复用设计模式.md)** — 自己做压缩引擎从哪借鉴什么

### 🍂 逐系统源码分析
→ **[04-OpenCode 源码分析](04-OpenCode源码分析.md)** — TypeScript · 181K⭐ · 锚定摘要 + auto-replay  
→ **[05-Reasonix 源码分析](05-Reasonix源码分析.md)** — Go · 25K⭐ · 缓存经济学 + cold resume  
→ **[06-OpenClaw 源码分析](06-OpenClaw源码分析.md)** — TypeScript · 381K⭐ · 内存冲刷 + 双轨制  
→ **[07-Hermes 源码分析](07-Hermes源码分析.md)** — Python · 5 阶段流水线 + 三重防抖

---

## 覆盖系统

| 系统 | 语言 | Stars | 核心机制 |
|------|------|-------|---------|
| Hermes Agent | Python | — | 5 阶段压缩流水线 · 每种工具一行智能摘要 |
| OpenClaw | TypeScript | 381K | 压缩前内存冲刷 · 双轨压缩+裁切 |
| Reasonix | Go | 25K | 缓存经济学驱动 · 仅在缓存过期时压缩 |
| OpenCode | TypeScript | 181K | 锚定摘要 · 溢出自动恢复 |

---

**mocklab** · 个人研究项目
