# Process Standard

This reference contains the detailed operating standard for the multi-thread generative governance skill. Load it when you need exact mode rules, permissions, state transitions, verification standards, audit scoring, rule evolution, or long-running safeguards.

## Table of Contents

1. System Definition
2. Mode Selection
3. Role Model
4. Run Workspace
5. Permissions
6. Round State Machine
7. Verification
8. Audit and Scoring
9. Rule Evolution
10. Candidate, Branch, and Git Handling
11. Long-Running Safeguards
12. Skill Self-Optimization

## 1. System Definition

The system is a multi-role quality governance process for complex generation tasks. It serves artifacts that can be generated, reviewed, modified, verified, and archived: code, documents, PPTs, images, stories, product plans, study materials, and process designs.

The first value of this system is cognitive role separation, but a unit called a `thread` must be backed by an independent Codex session. Same-session role work is a `role pass`, not a thread. Do not claim multi-thread, independent review, or anti-contamination unless session evidence exists.

Core goals:

- Improve artifact quality.
- Expose real risks before delivery.
- Reduce self-confirmation bias by separating proposer, attacker, defender, judge, executor, validator, and auditor.
- Keep changes traceable and recoverable.
- Preserve validation integrity.
- Support rule resourceization and evidence-triggered rule evolution.
- Support long-running work through heartbeat, handoff, and takeover.

Non-goals:

- Do not seek one-shot perfection.
- Do not open every possible role by default.
- Do not optimize every dimension in one round.
- Do not let background roles bypass the judge.
- Do not treat model confidence as evidence.
- Do not treat a complete process as proof of a good result.

Key terms:

- `Role`: a responsibility such as red, blue, judge, validator, or auditor.
- `Role pass`: same-session work performed by Main under a role label. It is useful for G1/light G2 work, but it is not independent.
- `Thread`: a delegated role backed by its own independent Codex session.
- `Session`: the actual Codex thread/session with its own context, title, id, project path, input package, and output.

## 2. Mode Selection

Select three independent modes.

### Governance Strength

`G1` light generation:

- Single image edit, short copy, single page, simple conversion, small explicit file task.
- Main thread performs most duties.
- Optional light red review.

`G2` standard governance:

- PPT, multi-page document, story handbook, product proposal, course material, complex but bounded content.
- Main + red + blue + judge.
- Add goal calibration, validation, or light audit when broad or important.

`G3` complex project:

- Code project, multi-file package, large document system, long story universe, complex product plan, multi-round project.
- Main + goal calibrator + red + blue + judge + executor + validator + auditor.
- Add rule evolver, merge judge, or specialist teams as needed.

### Write Mode

`W1` single writer:

- Main writes final.
- No independent executor unless explicitly needed.

`W2` candidate artifacts:

- Executors write separate `candidates/executor_X/`.
- Main or merge judge selects and merges into final.

`W3` branch or patch mode:

- Executors write separate branches, workspaces, or patches.
- Merge requires validation, merge decision, and audit.

### Runtime Safeguard

`R0` short task:

- Minimal state and final report.

`R1` medium/long task:

- Use `thread_status.md`, `round_log.md`, and `latest_handoff.md`.

`R2` long-running/unattended:

- Must use watchdog, heartbeat, write locks, active tasks, runtime health, latest handoff, expiry stop, and takeover.

### Scoring

Score each 0-3:

| Dimension | Meaning |
|---|---|
| A | Artifact complexity |
| S | Scope size |
| G | Goal ambiguity |
| R | Error/risk impact |
| V | Verification difficulty |
| W | Write complexity |
| D | Duration |

Governance score = A + S + G + R + V:

- 0-4: G1
- 5-8: G2
- 9+: G3

Write:

- W 0-1: W1
- W 2: W2
- W 3: W3

Runtime:

- D 0: R0
- D 1-2: R1
- D 3: R2

Hard triggers override scores.

Upgrade to G2 when:

- Output exceeds one page/paragraph/image.
- User asks for review, optimization, or quality improvement.
- Output will be delivered to others.
- Red-team findings are requested.

