# Awesome Agent Context Compression

> 四大主流 AI Agent 上下文压缩机制深度对比 — OpenCode · Reasonix · OpenClaw · Hermes Agent

## 一句话

**上下文压缩** = AI Agent 对话越来越长 → 将已完成的历史压缩为结构化摘要 → 释放上下文窗口继续工作。

---

## 覆盖系统

| 系统 | 语言 | 核心机制 |
|------|------|---------|
| **Hermes Agent** | Python | 5 阶段压缩流水线 · 每种工具一行智能摘要 |
| **OpenClaw** | TypeScript | 压缩前内存冲刷 · 双轨压缩+裁切 |
| **Reasonix** | Go | 缓存经济学驱动 · 仅在缓存过期时压缩 |
| **OpenCode** | TypeScript | 锚定摘要 · 溢出自动恢复 |

---

## 文件结构

```
00-总览                  ← 一句话 + 一张图 + 一张表
├── 01-Hermes压缩流程     ← 5 阶段逐步拆解
├── 02-四系统对比         ← 10 维度横向对比
├── 03-可复用设计模式      ← 自己实现压缩引擎的参考
├── 04-OpenCode源码分析   ← TypeScript 源码级分析
├── 05-Reasonix源码分析   ← Go 源码级分析
├── 06-OpenClaw源码分析   ← TypeScript 源码级分析
└── 07-Hermes源码分析     ← Python 源码级分析
```

---

## 作者

**陈志谦** · MockLab 工作室

面向 AI 研发负责人 / 技术总监 / 技术合伙人方向。

> *"我不是 AI 从业者，我是 AI 认知架构设计者。"*
