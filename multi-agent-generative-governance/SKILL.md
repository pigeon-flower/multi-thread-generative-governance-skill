---
name: multi-agent-generative-governance
description: Use when Codex needs to design, run, evaluate, or document a controlled multi-agent or multi-thread adversarial generation workflow for complex artifacts such as code projects, documents, PPTs, images, stories, product plans, study materials, skill packages, or long-running AI self-review tasks. Trigger when the user asks for 多线程对抗式生成, 多线程会议, 多 session, 独立视角, 防信息污染, 多角色生成治理, AI self-review, red/blue/judge/audit workflows, rule self-evolution, run workspace protocols, controlled candidate/branch writing, verification/audit loops, skill optimization governance, or turning such a process into a standardized skill or SOP.
---

# Multi-Agent Generative Governance

## Operating Principle

Treat this as a quality governance workflow, not as "open many chats and hope quality improves."

In this skill, a `thread` means a delegated unit backed by an independent Codex session. Same-session red/blue/judge work is a `role pass`, not a thread, and must not be claimed as independent multi-thread review.

Prioritize cognitive role separation, controlled writes, layered verification, and auditability. Do not create every role by default. First triage the task and choose only the governance strength, write mode, session isolation, and runtime safeguards that the task justifies.

Use these references only when needed:

- `references/process-standard.md`: full G/W/R mode rules, session model, roles, permissions, state machine, validation, audit, rule evolution, long-running safeguards.
- `references/templates.md`: copyable Markdown templates for task contract, triage, independent session evidence, permissions, scope lock, decisions, validation, audit, handoff, and user guide.
- `references/example-runs.md`: compact examples for G1, G2, G3, R2, skill self-optimization, and forward-test eval cases.

## First Move

Before proposing threads or edits, create a short Task Contract:

1. Identify the artifact type.
2. Restate the user's literal goal.
3. Infer the deeper quality goal.
4. List allowed scope, forbidden scope, validation expectations, and deadline.
5. Define the minimum effective improvement: what would count as a real improvement instead of a shallow token gesture.

If key information is missing, make a conservative assumption and record it. Ask only when a wrong assumption would cause risky writes, user-visible misdirection, or wasted long-running work.

Then select the smallest governance mode that can satisfy the Task Contract. Do not create independent sessions, run workspaces, or role artifacts merely because the skill can support them.

## Self-Optimization Mode

When the artifact is this skill or another skill, treat the skill folder as a multi-file documentation artifact. Use `G3/W1/R0` by default unless the user asks for independent sessions, long-running review, candidate comparison, or branch-based experimentation.

Run one bounded self-review loop:

1. Task Contract: define what real improvement means for the skill, not just prose polish.
2. Eval Contract: define realistic eval prompts, expected behavior, pass/fail criteria, observable evidence, and an old-skill or previous-iteration baseline when practical.
3. ScopeLock: choose one attack surface such as trigger accuracy, session isolation, role workflow, validation integrity, template completeness, or example coverage.
4. RedReview: identify concrete failure modes where a future Codex might misuse the skill.
5. BlueReview: reject preference-only findings and keep fixes minimal.
6. JudgeDecision: allow only specific file and section edits.
7. Execute: edit the source skill files only after judge approval.
8. Validate: check required files, frontmatter, references, unresolved scaffold markers, basic usability, and the eval contract. Use fresh independent sessions for complex forward-tests when available.
9. Audit: record what changed, what remains unverified, and whether another self-evolution round is justified.

Do not recursively optimize forever. One self-optimization round must either close, create a focused next-round suggestion, or defer to a later user request.

## Triage

Score the task on three independent axes:

- Governance strength: `G1` light, `G2` standard governance, `G3` complex project.
- Write mode: `W1` single writer, `W2` candidate artifacts, `W3` branches or patches.
- Runtime safeguard: `R0` short task, `R1` medium/long task, `R2` long-running or unattended.

Use hard upgrades:

- Upgrade to `G2` when the task asks for review, optimization, quality improvement, multi-page or multi-section output, delivery to others, or red-team findings.
- Upgrade to `G3` for multi-file code/projects, whole-project optimization, sustained adversarial generation, multiple executors, high refactor cost, runtime/build/experience validation, true independent sessions, or goals likely to be under-scoped.
- Upgrade to `R2` for 12+ hour, 24-hour, unattended, multi-round, local-device-dependent, or heartbeat-driven work.
- Treat "多线程", "多会议", "多 session", "独立视角", "防信息污染", and equivalent wording as a hard isolation trigger. If non-main threads are enabled, each one must be an independent Codex session under the correct project or workspace.
- Open goal calibration whenever the user says "整体优化", "完善", "长期训练", "提升质量", or the task is broad enough that AI may reduce it to a trivial fix.

For the detailed scoring matrix and hard triggers, read `references/process-standard.md`.

## Role Activation

Activate roles according to the selected mode:

