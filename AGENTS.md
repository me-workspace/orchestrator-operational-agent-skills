# AI Agent Structure and Skill Assignment

A decision document: how many agents to build for the skills in this pack, which skill goes on which agent, and how it operates day to day (the example here uses Discord as the home for the agents).

An Indonesian version of this document is at [AGENTS.id.md](./AGENTS.id.md).

## Cross-agent skill (baseline, installed on EVERY agent)

`continuous-learning`: the anti-staleness discipline. It classifies fast-decay facts (must be verified before use), learns from corrections (record to memory and report so the skill can be updated), runs scheduled knowledge reviews per domain, and enforces honesty rules (never present a guess as fact). This is the skill that keeps the other skills from rotting silently. Because it sits on every agent, the "max skills per agent" counts below mean domain skills plus this one baseline.

## Division principles (why not one all-knowing agent, and not one agent per skill)

1. **Context limit and triggering.** The metadata (name + description) of every installed skill always sits in the agent's context. Past roughly 6 to 7 skills per agent, context gets crowded and cross-skill mis-triggering starts (two skills both feel summoned).
2. **Role cohesion.** Skills used together in ONE workflow belong on the same agent (review code, then deploy, then debug is one engineer's continuous flow; content calendar, then production, then edit is one content team's continuous flow). Splitting them forces expensive handoffs.
3. **Separation of concerns.** Healthy roles are deliberately kept apart: an editor editing their own writing loses distance; an auditor auditing their own work loses credibility. The PM and auditor are intentionally not given implementation skills.
4. **Sensitive data.** Agents that hold payroll, tax, and employee data (Finance, People) are separated from agents that talk to the public and clients (Marketing, Sales), so context leaking between conversations is impossible by design.

## Recommendation: 8 agents (1 leader + 7 specialists)

### 0. COO, the leader and parent of all agents (proactive by design)
**Skills (1 + baseline):** `coo-orchestrator` (+ `continuous-learning`)
**Job:** route every request to the right specialist, shepherd cross-agent chains to completion, post a daily ops pulse and a weekly ops review, detect stalls over 24 hours, remind of deadlines 72 hours out, escalate critical items immediately, and watch for patterns (propose a new skill or SOP when something recurs).
**Deliberately only 1 domain skill:** a COO with specialist skills is tempted to do the work itself and becomes a bottleneck. Its job is to delegate and then follow up. Hard limits inside the skill: it does not decide externally binding matters (contracts, pricing, hiring) and does not bypass role guardrails.

### 1. ENGINEER, the technical builder
**Skills (5):** `sdlc-master`, `code-review-hardening`, `secure-deploy-ops`, `incident-debugging`, `uiux-engineer`
**Job:** build, review, deploy, and keep systems alive, from PR to production, including frontend and UX engineering.
**Note:** this is the most-used agent; do not add any non-technical skill to it.

### 2. ARCHITECT, the senior technical brain (a deliberate split from Engineer)
**Skills (5):** `principal-engineering`, `strategic-approach`, `project-audit`, `agent-skill-author`, `tech-scout`
**Job:** architecture decisions and trade-offs, choosing an approach before execution, auditing project health, designing and auditing other agents' skills (meta), and running a routine tech radar (scouting new technology plus CVE and EOL watch for your own stack).
**Why tech-scout is here:** technology intelligence and adoption decisions should be adjacent but two steps apart. The scout presents a scored radar; principal-engineering and strategic-approach decide adoption. Schedule the radar weekly or biweekly as this agent's routine task.
**Why split from Engineer:** the assessor and the builder should not be one head. An audit of code "you" wrote is not credible, and a strategy discussion should not be tempted straight into coding.

### 3. PRODUCT MANAGER, requirements and schedule
**Skills (4):** `prd-creator`, `project-timeline-creator`, `strategic-approach`, `admin-ops`
**Job:** idea and discussion to PRD; PRD to timeline; project meeting to detailed two-tier minutes; keep scope and agreements recorded.
**Note:** `strategic-approach` is deliberately on both PM and Architect. The PM uses it for product and MVP scoping, the Architect for technical direction; the two contexts rarely collide because the agents differ.

### 4. DESIGNER, the visual eye
**Skills (2):** `product-designer`, `uiux-engineer`
**Job:** visual concepts, design system, critique, and UI specs ready to implement.
**Note:** `uiux-engineer` deliberately overlaps with Engineer. On Designer it is used as a specification language (5 states, accessibility) so handoff to Engineer needs no translation. To economize, this agent can be merged into Engineer (see the 5-agent option).

### 5. FINANCE, money in, money out, and obligations
**Skills (2):** `finance-analyst`, `accounting-core`
**Job:** daily bookkeeping to monthly closing to analysis (runway, unit economics, pricing) to the tax calendar.
**Note:** these two are one continuous flow (record first, analyze later) but two hats. The skill descriptions already exclude each other, so they are safe on one agent. Hard rule: tax figures are always draft-until-verified.

### 6. GROWTH, the brand's public voice
**Skills (4):** `marketing-growth`, `social-media-specialist`, `content-creator`, `content-editor`
**Job:** campaign strategy to calendar and channels to content production to a quality gate before publishing. The full content pipeline lives on one agent because the flow is daily and back-and-forth.
**Note:** once content volume is high, split `content-editor` to a separate agent to restore editorial distance (writer is not the assessor). That is this agent's first split trigger.

