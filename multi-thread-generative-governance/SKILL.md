---
name: multi-thread-generative-governance
description: Use when Codex needs to design, run, or document MTGG: a multi-thread or multi-session generative governance workflow with reusable team mode for repeated or lightweight work and full governance mode for high-risk, independent, auditable work. Trigger for MTGG, multi-session governance, independent perspectives, anti-contamination, red/blue/judge/audit workflows, session reuse, session registry, handoff capsules, monitored behavior paths, controlled writes, validation and audit loops, rule self-evolution, or optimizing MTGG itself.
---

# Multi-Thread Generative Governance

MTGG has two operating environments:

- `Reuse-Fast`: reuse an existing MTGG team for repeated, related, or lightweight work.
- `Full-Governance`: run strict independent-session governance for high-risk, high-value, or anti-contamination work.

The goal is not to open many chats. The goal is to improve artifact quality through role separation, controlled writes, validation, audit, and managed session reuse.

## Load References

Read references only when needed:

- `references/process-standard.md`: detailed G/W/R modes, role permissions, session lifecycle, run state, validation, audit, long-running safeguards.
- `references/templates.md`: compact templates for speed budget, session registry, handoff capsule, reuse decision, behavior path, validation, audit.
- `references/example-runs.md`: examples for light, standard, full, long-running, and skill self-optimization runs.

## First Move

Create a short task contract before opening or reusing threads:

1. Artifact type.
2. Literal user goal.
3. Deeper quality goal.
4. Allowed scope and forbidden scope.
5. Validation expectation.
6. Minimum effective improvement.
7. Chosen environment: `Reuse-Fast` or `Full-Governance`.

If the user is asking for another MTGG round in the same project, treat it as a continuation candidate, not a fresh team by default.

## Environment Selection

Use `Reuse-Fast` when all are true:

- Same project or same artifact family.
- Existing MTGG sessions are available or can be safely rebriefed.
- The new objective is related to previous work or does not require stricter isolation.
- The task is lightweight, iterative, or mainly asks for another round.
- Quality can be protected with a small role set, handoff capsule, and validation summary.

Use `Full-Governance` when any are true:

- User asks for true independent sessions, anti-contamination, or fresh perspectives.
- The task is high-risk, user-facing, large, cross-file, or long-running.
- Prior sessions are contaminated, stale, wrong-project, blocked, missing handoff, or overloaded.
- Multiple candidate artifacts, branches, or high-risk writes are involved.
- Validation failure, unclear scope, or audit concern requires escalation.

Hard rule: do not call same-session role passes "threads." True multi-thread MTGG requires independent Codex sessions and session evidence.

## Triage

Score three axes:

- Governance: `G1` light, `G2` standard, `G3` complex.
- Write mode: `W1` single writer, `W2` candidates, `W3` branches/patches.
- Runtime: `R0` short, `R1` medium/long, `R2` unattended/long-running.

Hard upgrades:

- Upgrade to `G2` for review, optimization, quality improvement, multi-section output, delivery to others, or red-team findings.
- Upgrade to `G3` for multi-file projects, whole-project optimization, true independent sessions, multiple executors, high refactor cost, runtime validation, or under-scoped goals.
- Upgrade to `R2` for 12+ hour work, unattended work, heartbeat-driven work, or local-device continuity.

After triage, choose:

- `Stop`: minimum improvement met and risks recorded.
- `ContinueCompressed`: one more bounded round.
- `EscalateFull`: hard trigger, high-risk finding, failed validation, unclear scope, or user request.

## Session Registry And Team Pool

Before creating sessions, inspect or create a session registry. This is mandatory for true independent-session work.

Each entry tracks:

- team id
- role
- thread id
- title
- project path
- scope tags
- status: `idle`, `assigned`, `waiting`, `blocked`, `expired`, `retired`
- lease owner and lease expiry
- last input summary
- last output pointer
- handoff capsule pointer
- contamination notes
- reuse eligibility: `reusable`, `needs_rebrief`, `not_reusable`

Reuse first:

1. Find compatible sessions by project, role, scope, isolation level, and status.
2. Reuse `idle` or `needs_rebrief` sessions by sending a role-local rebrief.
3. Create a new session only when reuse is unsafe or unavailable.
4. Record every reuse decision, including rejected candidate ids and reasons.
5. Report active, idle reusable, blocked, expired, and retired sessions at close.

Do not create duplicate role chains such as `红队-5`, `红队-5B`, `红队-8` without a team id, lease reason, and retirement plan.

## Handoff Capsules

Do not rely on a session "remembering" prior work. Use a compact handoff capsule for reuse, replacement, retirement, and resumption after unrelated chat.