Upgrade to G3 when:

- Multi-file code or project.
- Whole-project optimization.
- Sustained adversarial generation.
- Multiple executor candidates.
- High refactor/rework risk.
- Runtime/build/experience validation needed.
- The user asks for true independent sessions or information-contamination resistance.
- Goal likely to be reduced to a shallow fix.

Upgrade to R2 when:

- 12+ hours, 24-hour training, unattended operation, multi-round automation, or local device continuity matters.

Independent session hard triggers:

- User says multi-thread, multi-meeting, multi-session, independent perspective, isolated review, anti-contamination, or equivalent terms.
- User asks red/blue/judge sessions not to see each other's reasoning.
- The task relies on independent candidate generation or independent review evidence.

When these triggers fire, each enabled non-main thread must be created as a separate project-scoped Codex session. If that is impossible, disclose the downgrade or block the multi-thread claim.

Always define Minimum Effective Improvement:

- What counts as a real improvement?
- What would be a shallow non-solution?

## 3. Role Model

A role is not automatically a thread. A role becomes a thread only when it has a separate Codex session and recorded session evidence. Otherwise, it is a main-proxied role pass.

Use role passes for light work. Use independent sessions when the user requests independence, anti-contamination, or when the selected G/W/R mode depends on independent evidence.

| Role | Writes | Does | Must Not Do |
|---|---|---|---|
| Main | state, inbox, final, locks, handoff | orchestrate, execute allowed final changes, merge, close | fabricate validation, expand scope silently |
| Goal calibrator | own outbox, `goal_calibration.md` | define literal/deeper goals, forbidden expansions, minimum improvement | execute or judge |
| Red team | own outbox | find risks with trigger, impact, evidence, minimal validation | fix, approve, demand implementation |
| Blue team | own outbox | verify/refute red findings, rank severity, propose minimal treatment | execute or approve |
| Judge | `judge_decision.md`, own outbox | decide Allow/Reject/Defer/NeedMoreEvidence | implement or validate |
| Executor | candidates/branches/patches after approval | generate allowed changes | write final by default, exceed boundaries |
| Validator | `validation_report.md`, own outbox | verify and report gaps | fix or overclaim |
| Auditor | audit files, own outbox | boundary check, residual risks, scores, next steps | approve merge or modify artifact |
| Rule evolver | rule proposals | propose evidence-backed rule changes | modify active rules |
| Watchdog | runtime health, own outbox | monitor deadlines, locks, thread health, workspace writability | judge content quality |
| Merge judge | `merge_decision.md` | decide candidate/branch merge | perform implementation |

Conclusion permissions matter:

- Red may say "risk found"; not "must fix."
- Blue may say "成立/部分成立/不成立"; not "main may directly modify."
- Judge may authorize or reject; not claim implementation or validation success.
- Executor may say "candidate produced"; not "final quality passed."
- Validator may say "verified/failed/not verified"; not "project is fully optimized."
- Auditor may say "process compliant/non-compliant"; not "merge approved."

Session permissions matter:

- Each independent session receives only its allowed input package.
- Session titles must be short, anonymous, readable, and written in the user's language when practical.
- Red must not read Blue/Judge/Executor outputs before submitting its own report.
- Blue may read Red findings only when its job is to verify/refute them.
- Judge may read source materials plus Red/Blue outputs, but not uncited private reasoning.
- No session may claim another session's work.
- Same-session role passes must be labeled as simulated or main-proxied.

## 4. Run Workspace

Full structure:

