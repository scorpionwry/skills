---
name: write-light-spec
description: 需求清晰后使用，用于为 feature、behavior change 或 bugfix 写轻量 spec，并保存到 .dev/skills/specs。
---

# write-light-spec

把确认过的 Requirements Brief 写成短小、可持久化、可验证的 spec。

## 流程

1. 重新读取 brief、相关仓库文档，以及同主题已有的 `.dev/skills/specs` 文件。
2. 使用 `../_shared/references/spec-template.md` 的结构。
3. 将 spec 保存到目标项目的 `.dev/skills/specs/YYYY-MM-DD-<topic>.md`。
4. 只有在 open questions 不阻塞 planning 时才写入；阻塞问题要先问清楚。
5. 完成后交给 `write-implementation-plan`。

## 规则

- Success criteria 必须是可观察的 pass/fail 检查。
- 除非是硬约束，不要把实现细节写进 spec。
- 明确 out of scope，防止 scope creep。

## 输出

告诉用户 spec 路径，并总结已经锁定的关键决策。

## 停止条件

写完 spec 后停止，除非用户要求继续 planning。
