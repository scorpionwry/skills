# Light Spec 模板

用于 `.dev/skills/specs/YYYY-MM-DD-<topic>.md`。

```markdown
# <功能或变更名称>

## Goal
一句话说明用户可见的结果。

## Success Criteria
- [ ] 可观察、可判断 pass/fail 的结果
- [ ] 可观察、可判断 pass/fail 的结果

## In Scope
- 本次明确交付的行为或产物

## Out of Scope
- 明确排除的相邻工作

## Constraints
- 技术、产品、兼容性、安全或依赖约束

## Risks
- 风险和缓解方式，或写“None known”

## Open Questions
- 问题、负责人、无人回答时的默认选择
```

规则：
- 使用具体、用户可观察的结果。
- 保持 spec 足够短，方便实现前重读。
- 如果某个问题阻塞 planning，先问清楚再写最终 spec。
