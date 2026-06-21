---
name: clarify-requirements
description: 在实现新功能、行为变更、产品改动或不清晰任务前使用；逐步澄清 goal、success criteria、constraints 和 scope。
---

# clarify-requirements

在实现前澄清意图。能从仓库中发现的事实先自己检查；只向用户询问产品选择、取舍或缺失决策。

## 流程

1. 先检查相关文档、代码、测试和既有模式。
2. 一次只问一个高影响问题。
3. 锁定这些字段：goal、用户/受众、success criteria、in scope、out of scope、constraints、risks 和默认选择。
4. 总结已经锁定的理解。
5. 如果后续要实现，交给 `write-light-spec`。

## 提问规则

- 只问会实质改变工作的事项。
- 优先给出带推荐默认值的多选项。
- 如果某个决策可以安全默认，记录默认值，不要阻塞。

## 输出

返回简洁的 Requirements Brief：
- Goal
- Success criteria
- Scope
- Constraints
- Open questions 或 defaults

## 停止条件

用户认可 brief，或已经没有阻塞性的歧义。
