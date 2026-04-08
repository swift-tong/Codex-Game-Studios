# Codex Game Studios

[English README](./README.md)

把一个 Codex 工作区扩展成结构化的独立游戏工作室流程。

`49` 个角色定义，`72` 个可复用技能，覆盖从概念到发布的完整工作流。

从这里开始：[AGENTS.md](./AGENTS.md) | [快速开始](./.agents/docs/quick-start.md) | [工作流指南](./docs/WORKFLOW-GUIDE.md)

## 这是什么

Codex Game Studios 是一个以 Codex 为核心的游戏开发模板。它为项目提供：

- 面向设计、架构、实现、QA 和发布的工作室化流程
- 位于 [`.agents/skills`](./.agents/skills) 的可复用技能
- 位于 [`.agents/agents`](./.agents/agents) 的角色定义
- 位于 [`.agents/docs`](./.agents/docs) 的共享规则、模板和流程文档
- 通过 [AGENTS.md](./AGENTS.md) 以及各子目录中的 `AGENTS.md` 提供项目级指令入口

这个仓库本身就是为了作为独立的 Codex 项目公开发布而整理的，`.agents/` 是主要集成面。

## 包含内容

| 类别 | 数量 | 说明 |
|---|---:|---|
| Agent 角色规范 | 49 | 包含导演、负责人、专家和引擎专项角色 |
| Skills | 72 | 覆盖概念设计、GDD、ADR、故事拆分、QA、发布和审计 |
| Rules | 11 | 面向代码、数据、测试和设计文档的路径级规则 |
| Templates | 39 | 包含 GDD、ADR、Sprint、UX、发布和审计模板 |
| 引擎参考 | 3 套 | Godot、Unity、Unreal 的参考快照与最佳实践说明 |

## 仓库结构

```text
AGENTS.md
.agents/
  agents/        # 角色定义与角色提示
  docs/          # 流程文档、模板、参考资料
  rules/         # 路径级规范
  skills/        # Codex 技能
design/
  AGENTS.md
docs/
  AGENTS.md
  engine-reference/
production/
src/
  AGENTS.md
```

## 前置条件

在使用这个仓库之前，请确认你已经具备：

- 本地可用的 Codex 环境
- Shell 中可用的 Git
- 一个可以在 Codex 中打开该仓库的工作区

可选但有帮助的环境：

- Python 3，用于依赖 Python 工具链的项目或检查
- Node.js，用于依赖 JavaScript 工具链的项目或脚本

## 如何使用

这个仓库的使用方式是在 Codex 中打开，并通过对话驱动工作流。
它不是一个“直接运行”的游戏程序，而是一个用于规划、设计和构建游戏项目的指令面、流程面和模板面。

### 基本使用步骤

1. 将仓库 clone 到你的工作区。
2. 在 Codex 中打开仓库。
3. 从 [AGENTS.md](./AGENTS.md) 开始。
4. 如有需要，先阅读这些快速参考：
   - [快速开始](./.agents/docs/quick-start.md)
   - [工作流指南](./docs/WORKFLOW-GUIDE.md)
   - [技术偏好](./.agents/docs/technical-preferences.md)
5. 在聊天中直接调用技能，例如：
   - `$start`
   - `$brainstorm`
   - `$setup-engine godot 4.6`
   - `$project-stage-detect`
6. 让 Codex 按照本地 `AGENTS.md` 和 `.agents/skills` 继续协作。

### Codex 会读取什么

在这个仓库中工作时，Codex 主要会使用：

- [AGENTS.md](./AGENTS.md) 作为根指令文件
- [`.agents/skills`](./.agents/skills) 作为可复用工作流定义
- [`.agents/agents`](./.agents/agents) 作为角色定义
- [`.agents/docs`](./.agents/docs) 作为模板、规范和流程文档来源
- [`design/AGENTS.md`](./design/AGENTS.md)、[`docs/AGENTS.md`](./docs/AGENTS.md)、[`src/AGENTS.md`](./src/AGENTS.md) 这些分层指令文件

### 在 Codex 里怎么说

常见的使用方式如下：

