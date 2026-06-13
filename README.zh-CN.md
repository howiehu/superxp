# SuperXP

[English](README.md)

SuperXP 是一个面向智能体软件开发的轻量级工作流框架，其设计基础来自极限编程和敏捷实践。

它的目标是通过更多依赖 Agents 和模型自身能力，以更少的规则、更低的 prompt 开销和更快的反馈，获得有效的工作流约束。

## 背景

SuperXP 致敬 [Superpowers](https://github.com/obra/superpowers)。我在实际工作中深度应用 Superpowers，并借此创造了很多价值。

同时，我也意识到，Superpowers 是导致我的工作时间变长、消耗更多 tokens 的关键原因。

所以，SuperXP 是一次对于工作流的重新思考。

## 原则

- 使用能够发挥作用的最小流程。
- 保持 prompts、规则和抽象简洁。
- 只有在反复证据表明必要时，才增加约束。
- 优先考虑可工作的软件、简单设计、测试和持续改进。
- 在增加框架机制之前，优先依赖 Agents 和模型能力。
- 所有实践都必须面向开源协作进行设计。

## v1 插件预览

SuperXP v1 是一个最小 Codex 插件预览，核心包含两个 skills：

- `using-superxp`：用于明确选择 SuperXP 的入口。
- `xp-loop`：核心 XP 工作流。

该工作流基于极限编程思想：

```text
Orient -> Clarify -> Slice -> Check -> TDD Cycle -> Verify -> Reflect
```

目标不是取消纪律，而是只保留能够产生快速反馈、清晰沟通、简单设计、小步增量和可验收交接的必要纪律。

### 极限编程约束

- **沟通：** 明确目标、范围、验收信号和交接上下文。
- **简单：** 选择能够工作的最小有价值增量。
- **反馈：** 在改动之前定义验收信号。
- **Test First：** 用测试驱动代码行为走向简单设计。
- **勇气：** 当意图、范围或验证方式不清楚时，必须停下并收敛。
- **尊重：** 保护客户意图、当前工作区、既有行为和下一位接手的 agent。

### Test First / TDD

TDD 是可测试代码变更的默认编码纪律。它将极限编程中的 Test First 实践连接到简单设计：先写下一个最小失败测试，再实现能够通过测试的最小代码，然后在测试保持通过的前提下重构。

新增行为、可复现缺陷修复、有行为风险的重构、公共接口、业务逻辑、状态流转和数据转换应使用 TDD。当严格 TDD 不适合时，Agents 必须在改动前说明原因，并定义替代反馈，例如构建、类型检查、人工检查、截图、日志、审查或生成结果校验。

### 澄清

当意图、范围、取舍或验收标准不清楚时，Agents 应优先使用宿主环境的原生提问能力。

当目标或成功标准不清楚时，使用发散提问探索选项。当需要锁定范围、方案、验收或工作流决策时，使用收敛提问。不要询问能够通过检查仓库自行回答的问题。

当以选项形式提问时，Agents 应基于已经观察到的事实给出每个选项，说明每个选项的推荐建议和主要取舍，并将综合分析后最推荐的选项放在第一项，同时简要说明推荐原因。

### Spec 和 Plan

SuperXP 区分会话内工作和跨会话过程文档：

- **Plan** 是一次会话内的执行跟踪。当工作可以在一次会话内完成、需要进度跟踪，或具有紧急性时，使用宿主工具自身的 Plan Mode。
- **Spec** 是具有生命周期的过程文档，用于一个会话无法可靠完成、需要跨会话或跨 agent 交接的复杂工作。
- **事故处理** 优先使用 Plan Mode：先稳定、缓解、验证，再在事后记录事故。

当当前会话需要多步骤排序、执行前达成一致，或需要面向用户展示进度跟踪时，Agents 应提示客户切换到宿主原生 Plan Mode。当 Plan Mode 结束并进入执行阶段时，Agents 必须使用宿主工具的 TODO 或 checklist 能力创建任务清单，并在执行过程中持续更新。

SuperXP 不创建默认的持久化 plan 文档。

### 文档结构

SuperXP 的文档结构应当 AI-first，并且符合 YAGNI：

- `docs/AGENTS.md` 定义面向 agents 的文档治理规则。
- `docs/templates/` 存放可复用模板。
- `docs/decisions/` 存放长期留存的 MADR 风格 ADR。
- `docs/incidents/` 存放长期留存的无责事故记录。
- `docs/specs/active/` 存放活跃的跨会话 Spec。
- `docs/specs/archive/` 只在短期保留有价值时存放历史 Spec。

Spec 过程文档使用：

```text
Epic -> Feature -> Story -> Scenario -> Task
```

实现顺序来自 User Story Mapping：

```text
Backbone -> Walking Skeleton -> Release Slices
```

代码、测试和 scoped `AGENTS.md` 仍然是最高权威的活文档。Epic 完成后，应将长期知识迁移到代码、测试、scoped `AGENTS.md`、ADR 或事故记录，然后归档或删除 Spec。

### Worktrees 和 Subagents

Worktrees 和 subagents 是一等的 agent 工程实践。

当需要保护工作区、支持回滚、进行并行试验或保持干净提交链时，使用 worktree 隔离。

当并行调查、独立审查、角色分离或上下文隔离能够降低风险或缩短反馈时间时，使用 subagents。

## 安装

请根据需要选择对应的安装通道。

### 正式版

正式版从 `main` 分支发布。

```bash
codex plugin marketplace add howiehu/superxp --ref main
```

### 开发版

开发版从 `dev` 分支发布。

```bash
codex plugin marketplace add howiehu/superxp --ref dev
```

如果是在已经克隆的本地仓库中进行开发，可以在仓库根目录安装 repo marketplace：

```bash
codex plugin marketplace add .
```

然后重启 Codex 或开启新的对话，打开插件目录，选择 SuperXP marketplace，并安装 `superxp`。

## 使用方式

SuperXP 不使用 hooks，也不应当在每一次对话中自动运行。只有当你明确选择它时，才使用 SuperXP：

- `/using-superxp`
- `$using-superxp`
- `$xp-loop`
- 以 `xp!` 开始用户消息，大小写均可，例如 `xp! help me slice this change`。

普通请求，例如 `fix this bug`、`use TDD` 或 `make a plan`，不应触发 SuperXP，除非你明确选择 SuperXP。

## 状态

SuperXP 当前处于初始化阶段。现阶段重点是让 v1 Codex 插件预览足够小，便于试用，同时足够具体，便于评估。

## 贡献

提交 issue 或 pull request 之前，请先阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可证

本项目使用 [LICENSE](LICENSE) 中列出的许可条款。