```text
runs/run_0001/
  README_RUN.zh.md
  00_manifest/
    run_manifest.md
    permissions.md
  01_task/
    task_contract.md
    task_brief.md
    triage.md
    run_profile.md
    thread_plan.md
    goal_calibration.md
    round_scope.md
    user_feedback.md
    user_override.md
  02_state/
    current_state.md
    round_state.md
    thread_status.md
    session_evidence.md
    runtime_health.md
  03_bus/
    inbox/
    outbox/
  04_decisions/
    judge_decision.md
    merge_decision.md
    rule_decision.md
  05_artifacts/
    source/
    candidates/
    branches/
    patches/
    diffs/
    final/
  06_validation/
    validation_report.md
    validation_queue.md
  07_audit/
    audit_log.md
    audit_R001.md
    round_log.md
    round_score.md
    final_audit.md
  08_locks/
    write_locks.md
    active_tasks.md
    permission_incidents.md
  09_handoff/
    latest_handoff.md
    takeover_notes.md
  rules/
    constitution.md
    rule_registry.md
    rule_changelog.md
    rule_evolution_queue.md
    proposals/
  delivery/
    final_artifact/
    final_report.md
    validation_summary.md
    audit_summary.md
    reproduction_notes.md
```

`session_evidence.md` is required for every true multi-thread run. It must record role, short title, session/thread id, source thread id when available, project path, input summary, forbidden inputs, permissions, output path, status, and contamination notes.

`thread_plan.md` must separate:

- Enabled independent sessions.
- Main-proxied role passes.
- Roles intentionally not activated.

Use Markdown files with YAML frontmatter for formal run documents.

Each file should include enough identity metadata to recover context: schema, run_id, round_id, role, status, version, input refs, output refs.

## 5. Permissions

Three permission types:

- File permission: read/write paths.
- Behavior permission: approve, merge, close, rollback, takeover, modify rules.
- Stage permission: what is allowed in the current state.

Permission levels:

| Level | Name | Meaning |
|---|---|---|
| P0 | Read | read only |
| P1 | Comment | write non-binding suggestions |
| P2 | WriteOwnOutbox | write own outbox |
| P3 | AppendLog | append logs |
| P4 | WriteCandidate | write candidate artifacts |
| P5 | WriteBranch | write own branch/workspace |
| P6 | WriteSharedState | write shared state |
| P7 | ApproveDecision | write formal decisions |
| P8 | WriteFinal | write final artifact |
| P9 | ModifyRules | change active rules |

Core rules:

1. Shared fact files have one writer.
2. Each role writes only its own outbox.
3. Review roles do not write artifacts.
4. Judge does not implement.
5. Executor does not judge.
6. Validator does not fix.
7. Auditor does not modify artifacts.
8. Rule evolver does not modify active rules.
9. Final is main-thread-only by default.
10. Parallel writing happens only in candidates or branches.
11. Incidents are recorded in `permission_incidents.md`.
12. Users change goals through `user_override.md`, not state files.

Incident types:

- File overreach.
- Stage overreach.
- Scope overreach.
- Rule overreach.
- Conclusion overreach.

## 6. Round State Machine

Standard loop:

```text
Triage -> GoalCalibration -> ScopeLock -> RedReview -> BlueReview
-> JudgeDecision -> Execute -> Validate -> Audit -> Retest -> StateUpdate
```

State machine:

```text
INIT
  -> TRIAGE
  -> GOAL_CALIBRATION
  -> SCOPE_LOCK
  -> RED_REVIEW
  -> BLUE_REVIEW
  -> JUDGE_DECISION
      REJECT -> BACKLOG / CLOSE
      DEFER -> VALIDATION_QUEUE / BACKLOG
      NEED_MORE_EVIDENCE -> RED_REVIEW / VALIDATE
      ALLOW -> EXECUTE -> VALIDATE -> AUDIT -> RETEST
          PASS -> STATE_UPDATE -> NEXT_ROUND / CLOSE
          FAIL -> BLUE_REVIEW / JUDGE_DECISION
```

Judge decisions:

- `Allow`
- `Reject`
- `Defer`
- `NeedMoreEvidence`

Judge decisions must include:

- Allowed scope.
- Forbidden scope.
- Required validation.
- Evidence basis.
- Whether execution may begin.

Reject vague approvals such as "适当优化", "自行调整", or "视情况处理."

## 7. Verification

Levels:

