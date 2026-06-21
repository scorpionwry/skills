---
name: tdd-loop
description: 实现 behavior、bug fix、business logic、API、data transformation 或测试时使用；执行 RED/GREEN/REFACTOR 和 behavior-first TDD。
---

# tdd-loop

通过 public interface 做 behavior-first TDD。测试应该描述系统做什么，而不是绑定私有实现细节。

## 流程

1. 找到 public interface 或最高价值的 test seam。
2. 为一个行为写一个 failing test。
3. 运行测试，确认失败能证明缺失行为。
4. 写最小实现让测试通过。
5. 运行 focused test 和相关周边测试。
6. 只有在 GREEN 时 refactor。
7. 为下一个行为重复循环。

## 规则

- 一次只覆盖一个行为。
- 尽量避免 mocks，除非外部系统让它不可避免。
- 如果没有好的 test seam，记录这个设计问题，并使用最窄但可靠的验证方式。
- 用户可以明确豁免 prototype、generated code 或纯配置。

## 输出

记录 RED/GREEN 证据：
- 新增的测试
- 观察到的失败
- 通过的命令
- Refactor 说明

## 停止条件

计划中的行为已经覆盖，或找不到可靠 test seam。