- `Run $start`
- `Use $brainstorm to help me define a 2D roguelike`
- `Run $setup-engine godot 4.6`
- `Use $design-system for combat`
- `Run $project-stage-detect on this repo`
- `Read AGENTS.md and tell me the next step`

你可以直接点名技能，也可以用自然语言描述任务。

## 按场景使用

### 场景 1：从零开始做一个新游戏

如果你还没有现成游戏仓库，或者只有一个模糊想法，走这条路径：

1. 运行 `$start`
2. 运行 `$brainstorm` 生成并收敛游戏概念
3. 运行 `$setup-engine` 选择并配置引擎
4. 运行 `$map-systems` 识别系统和依赖关系
5. 对每个主要系统运行 `$design-system <system-name>`
6. 运行 `$review-all-gdds`
7. 运行 `$create-architecture`
8. 运行 `$create-epics`
9. 运行 `$create-stories`
10. 运行 `$dev-story` 开始实施

### 场景 2：接入已有游戏项目

如果你已经有代码、设计文档或生产文档，走这条路径：

1. 将这个模板复制或合并到现有仓库中
2. 确保根目录 [AGENTS.md](./AGENTS.md) 和 [`.agents`](./.agents) 树已经存在
3. 在 Codex 中打开仓库
4. 运行 `$project-stage-detect`
5. 运行 `$adopt`
6. 运行 `$gate-check` 查看进入下一阶段前缺什么
7. 根据建议用对应技能补齐缺口

### 场景 3：只使用模板的一部分

你不需要一次用完整条工作流。

常见的部分使用方式：

- 只用设计流程：`$brainstorm`、`$map-systems`、`$design-system`
- 只用架构流程：`$create-architecture`、`$architecture-decision`
- 只用生产流程：`$create-epics`、`$create-stories`、`$sprint-plan`
- 只用 QA / 发布流程：`$team-qa`、`$smoke-check`、`$release-checklist`

## 最小示例

如果你只想验证这个模板是否能正常工作，可以按最短路径执行：

1. 在 Codex 中打开仓库
2. 输入 `Run $start`
3. 然后输入 `Run $brainstorm for a small 2D action game`
4. 然后输入 `Run $setup-engine godot 4.6`
5. 然后输入 `Run $map-systems`

如果这些步骤能顺利执行，说明仓库已经可以在 Codex 中正常使用。

如果你是在已有项目中接入，而不是从零开始，优先从 `$project-stage-detect` 和 `$adopt` 开始。

## 推荐工作流

1. `$start`
2. `$brainstorm`，或者直接带着已有概念进入
3. `$setup-engine`
4. `$map-systems`
5. `$design-system`
6. `$review-all-gdds`
7. `$create-architecture`
8. `$architecture-decision`
9. `$create-control-manifest`
10. `$create-epics`
11. `$create-stories`
12. `$dev-story`
13. `$code-review`
14. `$story-done`
15. `$team-qa`
16. `$release-checklist`

## 常见产出

随着工作流推进，Codex 通常会创建或更新这些内容：

- `design/` 下的设计文档
- `docs/` 下的技术和架构文档
- `production/` 下的计划和生产文档
- `src/` 下的实现代码

这个仓库提供的是流程和模板，真正的游戏内容需要在此基础上逐步生成。

## Codex 原生说明

- 面向 Codex 的主要资产位于 [`.agents`](./.agents)
- 根目录和子目录中的 [AGENTS.md](./AGENTS.md) 是指令入口
- 技能内容遵循 Codex 路径约定，并应引用 `.agents/docs/...`

## 建议优先阅读

- [AGENTS.md](./AGENTS.md)
- [.agents/docs/quick-start.md](./.agents/docs/quick-start.md)
- [.agents/docs/coordination-rules.md](./.agents/docs/coordination-rules.md)
- [.agents/docs/technical-preferences.md](./.agents/docs/technical-preferences.md)
- [docs/COLLABORATIVE-DESIGN-PRINCIPLE.md](./docs/COLLABORATIVE-DESIGN-PRINCIPLE.md)

## 当前状态

这个仓库已经被整理为可独立存在的 Codex 项目，`AGENTS.md` 与 `.agents/` 是唯一的当前指令入口。

## License

[MIT](https://opensource.org/licenses/MIT)
