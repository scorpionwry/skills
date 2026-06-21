# dev-skills

`dev-skills` 是一个轻量的软件开发技能包，用来帮助编码代理按更可靠的节奏完成需求澄清、轻量规格、实现计划、TDD、调试、执行和收尾审查。

哲学思想：

- 先澄清、再规格、再计划、再验证。
- 关键结论写入 `.dev/skills/`，方便跨会话恢复。
- 每个技能只做一件事，不用完整流程系统接管项目。

首版覆盖 Codex 和 Claude Code。它不会自动注入会话，也不会创建完整 CLI、状态机、并行 wave 或大型 `.planning/` 目录。

## 安装形态

仓库根目录就是插件根目录：

```text
.
├── .codex-plugin/plugin.json
├── .claude-plugin/plugin.json
├── skills/
└── README.md
```

Codex 使用 `.codex-plugin/plugin.json` 读取 `skills/`。Claude Code 使用 `.claude-plugin/plugin.json` 中列出的技能路径。其他运行时可以后续添加对应 manifest，但不影响当前技能本体。

## Quickstart

从 GitHub 安装：

```bash
npx skills@latest add scorpionwry/skills
```

只查看可安装 skills：

```bash
npx skills@latest add scorpionwry/skills --list
```

只安装某几个 skills：

```bash
npx skills@latest add scorpionwry/skills --skill dev-router --skill tdd-loop
```

安装到指定 agent：

```bash
npx skills@latest add scorpionwry/skills --agent codex
npx skills@latest add scorpionwry/skills --agent claude-code
```

## 推荐执行流程

### 新功能或行为变更

推荐流程：

```text
clarify-requirements
-> write-light-spec
-> write-implementation-plan
-> tdd-loop / execute-plan
-> review-and-finish
```

适用于新增功能、用户可观察行为变化、跨文件改动、产品规则调整。产物通常包括：

```text
.dev/skills/specs/YYYY-MM-DD-<topic>.md
.dev/skills/plans/YYYY-MM-DD-<topic>.md
.dev/skills/reviews/YYYY-MM-DD-<topic>.md
```

可以跳过 `clarify-requirements` 的情况：用户已经给出明确目标、成功标准、范围和约束。可以跳过 `write-light-spec` 的情况：改动非常小且计划文件已经足够表达需求。涉及行为逻辑时优先使用 `tdd-loop`；纯机械改动可直接走 `execute-plan`，但仍要记录验证证据。

### Bug 修复

推荐流程：

```text
debug-systematically
-> tdd-loop
-> review-and-finish
```

适用于失败测试、线上缺陷、回归、性能异常、偶发问题。`debug-systematically` 先建立复现循环，再最小化问题、列假设、验证原因。修复后用 `tdd-loop` 把最小复现沉淀为回归测试；如果没有合适测试接口，要在审查记录里说明原因和替代验证。

### 小改动

推荐流程：

```text
execute-plan
-> review-and-finish
```

适用于文案、配置、简单重命名、局部机械调整。可以不写 spec，但必须明确：

- 改了什么
- 如何验证
- 是否有用户可见影响

如果小改动过程中发现范围扩大，回到 `clarify-requirements` 或 `write-light-spec`。

## 完整示例：新增导出 CSV 功能

用户请求：

```text
帮我给订单列表增加导出 CSV 功能。
```

### 1. 澄清需求

使用 `clarify-requirements`，代理先确认关键产品选择：

```text
导出当前筛选结果，还是全部订单？
字段顺序是否固定？
最大导出行数是多少？
哪些角色可以导出？
```

得到 Requirements Brief：

```text
Goal: 用户可以从订单列表导出当前筛选结果为 CSV。
Success criteria:
- 导出的 CSV 只包含当前筛选条件下的订单
- 字段顺序固定为订单号、客户名、金额、状态、创建时间
- admin 和 manager 可以看到导出入口
- 普通用户看不到导出入口
Constraints:
- 首版同步下载，最大 5000 行
- 不做后台异步任务
```

