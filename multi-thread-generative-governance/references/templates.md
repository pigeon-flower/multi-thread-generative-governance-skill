# Templates

Copy and adapt these templates when creating a run workspace or documenting a governance loop.

## Table of Contents

1. Task Contract
2. Task Triage
3. Independent Thread Session Check
4. Forward-Test Eval Case
5. Goal Calibration
6. Round Scope
7. Red Team Report
8. Blue Team Response
9. Judge Decision
10. Validation Report
11. Audit Report
12. Skill Self-Optimization Round
13. Write Locks
14. Permission Incident
15. Rule Proposal
16. Runtime Health
17. Latest Handoff
18. README_RUN.zh.md

## Task Contract

```markdown
# Task Contract

任务类型：
目标产物：
核心目标：
深层目标：
本轮攻击面：
允许修改：
禁止修改：
验证方式：
截止条件：
完成标准：
最低有效改进：
```

## Task Triage

```markdown
---
schema: triage.v1
run_id:
status: READY
version: v001
---

# Task Triage

## 1. User Goal

原始目标：
重述目标：

## 2. Artifact Type

类型：
结构强度：强结构 / 半结构 / 弱结构 / 流程型

## 3. Scores

| Dimension | Score | Reason |
|---|---:|---|
| Artifact complexity A | | |
| Scope size S | | |
| Goal ambiguity G | | |
| Risk R | | |
| Verification difficulty V | | |
| Write complexity W | | |
| Duration D | | |

## 4. Selected Modes

- Governance: G1 / G2 / G3
- Write mode: W1 / W2 / W3
- Runtime: R0 / R1 / R2

## 5. Hard Triggers

- ...

## 6. Enabled Independent Sessions

| Role | User-Language Short Name | Session/Thread ID | Project Path | Status |
|---|---|---|---|---|
| Main | 主控-0 / Main-0 | | | active |
| Goal calibrator | 校准-1 / Goal-1 | | | pending / active / skipped |
| Red | 红队-1 / Red-1 | | | pending / active / skipped |
| Blue | 蓝队-1 / Blue-1 | | | pending / active / skipped |
| Judge | 裁判-1 / Judge-1 | | | pending / active / skipped |
| Executor | 执行-1 / Exec-1 | | | pending / active / skipped |
| Validator | 验证-1 / Val-1 | | | pending / active / skipped |
| Auditor | 审计-1 / Audit-1 | | | pending / active / skipped |
| Watchdog | 监控-1 / Watch-1 | | | pending / active / skipped |

## 7. Main-Proxied Role Passes

These are same-session role passes, not independent threads:

- Light red pass:
- Light judge pass:
- Light audit pass:

Cannot claim:

- Independent multi-thread review.
- Anti-contamination.
- Separate-session evidence.

## 8. Delegated Responsibilities

由主线程代管：
- ...

## 9. Minimum Effective Improvement

合格：

不合格：

## 10. Write Policy

...

## 11. Validation Policy

...

## 12. User Guide

README_RUN.zh.md：需要 / 不需要

## 13. Next Action

...
```

## Independent Thread Session Check

```markdown
# Independent Thread Session Check

## Basic Info

run_id:
project_path:
project_name:
check_time:
checked_by:

## Thread Registry

| Role | User-Language Short Name | Session/Thread ID | Source Thread ID | Project Path Confirmed | Input Source | Status |
|---|---|---|---|---|---|---|
| Main | 主控-0 / Main-0 | | | Yes / No | | PASS / FAIL |
| Red | 红队-1 / Red-1 | | | Yes / No | | PASS / FAIL |
| Blue | 蓝队-1 / Blue-1 | | | Yes / No | | PASS / FAIL |
| Judge | 裁判-1 / Judge-1 | | | Yes / No | | PASS / FAIL |
| Executor | 执行-1 / Exec-1 | | | Yes / No | | PASS / FAIL |
| Validator | 验证-1 / Val-1 | | | Yes / No | | PASS / FAIL |
| Auditor | 审计-1 / Audit-1 | | | Yes / No | | PASS / FAIL |

## Minimal Input Check

Each independent session received only:

- Role:
- Project path:
- Round scope / attack surface:
- Allowed files:
- Forbidden inputs:
- Write policy:
- Output format:

No session received:

- Expected answer:
- Main-thread preferred conclusion:
- Another session's conclusion before its stage:
- Judge decision before judge stage:
- Unrelated full-context dump:

## Project Ownership Check

- Session is under target project: Yes / No
- CWD or workspace root matches project path: Yes / No
- Output recorded in run workspace or role outbox: Yes / No
- Projectless or wrong-project session excluded from formal evidence: Yes / No

## Result

Overall: PASS / FAIL

Failures:

1. ...

Fixes:

1. ...
```

## Forward-Test Eval Case

