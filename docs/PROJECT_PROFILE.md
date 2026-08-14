# CodeSentinel Multi-Agent Review — Project Profile

## Recommended repository name

`code-sentinel-multi-agent-review`

## GitHub description

Orchestrated multi-agent framework for risk-aware code review, evidence verification, and automated repair.

## Chinese introduction

CodeSentinel Multi-Agent Review 是一个面向 AI IDE 与研发工作流的多 Agent 代码审查与自动修复框架。系统采用 Orchestrator–Worker 架构协调七类专家 Agent，通过 Prompt Contract 约束审查边界，并以代码风险地图驱动任务分发、证据补充和复审。

项目设计了统一的结构化 Finding 协议、分层去重策略以及“审查—补证—修复—验证—重评分”闭环，目标是提升审查覆盖稳定性、降低重复与误报，并让每项问题和修复都具备可追踪的证据链。

目前项目处于架构预览阶段，仓库仅发布设计、评测摘要与路线图，不包含实现源码。

## English introduction

CodeSentinel Multi-Agent Review is an orchestrated framework for risk-aware code review and automated repair. It coordinates seven bounded specialist agents through explicit prompt contracts, a shared structured finding protocol, risk-prioritized dispatch, evidence supplementation, hierarchical deduplication, and post-repair verification.

The project is currently published as an architecture preview. Implementation source code and reproducible evaluation assets will be released separately.

## Resume version — Chinese

设计多 Agent 代码审查与自动修复框架，基于 Orchestrator–Worker 架构协调七类专家 Agent，通过 Prompt Contract 与统一 JSON Schema 约束审查边界和输出；构建代码风险地图及“初审—补证—复审”闭环，并设计分层去重、0–100 代码健康评分和修复后验证机制。原型测试中，有效问题命中率由 64.3% 提升至 81.7%，重复评论率由 26.0% 降至 8.0%，自动修复 8 项中高危问题中的 6 项。

> 对外使用上述指标时，应同时说明它们来自原型测试，并准备回答数据集、基线、样本量和验证方式。

## Resume version — English

Designed an orchestrated multi-agent code review and repair framework coordinating seven specialist agents through prompt contracts and a shared JSON schema; introduced risk-prioritized review, evidence supplementation, hierarchical deduplication, post-repair verification, and a 0–100 code health model.

## Interview elevator pitch

这个项目解决的不是“让多个 Agent 一起看代码”，而是多个 Agent 如何在边界明确、结果可合并、证据可验证的前提下协作。Orchestrator 先生成代码风险地图，再把不同风险分配给七类专家 Agent。所有 Agent 必须按照统一 Finding Schema 输出；低置信度问题进入补证流程，重复结果按代码位置、根因和数据流进行分层合并。修复 Agent 生成补丁后，还需要通过测试或静态检查验证，并重新计算代码健康分。

## Suggested GitHub topics

`multi-agent` · `code-review` · `automated-repair` · `ai-agents` · `developer-tools` · `static-analysis` · `llm` · `ai-ide` · `software-quality` · `prompt-engineering`

