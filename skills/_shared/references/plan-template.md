# Implementation Plan 模板

用于 `.dev/skills/plans/YYYY-MM-DD-<topic>.md`。

```markdown
# <功能或变更名称> Implementation Plan

## Goal
一句话，和已批准的 spec 保持一致。

## Strategy
用 2-4 条说明实现策略和关键取舍。

## Tasks

### Task 1: <名称>
- Change:
- Verify:
- Evidence to record:

### Task 2: <名称>
- Change:
- Verify:
- Evidence to record:

## Finish Criteria
- [ ] 必要命令通过
- [ ] Spec success criteria 已覆盖
- [ ] 变更完成后写入 review 文件

## Rollback / Follow-up
- Rollback:
- Follow-up:
```

规则：
- 每个 task 都必须产出可验证结果。
- 优先 vertical slice，而不是只按技术层拆分。
- 如果仓库里有明确命令，写入精确 verification command。