- L0 static/structure: file existence, headings, symbols, config, page count.
- L1 build/format/rule: compile, tests, lint, format, document/PDF/PPT/image rule checks.
- L2 runtime/use-path: app launch, API call, user path, narrative path, presentation walkthrough.
- L3 experience/goal-achievement: user understanding, persuasion, visual fit, story tension, product clarity.

Validation reports must distinguish:

- Verified.
- Failed.
- Not verified.
- Evidence.
- Environment gaps.
- Cannot claim.

Artifact-specific emphasis:

- Code: L0 static, L1 build/tests/lint, L2 launch/API/key path, L3 real user path/performance/recovery.
- PPT: L0 page/title/spelling, L1 formatting/visual consistency, L2 talk-track path, L3 audience persuasion.
- Image: L0 size/format/subject, L1 style/composition/readability, L2 usage context simulation, L3 audience fit.
- Document/PDF: L0 sections/titles/references, L1 terminology/layout, L2 reader path, L3 communication goal.
- Story: L0 characters/places/timeline, L1 continuity/conflict/foreshadowing, L2 plot path, L3 reader emotion/rhythm.

## 8. Audit and Scoring

Audit types:

- Process audit: did the loop run correctly?
- Boundary audit: did execution obey judge scope?
- Result audit: did the artifact improve and what remains?

Round scoring:

| Dimension | 0 | 1 | 2 |
|---|---|---|---|
| Problem authenticity | vague | partial evidence | location, trigger, impact |
| Blue review | absent | assertion | validity and minimal plan |
| Judge boundary | none | vague | allowed/forbidden/validation clear |
| Change control | uncontrolled | related | minimal and bounded |
| Validation | none | static only | layered and explicit |
| Audit | none | summary | traceable to decision |
| Retest | none | formal | checks original and new risk |

Interpretation:

- 0-5 invalid round.
- 6-9 low-quality round.
- 10-12 acceptable round.
- 13-14 high-quality round.

Use two score families:

- Artifact quality score.
- Process governance score.

## 9. Rule Evolution

Rule files:

```text
rules/
  constitution.md
  rule_registry.md
  rule_changelog.md
  rule_evolution_queue.md
  proposals/
  decisions/
```

Rule layers:

- L0 constitution.
- L1 system rules.
- L2 role rules.
- L3 file permission rules.
- L4 domain adaptation rules.
- L5 temporary run rules.

Lifecycle:

```text
Draft -> Candidate -> Trial -> Active -> Deprecated / Rejected / Superseded
```

Trigger rule evolution only from evidence:

- Low governance scores across rounds.
- Overreach incidents.
- Vague judge boundaries.
- Red-team noise.
- Blue-team misses.
- Repeated goal underscoping.
- Repeated validation gaps.
- Repeated watchdog failures.
- Repeated user corrections.
- Bloated backlog without priority.

Flow:

```text
Audit evidence -> rule_evolution_queue -> rule proposal
-> rule judge -> main updates registry -> Trial
-> later audit -> Active / Revise / Reject
```

## 10. Candidate, Branch, and Git Handling

W2 merge flow:

```text
Executors submit candidates
-> validator checks candidates
-> blue/merge review compares
-> merge judge writes merge_decision.md
-> main merges to final
-> audit records
```

W3 Git principles:

1. `main` represents stable artifact.
2. AI executors write only `ai/*` branches.
3. Do not push directly to `main`.
4. Merges require merge decision, validation report, and audit log.
5. Round commits may use names like `run_0001/R001/validate`.

## 11. Long-Running Safeguards

R2 requires:

- `thread_status.md`
- `runtime_health.md`
- `write_locks.md`
- `active_tasks.md`
- `latest_handoff.md`
- `round_log.md`
- `final_audit.md`

Watchdog checks:

- Device awake.
- Network.
- Workspace writable.
- Disk space.
- Thread status.
- Lock expiry.
- Heartbeat freshness.
- Round timeout.
- Global deadline.

Heartbeat must check:

1. Deadline.
2. Stuck threads.
3. Unreleased locks.
4. Unresolved incidents.
5. Whether to stop new rounds.

On expiry:

