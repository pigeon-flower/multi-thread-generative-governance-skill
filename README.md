# 多智能体生成治理 Skill

![多智能体生成治理 Skill](assets/hero-zh.svg)

**MAGG（Multi-Agent Generative Governance，多智能体生成治理）** 是一个面向 Codex 的 Skill，用来把复杂 AI 生成任务变成一套**可分工、可验证、可审计、可交接**的治理流程。

它不是“多开几个聊天窗口”。它解决的是：当 AI 很容易自我确认、任务范围很大、结果需要交付给别人、或者你明确要求多线程/多角色独立审查时，如何让生成过程有规则、有证据、有边界。

更重要的是：**MAGG 的核心价值是用独立线程和治理记录，替代一部分原本需要人类持续盯着、反复审核、不断接管的监督工作。**
当任务需要跑很久、跨多轮、跨多个候选版本，或者人不能一直守在旁边时，MAGG 通过红队、蓝队、裁判、验证、审计、watchdog、handoff、锁和状态文件，让 AI 在离开人类实时监管的情况下，仍然能持续自检、控制写入、记录证据，并在需要时把状态交还给人。

> 仓库：`multi-agent-generative-governance-skill`  
> 一句话介绍：可审计多智能体生成治理 Codex Skill：用独立线程替代人工持续审核，支持长时间无人值守、验证证据、受控写入与 AI 自我改进。

## 核心优势：用线程替代人工持续监督

普通 AI 工作流的问题是：人一离开，AI 很容易继续沿着错误方向生成，或者生成完却没有可靠证据说明它真的检查过自己。MAGG 的设计目标不是让 AI “更会说”，而是让 AI 在长时间任务中拥有类似人工项目监管的结构。

```mermaid
flowchart LR
    Human["人类监督者"] -->|设定目标/边界| Contract["任务契约"]
    Contract --> Main["主控线程"]

    subgraph Agents["替代人工审核的线程网络"]
        Red["红队线程<br/>找风险"]
        Blue["蓝队线程<br/>过滤/反驳"]
        Judge["裁判线程<br/>批准/拒绝"]
        Val["验证线程<br/>检查证据"]
        Audit["审计线程<br/>记录边界"]
        Watch["监控线程<br/>长时间盯守"]
    end

    Main --> Red --> Blue --> Judge
    Judge -->|允许后| Main
    Main --> Val --> Audit
    Watch --> Main
    Audit --> Handoff["handoff<br/>把状态交还给人"]
    Handoff --> Human
```

MAGG 对人类监督的替代不是“完全不用人”，而是把人类从每一步都盯着，转变成：

- 人负责设定目标、边界和最终取舍。
- 线程负责持续审查、验证、记录和报警。
- 裁判负责阻止未经允许的写入。
- watchdog 和 handoff 负责长时间任务的状态延续。
- 验证和审计负责告诉人：哪些是真的完成，哪些不能宣称。

## 什么时候该用 MAGG

适合使用 MAGG 的任务，通常有一个共同点：**单次生成很容易看起来完成了，但实际质量、边界或验证不可靠。**

| 任务情形 | 为什么适合用 MAGG | 推荐强度 |
|---|---|---|
| 长时间任务、无人值守任务、24 小时/多轮迭代 | 核心场景。需要线程代替人工持续审核，使用心跳、handoff、锁、状态记录和接管机制 | R2 |
| 优化一个 Skill、SOP、提示词体系或工作流 | 容易只改措辞，不解决触发、边界、验证和真实使用问题 | G2/G3 |
| 复杂代码项目、跨文件重构、架构设计 | 需要红队找风险、裁判控范围、验证区分构建通过和真实可用 | G3 |
| PPT、报告、教材、产品方案、故事设定等多章节产物 | 需要目标校准、结构审查、内容一致性和交付审计 | G2 |
| 用户明确要求“多线程”“多 session”“独立视角”“防信息污染” | 必须用独立 Codex session 记录证据，不能用同一会话角色扮演糊弄 | G3 |
| 需要比较多个候选版本 | 需要候选产物、评审标准、合并裁判和验证记录 | W2/W3 |

不适合使用 MAGG 的任务：

- 简单问答、翻译一句话、改一个很小的格式问题。
- 用户只想要快速草稿，不需要审查和验证。
- 没有真实风险，却为了“看起来高级”强行开很多角色。
- 不能创建独立 session，却仍然想宣称“真实多线程独立审查”。

