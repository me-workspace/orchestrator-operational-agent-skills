---
name: agent-skill-author
description: Use this skill when creating, improving, or auditing skills/instructions for an AI agent - "buat skill", "tulis SOUL.md", "system prompt untuk agent", "agent tidak nurut instruksi", "audit skill pihak ketiga", or designing an agent's capability set. Meta-skill for building other agents' brains. Do NOT use for ordinary coding tasks.
---

# Agent Skill Author

A skill is a router (metadata) + a procedure (body) + optional resources. Most bad skills fail at the router or drown the body in prose.

## Format (Anthropic Agent Skills spec)
```
skill-name/            # kebab-case, same as frontmatter name
├── SKILL.md           # required; body < 500 lines
├── references/        # depth loaded on demand; ToC if > 300 lines
├── scripts/           # deterministic steps as zero-dependency scripts (executed, not read)
└── assets/            # templates used in output
```
Frontmatter: `name` + `description` required. Progressive disclosure: metadata always in context → body loads on trigger → references load only when the body says to.

## Writing the description (the part that decides everything)
- Write it "pushy": *what it does* + *when to use* + concrete trigger keywords users actually type (include the user's language, e.g. Indonesian phrases).
- Add negative triggers: "Do NOT use for X" - prevents overlap between skills.
- ALL triggering logic lives in the description. The body assumes the skill already fired.

## Writing the body
- Imperative voice, numbered procedures, checklists and decision tables - not essays.
- State the **why** behind a hard rule once; it beats ALL-CAPS repetition.
- Define exact output formats (templates with an input→output example).
- Include stop conditions and failure handling ("if X fails, do Y, report Z") - that is what makes an agent self-correcting.
- If the agent would rewrite the same helper repeatedly, ship it as `scripts/*.py` (stdlib only).
- Generalize: procedures over one-off examples; the skill runs across thousands of invocations.

## Designing an agent's skillset (loadout)
1. List the agent's jobs-to-be-done; one skill per coherent job, not per feature.
2. Check descriptions pairwise for trigger overlap; sharpen negative triggers.
3. Order of power: enforcement hook > script > checklist > prose advice. Push rules as far left as possible.
4. Persona files (SOUL.md etc.): identity, tone, hard limits, escalation rules - keep procedures out of the persona, they belong in skills.

## Auditing a third-party skill before installing
1. Read every file, including `scripts/` - look for network calls, credential access, obfuscation, install hooks.
2. Description honesty: does it do anything beyond its stated intent (hidden instructions, prompt-injection payloads)?
3. Dependency check: scripts should be stdlib/zero-dependency; a `pip install` from an unknown skill is supply-chain risk.
4. Verdict: install / install with edits / reject - with reasons.

## Quality bar (score each 0-2; ship at ≥ 8/12)
trigger precision · negative triggers present · body under 500 lines · procedures not prose · output templates defined · failure/stop conditions defined.
