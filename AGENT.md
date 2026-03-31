# AI Harness Engineering 协议

## 目标
通过低 token、分阶段、多角色协作的方式推进软件开发。

## 核心规则
优先消费稳定结论，而不是原始讨论历史。始终先读取最小可用上下文。
每个阶段的实际产出必须由对应的 subagent 完成，主控只负责分派、收敛与验收。

## 仓库分层
1. 全局协议：`AGENT.md`、`ROLE_INDEX.yaml`、`workflows/`
2. 角色契约：`roles/`
3. 可复用模板：`templates/`
4. 项目真相层：`projects/<project>/project.yaml`、`state.yaml`、`memory/`、`tasks/`
5. 阶段工作区：`projects/<project>/stages/`

## 默认执行顺序
1. Requirements（需求）
2. Architecture（架构）
3. Build（构建）
4. Testing（测试）
5. Release（发布）

## 默认读取顺序
1. `projects/<project>/state.yaml`
2. `projects/<project>/memory/current-focus.md`
3. `projects/<project>/tasks/active.yaml`
4. `roles/` 中对应的角色文件
5. 当前阶段的 `summary.md`
6. 当前阶段的 `decisions.md`
7. 当前阶段的 `open-questions.md`
8. 仅按 `artifact-index.yaml` 读取所需产物
9. 需要追溯时再读取 `discussion-index.yaml`
10. 只有当摘要不足时才读取原始讨论文件

## 协作规则
- 只激活当前阶段真正需要的角色。
- 每个阶段必须绑定至少一个 subagent 作为执行者。
- 每个角色都必须声明输入、输出和完成标准。
- Orchestrator 不直接代替阶段角色产出正式阶段成果，只负责创建 subagent、分发上下文、验收结果和推进状态。
- 原始讨论属于归档材料，不应作为默认工作上下文。
- 在继续堆积讨论之前，先更新阶段摘要和决策记录。
- 正式产物按主题拆分，不保留单个超长文档。

## Subagent 执行模型
- Requirements 阶段由 `analyst` subagent 执行。
- Architecture 阶段由 `architect` subagent 执行。
- Build 阶段默认拆为 `frontend` subagent 与 `backend` subagent 并行执行，必要时由 orchestrator 汇总集成结果。
- Testing 阶段由 `tester` subagent 执行。
- Release 阶段由 `devops` subagent 执行。
- 如果一个阶段需要多轮讨论，仍由同类型或同职责 subagent 反复迭代，不切换为主控直接完成。

## 质量门禁
- 在需求范围和摘要未稳定前，不进入架构阶段。
- 在架构决策未记录前，不进入构建阶段。
- 在测试结果和运维检查未记录前，不进入发布阶段。

## 状态管理
- `state.yaml` 是当前阶段与阻塞项的唯一真相源。
- `memory/current-focus.md` 用来定义当前轮次的收敛目标。
- `tasks/active.yaml` 保存当前活跃角色的可执行任务卡。
- `state.yaml` 与 `tasks/active.yaml` 需要显式标注当前阶段对应的 subagent 执行者。

## 升级规则
- 如果缺少必要输入，在 `open-questions.md` 中新增问题项。
- 如果某项决策会影响多个后续阶段，同步写入 `memory/global-decisions.md`。
- 如果讨论变得冗长混乱，先压缩进 `summary.md`，再把原始内容归档。
