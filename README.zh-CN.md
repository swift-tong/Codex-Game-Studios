# Codex Game Studios

[English](./README.md)

把一个 Codex 工作区扩展成结构化的独立游戏工作室流程。

`49` 个角色定义，`72` 个可复用技能，覆盖从概念到发布的完整工作流。

从这里开始：[AGENTS.md](./AGENTS.md) | [快速开始](./.agents/docs/quick-start.md) | [工作流指南](./docs/WORKFLOW-GUIDE.md)

## 这是什么

Codex Game Studios 是一个以 Codex 为核心的游戏开发模板，提供：

- 面向设计、架构、实现、QA 与发布的工作室化流程
- 位于 [`.agents/skills`](./.agents/skills) 的可复用技能
- 位于 [`.agents/agents`](./.agents/agents) 的角色定义
- 位于 [`.agents/docs`](./.agents/docs) 的共享规则、模板与流程文档
- 通过 [AGENTS.md](./AGENTS.md) 以及各子目录中的 `AGENTS.md` 提供项目级指令入口

这个仓库本身就是为了作为独立的 Codex 项目公开发布而整理的，`.agents/` 是主要集成面。

## 包含内容

| 类别 | 数量 | 说明 |
|---|---:|---|
| Agent 角色规范 | 49 | 包含导演、负责人、专家与引擎专项角色 |
| Skills | 72 | 覆盖概念设计、GDD、ADR、故事拆分、QA、发布与审计 |
| Rules | 11 | 面向代码、数据、测试和设计文档的路径级规则 |
| Templates | 39 | 包含 GDD、ADR、Sprint、UX、发布与审计模板 |
| 引擎参考 | 3 套 | Godot、Unity、Unreal 的参考快照与实践说明 |

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

## 在 Codex 中使用

1. 将仓库 clone 到你的工作区。
2. 在 Codex 中打开仓库。
3. 从 [AGENTS.md](./AGENTS.md) 开始。
4. 在聊天中直接调用技能，例如：
   - `$start`
   - `$brainstorm`
   - `$setup-engine godot 4.6`
   - `$project-stage-detect`
5. 让 Codex 按照本地 `AGENTS.md` 和 `.agents/skills` 继续协作。

如果你不是从零开始，而是接手一个已有项目，建议先运行 `$project-stage-detect` 和 `$adopt`。

## 推荐工作流

1. `$start`
2. `$brainstorm`，或者带着已有概念直接进入
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