```markdown
# Forward-Test Eval Case

## Eval ID

EVAL-001

## Realistic User Prompt

...

## Target Artifact / Input Files

- ...

## Expected Trigger Or Mode

...

## Pass Criteria

1. ...

## Fail Criteria

1. ...

## Observable Evidence

- Final response:
- Files created/changed:
- Session evidence:
- Validation report:

## No-Leak Session Prompt

Only include the skill path, project path, raw user request, allowed files, and role. Do not include expected answers, known bugs, intended fixes, or pass/fail criteria unless the test is explicitly about applying criteria.

Prompt shape:

    Use $skill-name at <skill_path> to handle the following user request:

    <raw user request>

## Baseline / Previous Iteration

- Baseline artifact:
- New artifact:
- Comparison method:

## Result

PASS / FAIL / NOT RUN

Notes:
```

## Goal Calibration

```markdown
# Goal Calibration

## Literal Goal

...

## Deeper Goal

...

## Reasonable Expansion

...

## Forbidden Expansion

...

## Minimum Effective Improvement

...

## Recommended Attack Surfaces

1. ...
```

## Round Scope

```markdown
# Round Scope R001

## Round Goal

...

## In Scope

- ...

## Out of Scope

- ...

## Allowed Finding Types

- ...

## Max Findings

...

## Minimum Effective Improvement

...

## Stop Conditions

- ...
```

## Red Team Report

```markdown
# Red Team Report R001

只读审查完成，未修改文件。

## Risk 1

定位：
触发场景：
影响：
证据：
最小验证：
严重度建议：

## Risk 2

...
```

## Blue Team Response

```markdown
# Blue Team Response R001

蓝队回应，不改文件。

## Finding 1

结论：成立 / 部分成立 / 不成立
严重度：高 / 中 / 低
理由：
最小处理：
验证方式：
是否交裁判：是 / 否

## Deferred / Rejected

- ...
```

## Judge Decision

```markdown
# Judge Decision R001

## Decision

Allow / Reject / Defer / NeedMoreEvidence

## Allowed Scope

1. ...

## Forbidden Scope

1. ...

## Required Validation

1. ...

## Evidence Basis

- Red:
- Blue:
- Source:

## Can Enter Execute

Yes / No

## Notes

不得使用“适当优化”“自行调整”“视情况处理”等模糊授权。
```

## Validation Report

```markdown
# Validation Report R001

## Validation Level Reached

- L0: completed / not completed
- L1: completed / not completed
- L2: completed / not completed
- L3: completed / not completed

## Verified

1. ...

## Failed

1. ...

## Not Verified

1. ...

## Evidence

- ...

## Environment Gaps

- ...

## Cannot Claim

本轮不能宣称：
- ...
```

## Audit Report

```markdown
# Audit Report R001

## Basic Info

run_id:
round_id:
time:
auditor:

## Goal

本轮目标：
最低有效改进标准：

## Process Trace

- Triage:
- GoalCalibration:
- ScopeLock:
- RedReview:
- BlueReview:
- JudgeDecision:
- Execute:
- Validate:
- Retest:

## Boundary Check

裁判允许边界：
实际修改边界：
是否越界：
证据：

## Change Summary

实际改动：
涉及产物：
涉及文件：

## Validation Summary

已验证：
未验证：
验证失败：
不能宣称：

## Scores

产物质量评分：
流程治理评分：

## Residual Risks

1. ...

## Next Round Suggestions

1. ...

## Handoff Summary

下一线程接管时应读取：
- ...
```

## Skill Self-Optimization Round

```markdown
# Skill Self-Optimization Round R001

## Task Contract

目标 Skill：
本轮攻击面：
最低有效改进：
允许修改：
禁止修改：

## Triage

- Governance: G3
- Write mode: W1 / W2 / W3
- Runtime: R0 / R1 / R2
- Enabled independent sessions:
- Main-proxied role passes:

## Eval Contract

| Eval ID | Realistic Prompt | Expected Behavior | Pass Criteria | Fail Criteria | Baseline |
|---|---|---|---|---|---|
| EVAL-001 | | | | | |

No-leak forward-test prompt:

- Includes:
- Excludes:

Artifacts to capture:

- Baseline output:
- New output:
- Session evidence:
- Validation report:

## Session Evidence

| Role | User-Language Short Name | Session/Thread ID | Project Path | Input Summary | Status |
|---|---|---|---|---|---|
| Main | 主控-0 / Main-0 | | | | |
| Red | 红队-1 / Red-1 | | | | |
| Blue | 蓝队-1 / Blue-1 | | | | |
| Judge | 裁判-1 / Judge-1 | | | | |
| Eval | 评测-1 / Eval-1 | | | | |

## RedReview

### Finding 1

定位：
风险：
触发场景：
证据：
最小验证：

## BlueReview

结论：成立 / 部分成立 / 不成立
理由：
最小处理：

## JudgeDecision

Decision: Allow / Reject / Defer / NeedMoreEvidence

Allowed scope:
- ...

Forbidden scope:
- ...

Required validation:
- ...

## Execution

修改文件：
- ...

修改摘要：
- ...

## Validation

L0:
L1:
L2:
L3:

Eval results:
- ...

Session isolation:
- Independent session ids verified: Yes / No
- Short anonymous names verified: Yes / No
- Project ownership verified: Yes / No
- Expected-answer leakage checked: Yes / No

Cannot claim:
- ...

Environment gaps:
- ...

## Audit

是否符合裁判边界：
是否还有残留风险：
是否需要下一轮：
下一轮建议：
```