## 你应该怎么使用

安装后，在 Codex 里直接点名这个 Skill：

```text
使用 $multi-agent-generative-governance 审查并优化这个 Skill。重点检查触发条件、真实多线程边界、验证完整性和交付说明。
```

如果你要真实多线程，需要明确说出来：

```text
使用 $multi-agent-generative-governance 做一次真实多线程审查。红队、蓝队、裁判、验证必须是独立 session，并记录 session id、短名称、输入范围和输出位置。
```

如果你只是要轻量审查，也可以这样说：

```text
使用 $multi-agent-generative-governance 做一次轻量红队审查，不需要独立 session，只要指出主要风险和最小修复建议。
```

MAGG 每次启动后，理想情况下会先给出这些东西：

- 任务契约：目标、范围、禁止范围、验证方式、最低有效改进。
- 模式选择：G1/G2/G3、W1/W2/W3、R0/R1/R2。
- 角色计划：哪些角色真的需要启用，哪些只是同会话 role pass。
- 验证边界：能验证什么，不能宣称什么。

## 一眼判断：该开什么模式

```mermaid
flowchart TD
    A["用户任务"] --> B{"只是小改动或明确单步任务？"}
    B -->|是| G1["G1 / W1 / R0<br/>主会话处理<br/>可加轻量红队 role pass"]
    B -->|否| C{"是否多章节、多文件、要交付、要优化质量？"}
    C -->|是| G2["G2<br/>任务契约 + 红队 + 蓝队 + 裁判 + 验证"]
    C -->|否| G1
    C --> D{"是否复杂项目、真实多线程、候选对比或高风险？"}
    D -->|是| G3["G3<br/>目标校准 + 独立角色 + 执行 + 验证 + 审计"]
    D -->|否| G2
    D --> E{"是否长时间运行或无人值守？"}
    E -->|是| R2["R2<br/>线程代替人工持续审核<br/>watchdog + heartbeat + locks + handoff"]
    E -->|否| R0["R0/R1<br/>按任务长度保留必要记录"]
```

## MAGG 的核心架构

MAGG 把一次复杂生成任务拆成四层：**治理层、执行层、证据层、长时间监管层**。前三层保证任务能被审查和验证，第四层保证任务在人离开后仍然能持续运行、留下状态、等待接管。

```mermaid
flowchart TB
    U["用户目标"] --> TC["任务契约<br/>Task Contract"]
    TC --> TRIAGE["模式选择<br/>G / W / R"]

    subgraph GOV["治理层：决定该做什么、谁能做、做到哪一步"]
        TRIAGE --> GC["目标校准"]
        GC --> SL["范围锁定"]
        SL --> J["裁判决策"]
    end

    subgraph ROLES["认知角色层：分离视角，减少自我确认"]
        RED["红队<br/>找失败模式"]
        BLUE["蓝队<br/>验证/反驳/排序"]
        EVAL["评测设计<br/>先定标准"]
        AUDIT_ROLE["审计<br/>查边界和证据"]
    end

    subgraph EXEC["执行层：只做被允许的写入"]
        EXE["执行者"]
        MERGE["合并/主写入"]
    end

    subgraph EVIDENCE["证据层：不能只靠感觉说完成"]
        VAL["验证报告"]
        SESSION["session evidence"]
        AUDIT["审计记录"]
        HANDOFF["handoff / 状态"]
    end

    subgraph RUNTIME["长时间监管层：替代人工持续盯守"]
        WATCHDOG["watchdog"]
        HEARTBEAT["heartbeat"]
        LOCKS["write locks"]
        TAKEOVER["takeover / 接管"]
    end

    SL --> RED --> BLUE --> J
    EVAL --> J
    J -->|Allow| EXE --> MERGE --> VAL --> AUDIT
    J -->|Reject / Defer| SL
    RED -.独立 session 时记录.-> SESSION
    BLUE -.独立 session 时记录.-> SESSION
    VAL --> HANDOFF
    AUDIT --> HANDOFF
    WATCHDOG --> HEARTBEAT --> HANDOFF
    LOCKS --> EXE
    HANDOFF --> TAKEOVER
```

## 标准治理闭环

![治理闭环](assets/governance-loop-zh.svg)