1. Stop new rounds.
2. Stop new modifications.
3. Safely close current work.
4. Write final audit.
5. Write latest handoff.
6. Mark run CLOSED.

Recovery order:

1. Read `README_RUN.zh.md`.
2. Read `current_state.md`.
3. Read `latest_handoff.md`.
4. Read `thread_status.md`.
5. Check `write_locks.md`.
6. Check latest round log.
7. Decide continue, rollback, takeover, or close.

## 12. Skill Self-Optimization

Use this protocol when the target artifact is this skill or another Codex skill.

Default triage:

- Artifact: strong/semi-structured multi-file skill package.
- Governance: `G3`.
- Write mode: `W1` unless explicitly comparing candidate rewrites; use `W2/W3` when candidates, patches, or branches are needed.
- Runtime: `R0` unless the user requests long-running review.
- Session isolation: independent sessions are required when the user asks for multi-thread, multi-session, independent perspectives, anti-contamination, or externalized red/blue/judge review.

Minimum effective improvement:

- Not enough: wording polish, renaming headings, or adding more abstract principles.
- Enough: reduce a concrete future misuse risk, improve trigger accuracy, clarify a workflow decision, add a missing validation step, repair a broken reference, or add a reusable template/example that changes how the skill performs.

Recommended attack surfaces:

1. Trigger accuracy: Will the skill trigger for intended requests and avoid adjacent misuse?
2. First move: Does it force triage before thread proliferation?
3. Session isolation: Do activated threads have separate sessions, short names, project ownership, minimal input, and no expected-answer leakage?
4. Role workflow: Can Codex execute red/blue/judge/audit without becoming theatrical?
5. Write control: Does it prevent background roles from writing final artifacts?
6. Validation integrity: Does it distinguish L0/L1/L2/L3 and record validation blockers?
7. Progressive disclosure: Is `SKILL.md` concise, with details in references?
8. Template coverage: Are the artifacts needed by a real run available?
9. Example coverage: Can a future Codex map common user requests to G/W/R choices?
10. Installation and sync: If a skill is installed separately from the source copy, are both updated or is the difference disclosed?

Self-review loop:

```text
TaskContract -> Triage -> EvalContract -> ScopeLock -> RedReview -> BlueReview
-> JudgeDecision -> Edit -> Validate -> ForwardTest/Audit -> NextRound/Close
```

Constraints:

- Keep the round scoped to one to three high-value changes.
- Prefer adding a missing operational instruction over expanding theory.
- Do not create an infinite self-improvement loop.
- Do not claim L1 validation if the validation script cannot run.
- If validation tooling fails due to local dependency issues, mark it as an environment gap and run the manual checklist.
- Before editing, define realistic eval prompts, expected behavior, pass/fail criteria, observable evidence, and baseline or old-skill comparison when practical.
- When forward-testing with independent sessions, pass raw artifacts and the user-like task. Do not pass expected answers, suspected bugs, intended fixes, or private main-thread conclusions unless the test explicitly requires them.
- Record whether each forward-test used a true independent session or a same-session role pass.

Eval contract fields:

- eval id
- realistic user prompt
- target artifact or input files
- expected trigger or mode
- pass criteria
- fail criteria
- observable evidence
- no-leak session prompt
- baseline or previous-iteration comparison
- artifacts captured
- result

Skill validation checklist:

- Required `SKILL.md` exists.
- YAML frontmatter contains only required triggering metadata unless the local skill format requires otherwise.
- `name` matches the folder name.
- `description` includes what the skill does and when to use it.
- `SKILL.md` references only existing bundled resources.
- No unresolved scaffold markers remain.
- `agents/openai.yaml`, if present, has a default prompt mentioning `$skill-name`.
- References are one level deep from `SKILL.md`.
- Long references include a table of contents or clear navigation.
- Self-optimization runs include an eval contract or explain why evals were not run.
- True multi-thread self-optimization includes `session_evidence.md` and formal outboxes for each independent session.
- Installed copy is synchronized when the user expects the skill to be available in future sessions.
