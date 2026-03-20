# autoresearch-pro

> Automatically improve any OpenClaw skill through iterative mutation-testing loops.
> Inspired by [Karpathy/autoresearch](https://github.com/karpathy/autoresearch).

**autoresearch-pro** is an OpenClaw skill that applies Karpathy's autoresearch methodology to optimize other OpenClaw skills — improving prompts, wording, constraints, examples, and tool descriptions through systematic mutation-testing.

## How It Works

The core loop:

```
For each round (up to 100):
  1. Make ONE small edit to the target skill's SKILL.md
  2. Score the result against a checklist (10 criteria)
  3. Score went up? → Keep the change
  4. Score went down? → Revert it
  5. Every 30 rounds → pause for human review
```

You define **what "good" looks like** via checklist questions. The agent handles the rest.

## Installation

### Option 1: Install via ClawHub (recommended)

```bash
clawhub install autoresearch-pro
```

### Option 2: Manual install

```bash
# Clone into your OpenClaw skills directory
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

## Usage

Trigger the skill by saying:

```
optimize [skill-name]
autoresearch [skill-name]
improve my [skill-name] skill
```

For example:

```
optimize merge-drafts
autoresearch feishu-calendar
```

The agent will:
1. Read the target skill's `SKILL.md`
2. Generate 10 checklist questions (you select which to use)
3. Run the autoresearch loop — 30 rounds, then pause for your confirmation
4. Continue up to 100 rounds total
5. Report the final improvements

## Checklist Questions

The skill evaluates skills against 10 dimensions:

| # | Dimension |
|---|-----------|
| 1 | Description clarity and actionability |
| 2 | Trigger coverage (does it catch real use cases?) |
| 3 | Workflow step clarity and sequencing |
| 4 | Error handling completeness |
| 5 | OpenClaw tool usage accuracy |
| 6 | Example quality and realism |
| 7 | Content conciseness (no redundancy) |
| 8 | Freedom calibration (right constraint/flexibility balance) |
| 9 | Reference quality and accuracy |
| 10 | Section completeness (no TODO placeholders) |

## Mutation Strategies

Small, targeted edits per round:

- Add a constraint rule (`must` / `never`)
- Strengthen trigger description
- Add a concrete example to a vague step
- Tighten vague language ("try to" → "must")
- Improve error handling
- Remove redundant content
- Add cross-references between sections
- Expand thin sections
- Improve section transitions

**One mutation per round** — small changes are verifiable; large rewrites are not.

## Project Structure

```
autoresearch-pro/
├── SKILL.md                           # Main skill (load this into OpenClaw)
├── scripts/
│   └── run_eval.py                    # Optional evaluation helper script
└── references/
    └── mutation_strategies.md         # Mutation strategy reference
```

## Real-World Results

Used to optimize the `merge-drafts` skill (draft merging tool):
- Description triggers: 6 → 15 variants
- Error handling cases: 4 → 13 scenarios
- Constraint rules: 0 → 10 mandatory rules
- All vague language precisely defined
- Steps fully cross-referenced

## References & Credits

- **Karpathy/autoresearch** — the original idea: [github.com/karpathy/autoresearch](https://github.com/karpathy/autoresearch)
- Inspired by the paper *Systematic Testing for Large Language Model Applications* (auto-grading via executable checklists)

## License

MIT

---

*If this tool saved you time, consider leaving a star ⭐*
