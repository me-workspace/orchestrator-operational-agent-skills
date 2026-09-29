# Contributing

Thanks for helping improve the pack. New skills, sharper triggers, and better methodology are all welcome.

## The bar for a skill

A good skill is a **procedure**, not an essay. Before you open a PR, check:

1. **One folder, one `SKILL.md`.** Optional companion files (`CHECKLIST.md`, `SCENARIOS.md`, etc.) are loaded on demand and referenced from `SKILL.md`.
2. **Front matter is complete.**
   ```yaml
   ---
   name: kebab-case-name        # matches the folder name
   description: >-
     When to use this skill (trigger-rich). Include NEGATIVE triggers:
     "Do NOT use for X (use other-skill)."
   ---
   ```
3. **Body is procedural.** Checklists, rubrics, decision trees, quality gates. Keep it under ~500 lines; push depth into companion files.
4. **It is honest.** Anything touching tax, law, medicine, or finance is marked draft-until-verified. Do not invent numbers, citations, or testimonials.

## Workflow

1. Fork and branch from `main`.
2. Add or edit one skill per PR where possible; keep diffs focused.
3. Test the trigger: run 5 to 10 realistic prompts and confirm the skill fires when it should and stays quiet when it should not.
4. Open the PR with a short note on what changed and why.

Good first contributions: adapting the tax and compliance skills to other jurisdictions, or new operational skills.

By contributing you agree your work is released under the [MIT License](./LICENSE).