```mermaid
sequenceDiagram
    participant Main as 主控
    participant Red as 红队
    participant Blue as 蓝队
    participant Judge as 裁判
    participant Exec as 执行
    participant Val as 验证
    participant Audit as 审计

    Main->>Main: 写任务契约
    Main->>Main: 选择 G/W/R 模式
    Main->>Red: 给定攻击面和允许输入
    Red-->>Main: 风险与失败模式
    Main->>Blue: 验证、反驳、排序风险
    Blue-->>Main: 最小修复建议
    Main->>Judge: 提交红蓝结论
    Judge-->>Main: Allow / Reject / Defer / NeedMoreEvidence
    Judge->>Exec: 仅允许指定范围
    Exec-->>Val: 产物或变更
    Val-->>Audit: 验证通过、失败、未验证、不能宣称
    Audit-->>Main: 边界合规与剩余风险
```

## 真实多线程：不是同一个会话里扮演角色

![真实线程证据](assets/session-evidence-zh.svg)

MAGG 的一条硬规则：

> 只有拥有独立 Codex session 的角色，才能叫 thread。  
> 同一会话内的红队/蓝队/裁判只能叫 role pass。

```mermaid
flowchart LR
    A{"用户是否要求<br/>多线程 / 多 session / 独立视角 / 防污染？"}
    A -->|否| B["可以使用同会话 role pass<br/>必须明确说明不是独立线程"]
    A -->|是| C["必须创建独立 Codex session"]
    C --> D["短名称<br/>红队-1 / 蓝队-1 / 裁判-1"]
    C --> E["项目路径<br/>必须是目标项目"]
    C --> F["最小输入包<br/>不能泄漏预期答案"]
    C --> G["独立输出<br/>outbox / final response"]
    D --> H["session evidence"]
    E --> H
    F --> H
    G --> H
    H --> I{"证据完整？"}
    I -->|是| J["可以宣称真实多线程审查"]
    I -->|否| K["只能说是降级或阻塞"]
```

session evidence 至少要记录：

| 字段 | 说明 |
|---|---|
| Role | 红队、蓝队、裁判、验证、审计等 |
| Short title | 用户语言中的短名称，例如 `红队-1` |
| Session/thread id | 独立会话 id |
| Project path | 是否在正确项目下运行 |
| Input summary | 给了什么输入 |
| Forbidden inputs | 明确没有给什么，例如预期答案、其他角色结论 |
| Output pointer | 输出文件或回复位置 |
| Status | pending / active / done / excluded |

## 写入权限模型

MAGG 不允许后台角色随便改最终文件。写入默认由主控或被批准的执行者完成。

```mermaid
flowchart TD
    RED["红队"] -->|只能写 outbox| BUS["03_bus/outbox"]
    BLUE["蓝队"] -->|只能写 outbox| BUS
    JUDGE["裁判"] -->|写决策| DEC["04_decisions"]
    EXEC["执行者"] -->|被允许后| CAND["05_artifacts / candidates"]
    MAIN["主控"] -->|最终整合| FINAL["delivery / final files"]
    VAL["验证"] --> REPORT["06_validation"]
    AUDIT["审计"] --> AUD["07_audit"]

    JUDGE -->|Allow 指定范围| EXEC
    CAND -->|验证后| MAIN
    REPORT --> MAIN
    AUD --> MAIN
```

常见规则：

- 红队只找风险，不修复、不批准。
- 蓝队验证和排序，不直接改最终产物。
- 裁判决定允许范围和禁止范围。
- 执行者只做裁判允许的修改。
- 验证报告必须写清楚不能宣称什么。
- 审计检查有没有越界、有没有证据缺口。

## 验证分层：不要把 L0 当 L3

![验证分层](assets/validation-ladder-zh.svg)

```mermaid
flowchart LR
    L0["L0 结构检查<br/>文件存在、frontmatter、引用路径"] --> L1["L1 规则检查<br/>脚本、格式、静态规则"]
    L1 --> L2["L2 使用路径<br/>dry-run、真实路径、session evidence"]
    L2 --> L3["L3 目标达成<br/>真实用户任务或独立 forward test"]
```

| 等级 | 能证明什么 | 不能证明什么 |
|---|---|---|
| L0 | 文件结构、引用、元数据存在 | 不能证明 Skill 好用 |
| L1 | 校验脚本或规则通过 | 不能证明真实任务成功 |
| L2 | 至少跑过一次真实路径或 dry-run | 不能证明长期稳定 |
| L3 | 对真实目标或独立测试有效 | 仍需记录边界和样本限制 |

