---
name: write-implementation-plan
description: 已有 spec 后使用，用于创建包含 tasks、verification commands 和 finish criteria 的 implementation plan，并保存到 .dev/skills/plans。
---

# write-implementation-plan

从 spec 创建决策完整但轻量的 implementation plan。

## 流程

1. 读取 spec，并检查相关代码、测试、package scripts 和本地约定。
2. 使用 `../_shared/references/plan-template.md` 的结构。
3. 优先拆成 vertical slices：每个 task 都应该产出可验证结果。
4. 如果仓库里能发现验证命令，写入精确命令。
5. 保存到 `.dev/skills/plans/YYYY-MM-DD-<topic>.md`。
6. 对行为逻辑推荐 `tdd-loop`，对任务序列推荐 `execute-plan`。

## 规则

- 本地模式够用时，不要引入新的大框架。
- 每个 task 都要有“Change / Verify / Evidence to record”。
- 如果 task 无法验证，拆分或重新设计。

## 输出

返回 plan 路径、task 数量和推荐执行路线。

## 停止条件

写完 plan 后停止，除非用户明确要求执行。
