---
name: dev-router
description: 当用户询问该使用哪个 dev-skills workflow，或任务属于新功能、bug 修复、小改动、planning、TDD、debugging、review 且不确定从哪里开始时使用。
---

# dev-router

把用户请求路由到最小可用的 dev-skills 流程。不要自动接管整个会话；只有在用户要求路由或明显不确定时使用。

## 流程

1. 判断请求属于下面哪条路线。
2. 推荐能保留验证纪律的最小 workflow。
3. 说明下一个应该调用的 skill，以及哪些步骤可以安全跳过。

## 路线

- 新功能或行为变更：`clarify-requirements` -> `write-light-spec` -> `write-implementation-plan` -> `tdd-loop` 或 `execute-plan` -> `review-and-finish`。
- Bug 或回归：`debug-systematically` -> `tdd-loop` -> `review-and-finish`。
- 小型机械改动：`execute-plan` -> `review-and-finish`，但必须记录验证证据。
- 已有 plan：使用 `execute-plan`；如果涉及行为逻辑，在执行中应用 `tdd-loop`。
- Review 或完成检查：使用 `review-and-finish`。

## 输出

用 1-3 条说明推荐路线，点名下一步要调用的 skill，并简要解释跳过的步骤。

## 停止条件

路由完成后停止，除非用户同时要求继续进入下一个 skill。