每份验证报告都应该分开写：

- 已验证
- 失败项
- 未验证
- 环境缺口
- 不能宣称

## Run Workspace 长什么样

复杂任务会生成或建议一个 run workspace，用来保存任务契约、角色输出、决策、验证和审计。

```text
run_xxxx/
├── 00_manifest/
├── 01_task/
│   ├── task_contract.md
│   └── triage.md
├── 02_state/
│   └── session_evidence.md
├── 03_bus/
│   └── outbox/
│       ├── red_1.md
│       ├── blue_1.md
│       └── judge_1.md
├── 04_decisions/
│   └── judge_decision.md
├── 05_artifacts/
├── 06_validation/
│   └── validation_report.md
├── 07_audit/
│   └── audit.md
├── 08_locks/
├── 09_handoff/
└── delivery/
```

对于长时间或无人值守任务，`08_locks/` 和 `09_handoff/` 不是装饰目录。它们承担的是原本需要人类项目管理员做的工作：

- `08_locks/`：防止多个执行线程同时写坏最终产物。
- `09_handoff/`：保存最新状态，让人或后续线程可以接管。
- heartbeat：说明任务还活着，不是静默卡死。
- watchdog：检查是否超时、卡住、越界或需要人工介入。
- expiry stop：到期必须停，不允许无限自我循环。

```mermaid
flowchart TB
    TASK["01_task<br/>任务契约/模式选择"] --> STATE["02_state<br/>session evidence"]
    STATE --> BUS["03_bus/outbox<br/>角色输出"]
    BUS --> DEC["04_decisions<br/>裁判决策"]
    DEC --> ART["05_artifacts<br/>候选或执行产物"]
    ART --> VAL["06_validation<br/>验证报告"]
    VAL --> AUD["07_audit<br/>审计记录"]
    AUD --> HAND["09_handoff<br/>交接和状态"]
    HAND --> DEL["delivery<br/>最终交付"]
```

## 长时间无人值守任务的运行方式

MAGG 在 R2 模式下，会把“人盯着 AI 干活”的过程拆成可记录的运行机制。

```mermaid
stateDiagram-v2
    [*] --> Planned: 任务契约
    Planned --> Running: 启动主控和角色线程
    Running --> Heartbeat: 定期写状态
    Heartbeat --> Running: 未发现异常
    Heartbeat --> Blocked: 缺权限/缺输入/验证失败
    Heartbeat --> Expired: 到达截止时间
    Running --> LockedWrite: 需要写入最终产物
    LockedWrite --> Validating: 获得写锁并执行
    Validating --> Auditing: 验证结果
    Auditing --> Handoff: 写交接文件
    Blocked --> Handoff: 等待人工接管
    Expired --> Handoff: 停止并交还状态
    Handoff --> [*]
```

这就是为什么 MAGG 要使用多线程：**不是为了热闹，而是用线程承担原本由人类完成的持续审核、交叉检查、状态记录和异常接管。**

## 典型使用案例

### 1. 长时间无人值守生成/优化

```text
使用 $multi-agent-generative-governance 运行一个长时间无人值守优化任务。
要求启用 watchdog、heartbeat、write locks 和 latest handoff。
如果验证失败或任务超时，停止继续写入，并把当前状态交还给我。
```

预期行为：

- 进入 R2 模式。
- 明确截止条件和接管机制。
- 定期记录任务状态。
- 写入前使用锁。
- 验证失败时停止扩大修改。
- 最后输出 handoff，而不是假装全部完成。

### 2. 优化一个 Skill

```text
使用 $multi-agent-generative-governance 优化这个 Skill。
重点检查：触发描述、真实多线程边界、验证完整性、示例覆盖、安装同步。
先给任务契约和评测标准，再允许修改。
```

预期行为：

- 先定义“什么算真实改进”。
- 先设计 eval，而不是直接改文字。
- 红队找未来误用风险。
- 蓝队过滤偏好型意见。
- 裁判只允许具体文件和章节修改。
- 验证区分 L0/L1/L2/L3。

### 3. 真实多线程审查

```text
使用 $multi-agent-generative-governance 做真实多线程审查。
红队、蓝队、裁判、验证必须是独立 session。
不要让它们看到彼此结论，最后记录 session evidence。
```

预期行为：

