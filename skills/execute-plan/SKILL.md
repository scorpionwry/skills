---
name: execute-plan
description: 执行已有 plan 时使用；逐 task 推进，记录 verification evidence，并在行为变更中按需使用 tdd-loop。
---

# execute-plan

执行 plan，但不把会话变成重型状态机。保持清楚的变更记录和验证证据。

## 流程

1. 读取 plan 和引用的 spec。
2. 检查当前 git status，不覆盖无关的用户改动。
3. 一次执行一个 task。
4. 涉及行为逻辑时，在 task 内使用 `tdd-loop`，除非用户明确豁免。
5. 运行该 task 的 verification command，并记录证据。
6. 如果工作跨会话，在 `.dev/skills/handoffs/YYYY-MM-DD-<topic>.md` 追加或创建简短执行记录。
7. 所有 task 完成后使用 `review-and-finish`。

## 规则

- 验证失败时，不要继续下一个 task；先修复或报告。
- 变更范围保持在 plan 内。
- 如果 plan 错了，先更新 plan 或询问，不要随意发挥。

## 输出

每个完成的 task 报告：
- Task name
- Files changed
- Verification evidence
- Remaining work

## 停止条件

所有 task 完成、被阻塞，或 plan 需要新的决策。
