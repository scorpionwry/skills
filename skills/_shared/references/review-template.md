# Review 模板

用于 `.dev/skills/reviews/YYYY-MM-DD-<topic>.md`。

```markdown
# Review: <功能或变更名称>

## Verdict
Ready | Needs fixes | Blocked

## Blocking Issues
- None

## Important Issues
- None

## Minor Issues
- None

## Verification Evidence
- Command:
  Result:
- Manual check:
  Result:

## Spec Coverage
- [ ] Success criterion covered
- [ ] Success criterion covered

## Follow-ups
- None
```

规则：
- 先列 issues，再写 summary。
- Claim 不等于 evidence；记录命令、输出、截图或已检查文件。
- 仍有 Blocking 或 Important issues 时，不要标记 Ready。
