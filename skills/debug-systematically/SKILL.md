---
name: debug-systematically
description: 诊断 bugs、regressions、flaky behavior、failing tests、performance issues，或用户说调试/排查时使用；修复前先建立 reproduction loop。
---

# debug-systematically

基于证据调试，而不是猜。修改生产代码前先建立 feedback loop。

## 流程

1. Reproduce：创建或找到一个能显示症状的命令、测试、脚本或手动步骤。
2. Minimize：缩小输入和步骤，只保留会导致问题的关键部分。
3. Hypothesize：列出 3-5 个按可能性排序的原因，并写出可证伪预测。
4. Probe：一次验证一个假设，使用有目标的检查或 instrumentation。
5. Fix：针对已证明的原因做最小修复。
6. Regress：如果有合适 seam，把最小复现沉淀成测试。
7. Cleanup：移除临时探针，写下验证证据。

## 规则

- 除非用户明确接受风险，否则不要在复现前实现 fix。
- 临时 debug logs 使用唯一标记，完成前移除。
- 如果复现需要用户或环境输入，明确说明缺少什么 artifact。

## 输出

返回：
- Reproduction command 或 steps
- Minimized case
- 选中的 hypothesis 和 evidence
- Fix summary
- Regression / verification evidence

## 停止条件

原始症状已修复且验证通过，或复现被外部条件阻塞。
