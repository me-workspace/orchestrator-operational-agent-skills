# Agent Skills for Business and Engineering

> 25 portable skills that turn a generic AI assistant into an operating team: ship software end to end and run the business around it, from PRDs and code review to finance, marketing, and HR.

![Skills](https://img.shields.io/badge/skills-25-2563eb)
![License](https://img.shields.io/badge/license-MIT-16a34a)
![Spec](https://img.shields.io/badge/spec-Agent%20Skills-111827)
![Claude Code](https://img.shields.io/badge/works%20with-Claude%20Code-8b5cf6)
![PRs welcome](https://img.shields.io/badge/PRs-welcome-f59e0b)

A **Skill** is a folder with a `SKILL.md` file: a focused, reusable procedure an AI agent loads only when it is relevant. This repo is a curated set of them, written to the [Anthropic Agent Skills](https://agentskills.io) spec, so they drop into Claude Code, the Claude Agent SDK, or any agent runtime that reads `SKILL.md`.

It is more than a pile of prompts. Every skill is a checklist, rubric, or decision tree with quality gates, and [`AGENTS.md`](./AGENTS.md) shows how to compose them into an 8-agent company (COO plus seven specialists) without the skills fighting each other for context.

---

## Why this pack

- **Procedures, not prose.** Skills produce consistent, reviewable output instead of freestyle text.
- **Trigger-rich descriptions.** Each `SKILL.md` says exactly when to fire, and when NOT to, which cuts wrong-skill activation when you install many.
- **Context-cheap.** Only the name and description sit in context; the body loads on demand. Install a dozen skills without drowning the window.
- **Honest by construction.** Skills that touch tax, law, or money carry a draft-until-verified rule inside the skill itself.
- **Portable.** If your agent can read a `SKILL.md`, it can use these.

---

## Quick start (Claude Code)

```bash
git clone https://github.com/me-workspace/agent-skills.git

# One skill, project-scoped
cp -r agent-skills/marketing-growth  .claude/skills/

# Or install a role loadout, globally
cp -r agent-skills/{prd-creator,project-timeline-creator,strategic-approach,admin-ops}  ~/.claude/skills/
```

The next time a matching request comes in ("write a campaign brief", "draft a PRD", "review this diff"), the agent loads the skill automatically.

> Do not install all 25 into one agent. Metadata for every installed skill stays in context. Pick a loadout per role. See [`AGENTS.md`](./AGENTS.md) for a worked design.

---

## The skills

### Software and AI (full SDLC)
| Skill | What it does |
|---|---|
| [`sdlc-master`](./sdlc-master) | End-to-end lifecycle: phases and gates, tech design doc, Definition of Done, branching, testing strategy |
| [`principal-engineering`](./principal-engineering) | Principal-level judgment: principles, trade-offs, decision framework, standard calls |
| [`strategic-approach`](./strategic-approach) | Choosing an approach: framing, three diverse options, recommendation plus kill criteria, MVP scoping |
| [`prd-creator`](./prd-creator) | Full PRD: measurable goals, mandatory non-goals, Given/When/Then acceptance criteria |
| [`project-timeline-creator`](./project-timeline-creator) | Timelines: breakdown to 2 days or less, dependencies, 1.5x buffer, critical path, slip protocol |
| [`project-audit`](./project-audit) | Project audit: 7 scored dimensions, evidence-based method, prioritized report and verdict |
| [`code-review-hardening`](./code-review-hardening) | Code review: correctness and security, verify before reporting, severity rubric |
| [`secure-deploy-ops`](./secure-deploy-ops) | Deploy: pre-deploy backup, live vs staged diff, smoke test, hardening baseline |
| [`incident-debugging`](./incident-debugging) | Production debugging: evidence-first, discriminating hypotheses, minimal fix, write-up |
| [`uiux-engineer`](./uiux-engineer) | UI/UX engineering: five required states, forms, responsive, accessibility, usability review |
| [`product-designer`](./product-designer) | Designer's eye: hierarchy, typography, color, spacing system, design system, critique |
| [`agent-skill-author`](./agent-skill-author) | Meta-skill: write and audit other agents' skills against a 12-point quality bar |
| [`tech-scout`](./tech-scout) | Tech radar: source sweep, 6-dimension rubric, hype immunity, CVE and EOL watch |

### Operations
| Skill | What it does |
|---|---|
| [`finance-analyst`](./finance-analyst) | SaaS metrics, runway, unit economics, pricing, monthly snapshot, red flags |
| [`accounting-core`](./accounting-core) | Double-entry journals, chart of accounts, reconciliation, assets and depreciation, tax draft, closing |
| [`sales-pipeline`](./sales-pipeline) | Scored lead qualification, discovery, proposal with scope exclusions, cadence, negotiation |
| [`marketing-growth`](./marketing-growth) | Campaign briefs, copywriting rules, SEO checklist, growth experiments, funnel review |
| [`social-media-specialist`](./social-media-specialist) | Per-platform grammar, content calendar and pillars, repurposing chain, metrics review |
| [`content-creator`](./content-creator) | Production: hook patterns, per-format structure (article, script, newsletter, thread), storytelling |
| [`content-editor`](./content-editor) | Four-pass quality gate: structure, clarity, style, correctness; verdict plus kill criteria |
| [`admin-ops`](./admin-ops) | SOPs, two-tier meeting minutes, email triage, document conventions |
| [`hr-officer`](./hr-officer) | Rubric-based recruitment, 30-day onboarding, performance, sensitive cases, compensation |
| [`hr-admin`](./hr-admin) | Payroll and statutory deductions (draft-until-verified), leave and attendance, contracts, compliance calendar |

### Cross-agent
| Skill | What it does |
|---|---|
| [`coo-orchestrator`](./coo-orchestrator) | Leader agent: routing, cross-agent chain shepherding, daily ops pulse, weekly review, escalation, accountability register |
| [`continuous-learning`](./continuous-learning) | Baseline for every agent: fast-decay fact classification with mandatory verification, learning from corrections, scheduled knowledge review, honesty rules |

> Tax and compliance skills (`accounting-core`, `hr-admin`, `hr-officer`) include Indonesia-oriented specifics and are marked draft-until-verified against the current year's regulations or a licensed professional. Adapt them to your jurisdiction.

---

## Compose them into a team

[`AGENTS.md`](./AGENTS.md) is a full worked design: which skills go on which agent, why the roles are split the way they are (an auditor should not audit its own work; finance data stays isolated from public-facing agents), and how to run it day to day. It also gives a lean 5-agent option. (Written in Indonesian; an English version is welcome as a PR.)

## How a skill works

```
skill-name/
└── SKILL.md    # front matter (name + description) + the procedure
```

```markdown
---
name: marketing-growth
description: Use this skill for marketing work, campaigns, SEO, ads, copywriting,
  landing pages, funnels. Do NOT use for one-to-one sales (use sales-pipeline).
---

# Marketing and Growth
No deliverable without: target audience, single message, measurable metric...
```

The agent keeps every skill's `description` in context and reads the body only when a task matches. That is what makes a large pack practical.

## Contributing

New skills, sharper triggers, and better methodology are welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md). Keep skills procedural, keep descriptions trigger-rich.

## License

[MIT](./LICENSE) (c) 2026 Wira Darma. Use them, fork them, ship them.

Indonesian catalog: [README.id.md](./README.id.md).

---

<p align="center"><b>If this pack saves you time, a star helps others find it.</b></p>