### 7. PEOPLE AND SALES OPS, humans and relationships
**Skills (4):** `hr-officer`, `hr-admin`, `sales-pipeline`, `admin-ops`
**Job:** recruitment through payroll, lead qualification through proposal, plus general administration.
**Note:** this is the only cross-functional combined agent, viable while HR and sales volume are still low. Split trigger: once there are more than about 10 employees OR an active sales pipeline over about 15 deals, split into PEOPLE (hr-officer + hr-admin) and SALES (sales-pipeline + admin-ops). Payroll and employee data are confidential; never use this agent for conversations involving external parties.

## Full matrix

| Skill | ENG | ARC | PM | DSG | FIN | GRW | P&S |
|---|---|---|---|---|---|---|---|
| sdlc-master | X | | | | | | |
| code-review-hardening | X | | | | | | |
| secure-deploy-ops | X | | | | | | |
| incident-debugging | X | | | | | | |
| uiux-engineer | X | | | X | | | |
| principal-engineering | | X | | | | | |
| strategic-approach | | X | X | | | | |
| project-audit | | X | | | | | |
| agent-skill-author | | X | | | | | |
| tech-scout | | X | | | | | |
| prd-creator | | | X | | | | |
| project-timeline-creator | | | X | | | | |
| admin-ops | | | X | | | | X |
| product-designer | | | | X | | | |
| finance-analyst | | | | | X | | |
| accounting-core | | | | | X | | |
| marketing-growth | | | | | | X | |
| social-media-specialist | | | | | | X | |
| content-creator | | | | | | X | |
| content-editor | | | | | | X | |
| sales-pipeline | | | | | | | X |
| hr-officer | | | | | | | X |
| hr-admin | | | | | | | X |

Total: 25 skills (23 domain + coo-orchestrator + continuous-learning baseline on every agent), 8 agents (1 leader + 7 specialists), at most 5 domain skills per agent, 3 skills deliberately doubled (uiux-engineer, strategic-approach, admin-ops) with the reasons written above. `coo-orchestrator` lives only on the COO; never install it on a specialist (two orchestrators means a routing war).

## Operations on Discord (the agents' home)

All agents live on one Discord server; humans (you and the team) interact through channels. Design principles:

**1. One channel per agent, not one crowded channel.**
`#engineer` `#architect` `#product` `#design` `#finance` `#growth` `#people-sales`: a channel is the agent's conversation context. Mixing all agents in one channel breaks routing (everyone feels summoned) and mixes context.

**2. Restricted channels for sensitive data.**
`#finance` and `#people-sales` must be private (role-restricted). Payroll, tax, employee data, and deal negotiations must not be readable by general server members. This mirrors the data-isolation principle in the agent split.

**3. Broadcast channels: `#radar` and `#daily-ops`.**
- `#radar`: the ARCHITECT posts the scheduled tech radar plus CVE and EOL alerts. Everyone reads; no one asks there (discussion goes to #architect).
- `#daily-ops`: a short daily and weekly summary from each agent (one message: what was done, what needs a human decision), so the owner can scan 7 agents in one scroll.

**4. Handoff between agents goes through artifacts, not across channels.**
An agent does not read another agent's channel. PRDs, timelines, minutes, and design docs are stored in shared storage (repo or drive) and the link is handed by a human (or a router bot) to the next agent's channel. This is intentional: it prevents a hallucination chain between agents and keeps the human at the decision point.

**5. Action guardrails on Discord.**
A Discord message is untrusted input: an agent only obeys commands from allowed roles (owner or admin), not any member. This is a hard rule in the system, not just in the prompt. External actions (email or WhatsApp to a client, transfers, social posts, deploys) always require explicit confirmation in the channel from a human with the right role, with a summary of what will be done.

**6. Scheduled tasks.**
A cron per agent triggers its routine and posts the result to its channel: FINANCE, monthly closing and tax calendar (start of month); ARCHITECT, tech radar (weekly) plus continuous-learning knowledge review (monthly, mandatory in January for the annual regulations); GROWTH, content metrics review (weekly); PEOPLE, HR compliance calendar (start of month). An empty result is still reported in one line; the absence of a report must mean a problem, not ambiguity.

## Lean option: 5 agents (if server capacity or cost is limited)
1. **ENGINEER+** = ENGINEER + DESIGNER (7 skills, already at the top of the range)
2. **ARCHITECT** unchanged (4)
3. **PM** unchanged (4)
4. **FINANCE+OPS** = FINANCE + hr-admin + admin-ops (5), everything bookkeeping and administrative
5. **GROWTH+SALES** = GROWTH + sales-pipeline, with hr-officer moved to PM (6)
Trade-off: ENGINEER+ is heavy, and Growth+Sales mixes the public voice with one-on-one negotiation. Use only as a transition phase.

## Cross-agent workflow (example: a new feature end to end)
Idea -> **PM** (PRD + kickoff minutes) -> **ARCHITECT** (approach + design review) -> **PM** (timeline) -> **DESIGNER** (UI spec) -> **ENGINEER** (build, review, deploy) -> **ARCHITECT** (periodic audit) -> **GROWTH** (launch content) -> **FINANCE** (record revenue, measure unit economics).
Handoff between agents always goes through a written artifact (PRD, design doc, timeline, minutes), not "continue from the chat next door", because agents do not share context.

## Suggested rollout
Do not turn on all 7 at once. Order: ENGINEER -> PM -> FINANCE (the three most frequent flows), then the rest after 1 to 2 weeks of observing triggering. For each new agent: test 5 to 10 real prompts, note mis-triggers, sharpen the negative triggers in the description before continuing.
