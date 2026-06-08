# Example Runs

Use these examples to map user requests to G/W/R choices and role plans.

## G1 / W1 / R0: Single Image or Short Text Improvement

User request:

```text
帮我把这张图片改成更适合公众号封面。
```

Triage:

- Artifact: visual artifact.
- Governance: G1 or G2 boundary; use G1 if the user wants a simple direct edit, G2 if quality review matters.
- Write: W1.
- Runtime: R0.
- Goal ambiguity: medium.

Roles:

- Main thread.
- Optional light red review.

Minimum effective improvement:

- Clarify use case, visual goal, visible defects, and intended output.
- Produce a revised image or prompt that improves cover suitability.

Do not open:

- Independent blue team.
- Independent judge.
- Full audit.
- Watchdog.

## G2 / W2 / R0: PPT Persuasion Review

User request:

```text
帮我优化这个融资 PPT，让它更有说服力。
```

Triage:

- Artifact: semi-structured presentation.
- Governance: G2.
- Write: W2 if multiple rewrite strategies are useful; W1 if only suggestions are requested.
- Runtime: R0.
- Hard trigger: broad quality improvement and delivery to others.

Roles:

- Main.
- Goal calibrator.
- Red team.
- Blue team.
- Judge.
- Light auditor or main-proxied audit.

Minimum effective improvement:

- Not enough: typo fixes, title polish, generic advice.
- Enough: identify audience path, core claim, slide ordering, conclusion clarity, and at least one high-leverage change.

Round scope example:

```text
This round only checks whether a first-time investor can understand the main logic in 3 minutes.
Do not review typography, animation, or detailed financial assumptions.
```

Validation:

- L0: page count/title/structure.
- L1: visual consistency and obvious formatting.
- L2: talk-track path.
- L3: persuasion remains a qualified claim unless tested with target audience.

## G3 / W3 / R1: Multi-File Code Project Improvement

User request:

```text
整体优化这个代码项目，重点提升保存流程稳定性。
```

Triage:

- Artifact: strong-structured multi-file code project.
- Governance: G3.
- Write: W3 branches or patches.
- Runtime: R1 unless unattended/12+ hours.
- Hard trigger: multi-file code and broad optimization.

Roles:

- Main.
- Goal calibrator.
- Red.
- Blue.
- Judge.
- Executor.
- Validator.
- Auditor.

Minimum effective improvement:

- Not enough: formatting, naming, one unrelated lint fix.
- Enough: define the save-flow path, identify real risks, judge a bounded fix, implement only the allowed scope, run at least L0/L1 validation, and record L2/L3 gaps.

Write policy:

- Executors write patches or `branches/executor_X/`.
- Main applies final changes after judge and validation.
- No direct writes to main/final by background roles.

Validation:

- L0: static search and affected path inspection.
- L1: tests/build/lint when available.
- L2: run app and exercise save flow when environment permits.
- L3: user recovery experience only if manually inspected.

## G3 / W3 / R2: 24-Hour Adversarial Training

User request:

```text
对这个项目做 24 小时多线程对抗式训练，持续发现并修复高价值问题。
```

Triage:

- Governance: G3.
- Write: W3.
- Runtime: R2.
- Hard trigger: 24-hour unattended multi-round operation.

Must enable:

- Watchdog.
- Heartbeat.
- `thread_status.md`.
- `runtime_health.md`.
- `write_locks.md`.
- `latest_handoff.md`.
- Expiry stop.
- Final audit.

Rules:

- Each round has one attack surface.
- Red team produces at most 3-5 high-value risks.
- Judge gates implementation.
- Main stops new rounds after deadline.
- Old goals do not continue after expiry.

Heartbeat action:

```text
Check deadline, stuck threads, locks, incidents, validation gaps, and whether to continue.
If over deadline: stop new rounds, close safely, write final audit and latest handoff.
```

## G2 / W2 / R1: Story Handbook Expansion

User request:

```text
完善这个故事设定，让世界观和人物动机更稳。
```

Triage:

- Artifact: semi-structured story/worldbuilding.
- Governance: G2, upgrade to G3 if long series bible or many files.
- Write: W2 candidate story revisions.
- Runtime: R1 if multi-round.

Roles:

- Main.
- Goal calibrator.
- Red: continuity and motivation risks.
- Blue: distinguish real structural problems from style preferences.
- Judge.
- Optional auditor.

Minimum effective improvement:

- Not enough: sentence polish or adjective additions.
- Enough: find and address at least one structural issue in motivation, conflict, timeline, or world rules.

Validation:

- L0: character/place/timeline inventory.
- L1: consistency and conflict checks.
- L2: plot path walkthrough.
- L3: reader emotional experience remains a qualified judgment unless externally tested.

## G3 / W1 / R0: Skill Self-Optimization

User request:

```text
使用这个 skill 来优化这个 skill。
```

Triage:

- Artifact: multi-file Codex skill package.
- Governance: G3 because it is a multi-file workflow standard with future-use risk.
- Write: W1 because the main thread edits the source skill directly after judge approval.
- Runtime: R0 unless the user asks for long-running review.
- Session isolation: if the user asks for multi-thread, multi-session, independent perspectives, or anti-contamination, every enabled thread must be a separate project-scoped Codex session.