### 2. 写轻量规格

使用 `write-light-spec`，生成：

```text
.dev/skills/specs/2026-06-21-export-orders-csv.md
```

规格包含目标、成功标准、范围、约束、风险和开放问题。它不需要写实现细节，只锁定用户可观察结果。

### 3. 写实现计划

使用 `write-implementation-plan`，生成：

```text
.dev/skills/plans/2026-06-21-export-orders-csv.md
```

计划示例：

```markdown
# Export Orders CSV Implementation Plan

## Goal

订单列表支持按当前筛选条件导出 CSV。

## Strategy

- 复用订单列表已有筛选参数。
- 后端新增 CSV 导出接口并限制最大 5000 行。
- 前端按钮只负责携带当前查询参数并触发下载。

## Tasks

### Task 1: 后端 CSV 接口

- Change：新增导出接口，复用订单筛选逻辑，输出固定字段顺序。
- Verify：运行订单导出接口测试，覆盖权限、筛选、字段顺序。
- Evidence to record：测试命令和结果。

### Task 2: 前端导出按钮

- Change：在订单列表工具栏增加导出入口，携带当前筛选参数。
- Verify：运行组件或集成测试，覆盖权限可见性和参数传递。
- Evidence to record：测试命令和结果。

### Task 3: 收尾验证

- Change：手动验证真实下载文件。
- Verify：检查文件名、编码、字段顺序和筛选结果。
- Evidence to record：手动验证结论。
```

### 4. 执行与 TDD

涉及接口行为和权限逻辑时使用 `tdd-loop`：

```text
RED: 写接口测试，断言筛选结果和字段顺序
GREEN: 实现最小 CSV 导出
REFACTOR: 复用已有订单筛选逻辑
```

执行任务时使用 `execute-plan`，每个任务完成后记录：

```text
Task：后端 CSV 接口
Files changed：...
Verification：npm test orders-export.test.ts
Result：pass
Remaining：前端按钮
```

### 5. 审查收尾

使用 `review-and-finish`，生成：

```text
.dev/skills/reviews/2026-06-21-export-orders-csv.md
```

审查记录包含阻断问题、重要问题、轻微问题、验证证据、规格覆盖和最终 verdict。

最终产物树：

```text
.dev/skills/
├── specs/
│   └── 2026-06-21-export-orders-csv.md
├── plans/
│   └── 2026-06-21-export-orders-csv.md
└── reviews/
    └── 2026-06-21-export-orders-csv.md
```

## 技能索引

| Skill                       | 用途                                   |
| --------------------------- | -------------------------------------- |
| `dev-router`                | 不确定从哪里开始时，选择最小可用流程。 |
| `clarify-requirements`      | 实现前澄清目标、成功标准、范围和约束。 |
| `write-light-spec`          | 写轻量规格到 `.dev/skills/specs/`。    |
| `write-implementation-plan` | 写可执行计划到 `.dev/skills/plans/`。  |
| `execute-plan`              | 按计划执行任务并记录验证证据。         |
| `tdd-loop`                  | 对行为逻辑执行 RED/GREEN/REFACTOR。    |
| `debug-systematically`      | 先复现、再最小化、再假设验证和修复。   |
| `review-and-finish`         | 完成前审查、验证、写收尾记录。         |

## 产物目录约定

使用者项目中的开发产物放在 `.dev/skills/`：

```text
.dev/skills/
├── specs/
├── plans/
├── reviews/
└── handoffs/
```

目录按需创建。`specs/` 记录需求和成功标准；`plans/` 记录可执行任务；`reviews/` 记录完成前审查；`handoffs/` 记录跨会话恢复信息。

## 设计取舍

- 保留纪律，但不强制所有任务走完整流程。
- 保留持久化产物，但不用大型项目状态系统。
- 保留 TDD，但允许用户明确豁免原型、生成代码和纯配置。
- 保留审查，但不默认启动并行代理或跨模型评审。
- 保留多运行时外壳，但首版只维护 Codex 与 Claude Code manifest。