- 创建或要求创建独立 session。
- 每个 session 使用短名称。
- 每个 session 只收到本角色需要的输入。
- 没有 session evidence 就不能宣称独立多线程。

### 4. 多候选方案比较

```text
使用 $multi-agent-generative-governance 为这个产品方案生成两个候选版本，再用裁判选择合并方向。
要求保留每个候选的优缺点、验证结果和合并理由。
```

预期行为：

- 进入 W2 或 W3 写入模式。
- 候选写入独立目录或分支。
- 合并前需要验证和裁判决策。
- 最终说明为什么选这个版本。

## 安装

把 Skill 文件夹复制到本机 Codex skills 目录：

```powershell
Copy-Item -Recurse .\multi-agent-generative-governance "$env:USERPROFILE\.codex\skills\multi-agent-generative-governance"
```

仓库结构：

```text
multi-agent-generative-governance-skill/
├── multi-agent-generative-governance/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── process-standard.md
│       ├── templates.md
│       └── example-runs.md
├── assets/
│   ├── hero-zh.svg
│   ├── governance-loop-zh.svg
│   ├── session-evidence-zh.svg
│   ├── validation-ladder-zh.svg
│   └── *-en.svg
└── docs/
    ├── MAGG_visual_deck.pdf
    └── MAGG_visual_deck.pptx
```

## 视觉版材料

仓库包含一份更适合展示的视觉介绍材料：

- [`docs/MAGG_visual_deck.pdf`](docs/MAGG_visual_deck.pdf)
- [`docs/MAGG_visual_deck.pptx`](docs/MAGG_visual_deck.pptx)

这份材料的结构是：前半中文，后半英文。图片也分成中文图和英文图，不在同一张图里混排。

---

## English Version

![Multi-Agent Generative Governance Skill](assets/hero-en.svg)

**Multi-Agent Generative Governance (MAGG)** is a Codex Skill for turning complex AI generation into an auditable governance process with role separation, controlled writes, validation evidence, long-running supervision, and handoff.

Its core advantage is not simply "more agents." MAGG uses independent threads and durable records to replace part of the human supervision loop: continuous review, cross-checking, write control, status tracking, and safe handoff when humans are not watching the task in real time.

### When To Use MAGG

Use MAGG when a task is too broad, risky, or easy to self-confirm for a single-pass generation:

- Long-running or unattended work that needs watchdog, heartbeat, locks, and handoff.
- Skill, SOP, prompt-system, or workflow optimization.
- Complex code projects or multi-file architecture work.
- Multi-section decks, reports, courseware, product plans, or story systems.
- True multi-thread or independent-session review.
- Candidate comparison and merge decisions.

Do not use MAGG for trivial edits, one-line Q&A, or work where the user only wants a fast draft.

### How To Use

```text
Use $multi-agent-generative-governance to review and improve this project plan.
Focus on scope, risks, write control, validation evidence, and what cannot be claimed.
```

For true independent review:

```text
Use $multi-agent-generative-governance for true multi-session review.
Red, Blue, Judge, and Validator must be separate sessions and must record session evidence.
```

### Architecture

![Governance loop](assets/governance-loop-en.svg)

MAGG is designed so threads can take over part of the work humans usually do during long tasks: checking assumptions, challenging outputs, approving writes, validating claims, recording state, and handing control back to a person when needed.

```mermaid
flowchart TB
    User["User Goal"] --> Contract["Task Contract"]
    Contract --> Triage["Mode Selection: G / W / R"]
    Triage --> Scope["Scope Lock"]
    Scope --> Red["Red Review"]
    Red --> Blue["Blue Response"]
    Blue --> Judge["Judge Decision"]
    Judge -->|Allow| Execute["Execute"]
    Execute --> Validate["Validate"]
    Validate --> Audit["Audit"]
    Audit --> Handoff["State Update / Handoff"]
    Judge -->|Reject / Defer| Scope
    Watchdog["Watchdog / Heartbeat"] --> Handoff
```

### True Threads

![Session evidence](assets/session-evidence-en.svg)

A same-session role pass is useful, but it is not independent. A real thread requires an independent Codex session and recorded session evidence.

### Validation

![Validation ladder](assets/validation-ladder-en.svg)

MAGG separates L0 static checks, L1 rule checks, L2 use-path checks, and L3 outcome proof. A validation report should always state what passed, what failed, what was not verified, environment gaps, and what cannot be claimed.

## License

MIT. See [`LICENSE`](LICENSE).
