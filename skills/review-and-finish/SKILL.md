---
name: review-and-finish
description: 在声明完成、开 PR 或 handoff 前使用；执行 code review、verification summary、completion check，并写入 .dev/skills/reviews。
---

# review-and-finish

在说“完成”前审查变更。先列 findings，再给 summary。

## 流程

1. 读取相关 spec、plan 和当前 diff。
2. 检查 correctness、scope drift、missing tests、fragile design 和 verification gaps。
3. 运行或核验 plan 承诺的验证证据。
4. 使用 `../_shared/references/review-template.md` 的结构。
5. 对重要或用户可见工作，保存到 `.dev/skills/reviews/YYYY-MM-DD-<topic>.md`。
6. 给出 verdict：Ready、Needs fixes 或 Blocked。

## 严重级别

- Blocking：交付前必须修复。
- Important：交付前应该修复，除非用户接受风险。
- Minor：可以作为 follow-up 或 polish。

## 输出

返回：
- 按严重级别排序的 findings
- Verification evidence
- Spec coverage
- Final verdict
- Follow-ups

## 停止条件

所有 Blocking 和 Important 问题都已解决，或被用户明确接受。
