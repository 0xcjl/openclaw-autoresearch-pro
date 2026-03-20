---
name: autoresearch-pro
description: Automatically iterate and improve any OpenClaw skill's SKILL.md through mutation-testing loops. Inspired by Karpathy's autoresearch. Use when the user says "optimize [skill]", "autoresearch [skill]", "improve my skill", or explicitly requests skill quality improvement. Not for general Q&A or other tasks.
---

# autoresearch-pro

## Overview

Automatically improve any OpenClaw skill through iterative mutation-testing: small edits to SKILL.md → run test cases → score with checklist → keep improvements, discard regressions. Works on any skill in `~/.openclaw/skills/`.

**Inspired by [Karpathy/autoresearch](https://github.com/karpathy/autoresearch).**

---

## Workflow

### Step 1 — Identify Target Skill

Ask the user for the skill to optimize if not already specified. Resolve the skill path:

```
~/.openclaw/skills/<skill-name>/
```

If the skill name is ambiguous, list `~/.openclaw/skills/` and ask which one.

### Step 2 — Generate Checklist (10 Questions)

Read the target skill's SKILL.md fully first. Then generate 10 diverse, specific yes/no checklist questions that evaluate output quality across these dimensions:

| # | Dimension | What to Check |
|---|----------|---------------|
| 1 | Description clarity | Is the `description` in frontmatter precise and actionable? |
| 2 | Trigger coverage | Does the description cover the main real-world use cases? |
| 3 | Workflow structure | Are workflow steps clearly sequenced and non-ambiguous? |
| 4 | Error guidance | Does it handle error states and edge cases? |
| 5 | Tool usage accuracy | Are tool names and parameters correct for OpenClaw? |
| 6 | Example quality | Do examples reflect real usage patterns? |
| 7 | Conciseness | Is the content free of redundant/unnecessary repetition? |
| 8 | Freedom calibration | Is the degree of freedom (instruction specificity) appropriate? |
| 9 | Reference quality | Are references/links accurate and useful? |
| 10 | Completeness | Are all necessary sections present and filled in? |

**Present the 10 questions to the user**, numbered 1-10. Ask them to select which ones to activate (e.g., "use questions 1, 3, 5, 7"). Default: use all 10 if user doesn't specify.

### Step 3 — Prepare Test Cases

Generate 3-5 realistic test inputs that represent the skill's real usage scenarios. These should be concrete prompts or inputs that a user would actually send when using the target skill.

Store test cases in memory or a temp variable — do not write to disk.

### Step 4 — Run Autoresearch Loop

**Loop configuration:**
- **Rounds per batch**: 30
- **Max total rounds**: 100
- **Pause**: After every batch of 30 rounds, show summary and ask user to continue or stop
- **Stop condition**: User says stop, OR all 100 rounds completed

**Per-round procedure:**

1. **Mutate**: Make ONE small edit to the target SKILL.md. Mutation types (pick one randomly or strategically):
   - Rewrite/add a constraint rule in the description or workflow
   - Add/remove/refine a workflow step
   - Strengthen or clarify a vague instruction
   - Add an example to a section
   - Tighten or expand degree of freedom in a instruction
   - Remove redundant content
   - Improve a section header or transition text

2. **Test**: For each test case, run the skill by reading SKILL.md and simulating how the skill would respond. Since we cannot actually invoke the skill in a sub-agent, simulate by reading the SKILL.md and reasoning about what output it would produce given the test input.

3. **Score**: For each test output, apply each active checklist question (0 or 1 per question). Score = (passed / total) × 100.

4. **Decide**: If new average score ≥ previous best score → keep the mutation (write it). If lower → revert to previous version.

5. **Log**: Record round number, mutation type, score delta, and keep/revert decision.

**Keep a running diff** showing the accumulated improvements vs. the original SKILL.md.

### Step 5 — Report Results

After each batch (every 30 rounds), report:

```
Batch N (rounds X-Y):
  Best score: XX%
  Mutations kept: N  |  Reverted: N
  Most effective mutation types: [list top 2-3]

Accumulated improvements:
[brief description of what changed]

Continue? (yes/stop)
```

After full completion (100 rounds or user stop), show final summary:
- Original score vs. final score
- Top 3 most impactful mutations
- Final diff (or summary of changes)
- File path of optimized skill

---

## Mutation Strategy Reference

When making mutations, prefer:

**High-impact, low-risk changes:**
- Adding explicit [constraints] or [禁止] rules where the skill currently is vague
- Expanding description triggers to cover edge cases the user has encountered
- Adding concrete examples to abstract workflow steps
- Tightening vague language ("optionally" → "always do X unless Y")

**Avoid:**
- Large rewrites of entire sections in one round
- Changing the skill's fundamental scope
- Adding external dependencies or scripts not already present

---

## Tips

- The goal is **small, verifiable improvements** — one precise edit per round is better than many simultaneous changes.
- If a mutation improves one test case but hurts another, weigh the net delta carefully.
- Use the checklist as objective guardrails — don't let the model "explain away" a regression.
- The user is the final judge of quality — report honestly, even if the score didn't improve much.