## Write Locks

```markdown
# Write Locks

## Active Locks

| Lock ID | Target | Locked By | Mode | Status | Since | Expires | Reason |
|---|---|---|---|---|---|---|---|
| L001 | 05_artifacts/final/report.md | main | exclusive | active | | | applying approved changes |

## Rules

1. final/ 默认只能由 main 加锁写入。
2. candidates/{role}/ 只能由对应角色加锁写入。
3. branches/{role}/ 只能由对应角色加锁写入。
4. 锁过期后不能自动视为安全，必须由主线程或设备监控线程报告。
5. 任何线程发现锁冲突，必须停止写入并报告 BLOCKED。
```

## Permission Incident

```markdown
# Permission Incident

## Incident ID

INC-001

## Type

文件越权 / 阶段越权 / 范围越权 / 规则越权 / 结论越权

## Detected By

...

## Role Involved

...

## Description

...

## Evidence

- ...

## Immediate Action

- ...

## Resolution

待处理
```

## Rule Proposal

```markdown
# Rule Proposal RUL-PROP-001

## Trigger

触发来源：
- ...

## Problem

当前流程问题：

## Evidence

1. ...

## Proposed Rule

规则名称：
规则等级：
适用范围：
规则内容：

## Expected Benefit

...

## Possible Side Effects

...

## Suggested Status

Draft / Candidate / Trial

## Required Decision

是否允许进入 Trial：
```

## Runtime Health

```markdown
# Runtime Health Report

## Status

Normal / Warning / Blocked / Critical

## Checks

- Device awake:
- Network:
- Workspace writable:
- Disk:
- Heartbeat:
- Thread status:
- Locks:
- Deadline:

## Problems

1. ...

## Recommended Action

Continue / Notify Main / Create Takeover / Stop New Rounds
```

## Latest Handoff

```markdown
# Latest Handoff

## Objective

...

## Current Round

...

## Current Stage

...

## Last Judge Decision

...

## Implemented Changes

- ...

## Verification

已验证：
- ...

未验证：
- ...

## Open Risks

- ...

## Locks / Incidents

- ...

## Next Action

...
```

## README_RUN.zh.md

```markdown
# 本次多线程生成任务说明

## 1. 本次任务

任务目标：
产物类型：
运行模式：

## 2. 为什么使用这个模式

系统判断：
- ...

因此选择：
- 治理强度：
- 写入模式：
- 运行保障：

## 3. 本次开启的独立 session

| 角色 | 用户语言短名称 | Session/Thread ID | 状态 | 做什么 |
|---|---|---|---|---|
| 主线程 | 主控-0 | | | 协调、最终写入 |
| 红队 | 红队-1 | | | 找风险 |
| 蓝队 | 蓝队-1 | | | 复核和筛选 |
| 裁判 | 裁判-1 | | | 允许/拒绝/延期 |
| 验证 | 验证-1 | | | 检查证据 |
| 审计 | 审计-1 | | | 查流程合规 |
| 设备监控 | 监控-1 | | | 心跳、接管、锁 |

主线程代理的轻量角色：

- ...

## 4. 文件夹怎么看

- 01_task/：任务说明
- 02_state/：当前状态
- 03_bus/：线程通信
- 04_decisions/：裁判决定
- 05_artifacts/：产物
- 06_validation/：验证
- 07_audit/：审计
- 08_locks/：写入锁
- 09_handoff/：接管信息

## 5. 用户主要看哪里

最终结果：
- 05_artifacts/final/

修改原因：
- 04_decisions/judge_decision.md
- 07_audit/audit_log.md

恢复任务：
- 09_handoff/latest_handoff.md

## 6. 用户可以安全修改哪里

可以修改：
- 01_task/user_feedback.md
- 01_task/user_override.md

不建议修改：
- 02_state/current_state.md
- 04_decisions/judge_decision.md
- 08_locks/write_locks.md

## 7. 中断后怎么办

1. 查看 latest_handoff.md
2. 查看 current_state.md
3. 检查 thread_status.md
4. 让主线程根据接管文件继续

## 8. 最终交付

最终产物位置：
- ...

验证摘要：
- ...

审计摘要：
- ...

本轮不能宣称：
- ...
```