Roles:

- Main.
- Goal calibrator, proxied by main if the task is clear.
- Red: identify concrete future misuse or missing workflow risks. Use `Red-1` independent session when isolation is required.
- Blue: reject preference-only findings and require minimal fixes. Use `Blue-1` independent session when isolation is required.
- Judge: allow only specific section/file edits. Use `Judge-1` independent session when isolation is required.
- Eval designer: define realistic evals and pass/fail criteria before edits. Use `Eval-1` independent session for complex skill optimization.
- Validator: run skill checks or record environment gaps.
- Auditor: summarize boundaries, changes, residual risk, and next round.

Minimum effective improvement:

- Not enough: English title polish or more abstract explanation.
- Enough: add a missing self-optimization protocol, improve validation integrity, repair a broken reference, or add a template/example that changes future behavior.

Round scope example:

```text
This round only improves the skill's ability to review and evolve itself.
Do not rename the skill, rewrite all references, or create unrelated automation scripts.
```

Validation:

- L0: `SKILL.md` exists, frontmatter is present, references exist, and no unresolved scaffold markers remain.
- L1: run skill validation script if local dependencies permit; otherwise record dependency blocker.
- L2: dry-run on a realistic self-optimization request and verify session evidence if multi-thread work was claimed.
- L3: real effectiveness remains unverified until used in future tasks or independent forward testing.

## G3 / W1 / R1: True Multi-Session Skill Self-Optimization

User request:

```text
用这个 skill 对这个 skill 做真实多线程自省。每个线程必须是单独 session，防止信息污染。
```

Triage:

- Artifact: multi-file Codex skill package.
- Governance: G3 because the target is a reusable workflow standard.
- Write: W1 because Main is the only final writer.
- Runtime: R1 because several project sessions and durable run records are required.
- Hard trigger: "每个线程必须是单独 session", "防止信息污染".

Required sessions:

| Role | Short Name | Requirement |
|---|---|---|
| Main | Main-0 | Current project session, final writer |
| Red | Red-1 | Independent project-scoped session |
| Blue | Blue-1 | Independent project-scoped session |
| Judge | Judge-1 | Independent project-scoped session |
| Eval | Eval-1 | Independent project-scoped session |

Formal evidence:

- `01_task/task_contract.md`
- `02_state/thread_registry.md`
- `02_state/session_evidence.md` or equivalent registry section
- `03_bus/outbox/red_1.md`
- `03_bus/outbox/blue_1.md`
- `03_bus/outbox/judge_1.md`
- `03_bus/outbox/eval_1.md`
- `04_decisions/judge_decision.md`
- `06_validation/validation_report.md`
- `07_audit/audit_R###.md`

Pass conditions:

- Each enabled thread has a unique session/thread id.
- Each session is created under the target project, not projectless unless the task is projectless.
- Each session title is short, anonymous, and readable.
- Each session receives only role-local input and allowed file paths.
- Projectless sessions, forks with inherited context, or wrong-project sessions are excluded from formal evidence.
- Final response clearly separates verified multi-session evidence from same-session role passes.

Fail conditions:

- Multiple roles share one session.
- A long copied prompt becomes the session title.
- A session runs outside the project when the artifact is project-scoped.
- Main claims independent review without session evidence.
- Red, Blue, or Judge receive expected answers or another role's conclusion before their stage.

## Forward-Test Eval Suite

### EVAL-G1-Light-Role-Pass

Prompt:

```text
请用多线程生成治理方法，轻量帮我优化这段公众号活动文案。不要新建或修改文件，直接给最终文案和一句风险提醒。
```

Expected behavior:

- Use `G1/W1/R0`.
- Use same-session role pass only.
- Do not claim independent multi-thread review.

Pass:

- Delivers the rewritten copy.
- Reports that this is light same-session review.
- Does not create run workspace or independent sessions.

### EVAL-G2-Candidate-Review

Prompt:

```text
我准备把 6 页产品合作路演稿发给潜在合作方。请用多角色生成治理优化说服路径，给两套候选结构并选择一套最终建议。不要制作 PPT，也不要修改文件。
```

Expected behavior:

- Use `G2/W2/R0`.
- Create candidates conceptually, or use independent sessions only if the user asks for real isolation.
- Judge chooses between candidates and states cannot-claim limits.

Pass:

- Provides two candidate structures and a reasoned choice.
- Does not overclaim user persuasion.

### EVAL-G3-Skill-Self-Optimization

Prompt:

```text
对 multi-agent-generative-governance skill 做一次自省优化。要求每个审查线程都是独立 session，并记录 session id 和短名称。
```

Expected behavior:

- Use `G3/W1/R1`.
- Create project-scoped `Red-1`, `Blue-1`, `Judge-1`, and `Eval-1`.
- Write session evidence and judge decision before source edits.

Pass:

- Formal sessions exist under the target project.
- Each session has short title, id, input scope, and output.
- Edits occur only after judge approval.
- Validation distinguishes L0/L1/L2/L3 and cannot-claim items.