- `G1/W1/R0`: main session only; optionally perform a light same-session red-team role pass. Main may proxy simple judge/audit duties only when independent review is not required.
- `G2`: main plus selected red, blue, and judge sessions when independent review is required; otherwise use clearly labeled main-proxied role passes. Add goal calibration, validator, or light auditor when goals are broad or output is important.
- `G3`: main, goal calibrator, red, blue, judge, executor, validator, and auditor as independent sessions when activated. Add rule evolver, merge judge, specialist red/blue teams when justified.
- `R2`: add watchdog, heartbeat, thread status, session evidence, write locks, latest handoff, expiry stop, and takeover mechanism.

Do not let role count become the objective. One high-quality closed loop is better than many noisy findings.

## Independent Thread Sessions

When the user asks for multi-thread, multi-meeting, multi-session, independent perspectives, anti-contamination, or roles that should not see each other's reasoning, every enabled thread must be a separate Codex session. If you cannot create, read, or coordinate independent sessions, say so and either ask permission to downgrade to same-session role passes or mark the requested multi-thread step blocked.

Create project-scoped sessions for project work, not projectless sessions. Rename each session immediately with a short anonymous readable title in the user's language; do not use pasted task text as the session name. For Chinese users, prefer names such as `红队-1`, `蓝队-1`, `裁判-1`, `评测-1`, `验证-1`, or `审计-1`. For English users, use `Red-1`, `Blue-1`, `Judge-1`, `Eval-1`, `Val-1`, or `Audit-1`.

Give each session only task-local input: role, project path, allowed files, forbidden inputs, output shape, write policy, and the current attack surface. Do not leak expected answers, judge preferences, another session's conclusion, or the main thread's private reasoning unless that role is explicitly supposed to review prior outputs.

Record session evidence before claiming true multi-thread work:

- role and short title
- session/thread id
- source thread id when available
- project path or workspace root
- input summary and forbidden inputs
- read/write permission
- output path or final response pointer
- status

Without this evidence, describe the work as a same-session role pass, not multi-thread governance.

## Standard Loop

Use this loop for standard and complex work:

```text
Triage -> GoalCalibration -> ScopeLock -> RedReview -> BlueReview
-> JudgeDecision -> Execute -> Validate -> Audit -> Retest -> StateUpdate
```

Rules:

- `ScopeLock` limits the round to one attack surface.
- Red team finds risks; it does not fix or approve.
- Blue team verifies, refutes, ranks, and suggests minimal treatment.
- Judge decides `Allow`, `Reject`, `Defer`, or `NeedMoreEvidence` with allowed scope, forbidden scope, and required validation.
- Execution starts only after an `Allow`.
- Validation reports what passed, failed, was not verified, and what cannot be claimed.
- Audit checks boundary compliance, residual risk, and next action.

## Write Control

Default to main-thread-only final writes.

- `final/` or the main branch is single-writer by default.
- Background review roles only write their own `outbox`.
- Executors may write `candidates/`, `branches/`, or `patches/` only after judge approval.
- Candidate/branch merges require validation plus merge decision.
- Rule evolution roles may propose rules, never directly modify active rules.

Treat file writes, final quality claims, and rule changes as high-risk capabilities.

## Verification Integrity

Never let lower-level verification masquerade as higher-level proof.

- `L0`: static/structure checks.
- `L1`: build/format/rule checks.
- `L2`: runtime/use-path checks.
- `L3`: experience/goal-achievement checks.

Every validation report must separate:

- Verified.
- Failed.
- Not verified.
- Environment gaps.
- Cannot claim.

For skill artifacts, apply this additional checklist:

- `L0`: required files exist, frontmatter has `name` and `description`, referenced files exist, and no unresolved scaffold markers remain.
- `L1`: run the skill validation script when available; if dependency errors block it, record the blocker and perform the L0 checklist manually.
- `L2`: dry-run the skill against at least one realistic request or example. For true multi-thread requests, verify independent session ids, short names, project ownership, minimal input, and no expected-answer leakage.
- `L3`: do not claim real-world effectiveness until it has helped on an actual user task or an independent forward test.

## Run Workspace

For G2/G3/R1/R2 work or any true independent-session run, create a run workspace with:

```text
00_manifest/
01_task/
02_state/
  session_evidence.md
03_bus/
04_decisions/
05_artifacts/
06_validation/
07_audit/
08_locks/
09_handoff/
rules/
delivery/
```

Use a compressed version for G1 tasks. Generate `README_RUN.zh.md` when creating a run workspace so normal users know where final artifacts, session evidence, decisions, audit logs, safe feedback files, and handoff files live.

## Output Discipline

For user-facing replies, report the chosen G/W/R mode, enabled independent sessions or main-proxied role passes, minimum effective improvement, next loop step, and any validation limits. Keep the reply short unless the user asks for a full SOP.

For run files, be structured and explicit. Use templates from `references/templates.md`.

