# MTGG Runtime Optimization Log

Date: 2026-06-11

## Summary

This update turns MTGG from a process-heavy multi-session workflow into a more explicit governance runtime. The core change is that MTGG now supports two operating environments inside one skill:

- `Reuse-Fast`: reuse an existing MTGG team for repeated, related, or lightweight work.
- `Full-Governance`: run strict independent-session governance for high-risk, auditable, anti-contamination work.

This remains one MTGG skill. The two environments are runtime profiles inside the same skill.

## Why This Was Needed

Real MTGG usage exposed several problems:

- Repeated MTGG requests created new role sessions instead of reusing existing teams.
- Old Red/Blue/Judge/Validator/Auditor sessions were left unmanaged.
- Interleaving normal main-thread chat between MTGG rounds made continuation ambiguous.
- Creating or deleting sessions risked context loss.
- Session naming, evidence, and behavior records were inconsistent.
- The original workflow was quality-oriented but too expensive for lightweight repeated use.

## What Changed

### 1. Two Operating Environments

MTGG now distinguishes between:

- `Reuse-Fast` for repeated, related, or lightweight tasks.
- `Full-Governance` for strict independent governance.

The intent is to avoid over-opening sessions while preserving full governance when the task requires it.

### 2. Session Registry And Team Pool

MTGG now requires a registry before creating new independent sessions.

The registry tracks:

- team id
- role
- thread id
- title
- project path
- scope tags
- status
- lease owner and expiry
- last input and output pointers
- handoff capsule pointer
- contamination notes
- reuse eligibility

### 3. Reuse-First Policy

New MTGG rounds must first check whether existing role sessions can be reused.

New sessions are allowed only when reuse is unsafe or unavailable, such as:

- wrong project
- stale or expired role
- missing handoff
- contamination risk
- active lease conflict
- user explicitly requests a fresh team

### 4. Handoff Capsules

MTGG now handles context continuity through handoff capsules instead of relying on raw chat memory.

A capsule records durable role-local state:

- objective and scope
- allowed and forbidden inputs
- durable findings and decisions
- validation state
- unresolved risks
- output pointers
- contamination notes
- cannot-claim limits
- next action

This protects continuity when sessions are reused, replaced, retired, or resumed after unrelated chat.

### 5. Session Lifecycle Rules

Sessions now have lifecycle states:

- `idle`
- `assigned`
- `waiting`
- `blocked`
- `expired`
- `retired`

MTGG now prefers retirement over deletion. A session should not be deleted or archived until useful context has been merged, rejected, or captured in a handoff capsule.

### 6. Immediate Naming Gate

New sessions must be renamed before substantive delegation.

Recommended stable names include:

- `红队-A`
- `蓝队-A`
- `裁判-A`
- `验证-A`
- `审计-A`
- `监测-A`

If naming is missed, it must be recorded as an incident and remediated.

### 7. Unified Behavior Recording

MTGG now explicitly supports a single unified run record when human readability matters.

The record should include:

- registry lookup
- reuse decision
- thread creation
- naming
- lease assignment
- prompts
- reads and writes
- decisions
- validation
- audit
- incidents and remediation

### 8. Skill Structure Cleanup

The main `SKILL.md` was reduced to a concise high-signal entry file. Detailed rules remain in references:

- `references/process-standard.md`
- `references/templates.md`
- `references/example-runs.md`

This follows the skill-creator principle that `SKILL.md` should be an operational guide, not a large manual.

## Files Updated

- `multi-thread-generative-governance/SKILL.md`
- `multi-thread-generative-governance/references/process-standard.md`
- `multi-thread-generative-governance/references/templates.md`
- `multi-thread-generative-governance/references/example-runs.md`
- `multi-thread-generative-governance/agents/openai.yaml`

## Validation

Completed:

- Confirmed official skill name remains `multi-thread-generative-governance`.
- Confirmed no candidate-skill naming remains in the promoted skill.
- Confirmed key runtime concepts exist in the skill files:
  - `Reuse-Fast`
  - `Full-Governance`
  - `Session Registry`
  - `Handoff Capsules`
  - `Reuse Decision`
  - behavior recording
- Confirmed a backup of the pre-optimization MTGG was created locally.

Not yet completed:

- Fresh-session trigger test.
- Repeated MTGG benchmark using an existing team.
- Full governance benchmark with strict anti-contamination.
- Empirical speedup measurement.
- Empirical no-quality-loss validation.

## Expected Impact

Speed:

- Fewer unnecessary new sessions.
- Lower startup overhead for repeated MTGG work.
- Less duplicate role output.
- Better early-stop and reuse behavior.

Quality:

- More explicit session lifecycle management.
- Better continuity through handoff capsules.
- Lower risk of context loss when replacing sessions.
- Stronger auditability through registry and behavior records.

User experience:

- Less sidebar/session clutter.
- Clearer reporting of which sessions were reused or newly created.
- Easier understanding of whether a run is lightweight reuse or full governance.

## Remaining Risks

- The registry is currently procedural, not enforced by a deterministic runtime.
- Handoff capsule quality depends on the main thread creating good summaries.
- If a future run skips registry lookup, duplicate session sprawl can still occur.
- If too much context is put into a handoff capsule, anti-contamination can weaken.
- If too little context is put into a handoff capsule, continuity can fail.

## Next Steps

1. Run a repeated-round benchmark:
   - Round 1: create MTGG team.
   - Normal chat interruption.
   - Round 2: request another MTGG round.
   - Verify reuse instead of duplicate creation.

2. Run a full-governance benchmark:
   - Force independent Red/Blue/Judge/Validator/Auditor roles.
   - Verify registry, naming, handoff, and audit records.

3. Add deterministic helper scripts later if needed:
   - registry validator
   - handoff capsule checker
   - session reuse decision checker