A handoff capsule contains only durable role-local state:

- objective and scope lock
- allowed and forbidden files or inputs
- durable findings, decisions, validation state, and unresolved risks
- output pointers
- contamination notes
- cannot-claim limits
- next recommended action

When reusing a session, send the handoff capsule plus the new role-local task. When replacing a session, seed the replacement with the predecessor capsule and mark inherited facts separately from new instructions.

If no capsule exists, reconstruct one from records or state that continuity is not verified.

## Role Activation

Activate only roles with distinct responsibilities:

- Main: orchestrates, writes final, preserves boundaries.
- Red: finds risks; does not fix or approve.
- Blue: verifies/refutes/ranks risks; does not approve.
- Judge: allows, rejects, defers, or requests evidence.
- Executor: implements only after Judge `Allow`.
- Validator: verifies and records gaps; does not fix or overclaim.
- Auditor: checks boundary compliance and residual risk.
- Monitor: records observable behavior only.
- Watchdog/MergeJudge/RuleEvolver/specialists: add only when justified.

One strong closed loop is better than many noisy roles.

## Creating Or Reusing Sessions

For project work, use project-scoped sessions. Rename each session immediately before substantive delegation.

Chinese titles should be stable and short, such as `红队-A`, `蓝队-A`, `裁判-A`, `验证-A`, `审计-A`, `监测-A`, or role plus task tags like `红队-论文`.

Immediate naming is a gate:

1. Create or identify session.
2. Rename it.
3. Record registry entry.
4. Assign or renew lease.
5. Send task-local input.

If naming is missed, record the incident, remediate the title, and include it in audit.

Each role receives only:

- role
- project path
- current objective and attack surface
- allowed inputs/files
- forbidden inputs/files
- write policy
- output shape
- handoff capsule when continuity is required

Do not leak expected answers, judge preferences, or another role's output unless the role is explicitly reviewing that output.

## Scheduling

Parallelize independent work, not dependent decisions:

- Red, Goal, independent research, and Validator precheck may run in parallel.
- Blue waits for Red only when verifying Red findings.
- Judge waits for relevant evidence before authorizing writes.
- Executor waits for Judge `Allow`.
- Validator waits for the artifact or patch.
- Auditor can inspect process evidence in parallel but cannot approve content.
- Monitor runs throughout and records observable events only.

Each session may hold only one active lease. If a role is busy, wait, justify a backup, or defer.

## Write Control

Default to main-thread-only final writes.

- Background roles write only their outbox or return final responses.
- Executors write candidates, branches, or patches only after Judge approval.
- Candidate/branch merges require validation and merge decision.
- Rule evolution roles propose rules; they do not modify active rules directly.

Treat file writes, final claims, and rule changes as high-risk capabilities.

## Validation

Never let lower-level validation masquerade as higher-level proof:

- `L0`: static or structure checks.
- `L1`: build, format, or rule checks.
- `L2`: runtime or use-path checks.
- `L3`: experience or goal-achievement checks.

Every validation report separates:

- Verified.
- Failed.
- Not verified.
- Environment gaps.
- Cannot claim.

For skill work, L0 must check frontmatter, required files, reference paths, unresolved scaffold markers, and naming/registry rules. L2 for true multi-thread requests must verify independent session ids, short names, project ownership, minimal inputs, reuse decision, handoff capsule, and no expected-answer leakage.

## Behavior Recording

When the user asks for detailed records, or when using `Full-Governance`, create or assign Monitor.

Record all observable MTGG-guided actions:

- registry lookup
- reuse decision
- thread creation
- naming
- lease assignment or release
- prompts
- reads and writes
- decisions
- validation
- audit
- incidents and remediations

Do not record hidden reasoning. Prefer one unified run record when the user needs human-readable traceability.

## Run Workspace

For `Reuse-Fast`, use a compact record:

```text
task_contract.md
session_registry.md
handoff_capsules.md
decision.md
validation.md
final_report.md
```

For `Full-Governance`, R1/R2, or true independent sessions, preserve at minimum:

```text
task_contract.md
session_registry.md
session_evidence.md
handoff_capsules.md
behavior_path.md
judge_decision.md
validation_report.md
audit_log.md
latest_handoff.md
```

If the user asks for one document, consolidate these sections into one unified run record instead of scattering files.

## Output Discipline

User-facing updates should report:

- chosen environment and G/W/R mode
- reused roles and newly created roles
- why any new session was required
- minimum effective improvement
- validation limits
- next step

Keep progress updates short. Do not hide material risk, failed validation, boundary incidents, or cannot-claim limits.
