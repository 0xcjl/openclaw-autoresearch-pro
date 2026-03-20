# autoresearch-pro

> Automatically improve any OpenClaw skill, prompt, or article through iterative mutation-testing loops.
> Inspired by [Karpathy/autoresearch](https://github.com/karpathy/autoresearch).

**autoresearch-pro** applies Karpathy's autoresearch methodology to optimize any text-based content — OpenClaw skills, prompts, or articles — through systematic mutation-testing.

## Three Optimization Modes

| Mode | Use when | Input |
|------|----------|-------|
| **Skill** | "optimize merge-drafts" | A skill's SKILL.md |
| **Prompt** | "optimize this prompt" | Any prompt text |
| **Article** | "polish this article" | Any document/text |

## How It Works

```
For each round (up to 100):
  1. Make ONE small edit to the target content
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
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

## Usage

**Skill mode:**
```
optimize merge-drafts
autoresearch feishu-calendar
improve my skill feishu-task
```

**Prompt mode:**
```
optimize this prompt: [paste your prompt]
improve my prompt
```

**Article mode:**
```
polish this article: [paste article text]
improve this article
```

The agent will:
1. Read the target content and generate 10 checklist questions
2. You select which criteria to use (or use all 10 by default)
3. Run the loop — 30 rounds, then pause for your confirmation
4. Continue up to 100 rounds total
5. Report final improvements

## Checklist Questions

**Skill mode:**

| # | Dimension |
|---|-----------|
| 1 | Description clarity and actionability |
| 2 | Trigger coverage (real-world use cases) |
| 3 | Workflow step clarity and sequencing |
| 4 | Error handling completeness |
| 5 | OpenClaw tool usage accuracy |
| 6 | Example quality and realism |
| 7 | Content conciseness (no redundancy) |
| 8 | Freedom calibration (constraint/flexibility balance) |
| 9 | Reference quality and accuracy |
| 10 | Section completeness (no placeholders) |

**Prompt mode:**

| # | Dimension |
|---|-----------|
| 1 | Goal clarity and specificity |
| 2 | Role/tone specification |
| 3 | Input format description |
| 4 | Output format specification |
| 5 | Constraint boundaries stated |
| 6 | Context sufficiency to avoid hallucination |
| 7 | Edge case handling |
| 8 | Conciseness (no contradictions) |
| 9 | Actionability (concrete vs. vague) |
| 10 | Completeness of necessary elements |

**Article mode:**

| # | Dimension |
|---|-----------|
| 1 | Title clarity and value proposition |
| 2 | Opening hook quality |
| 3 | Logical structure |
| 4 | Argument support with evidence |
| 5 | Conciseness (no padding) |
| 6 | Transition flow |
| 7 | Closing strength |
| 8 | Tone consistency |
| 9 | Readability (sentence variation) |
| 10 | Audience match |

## Mutation Strategies

Small, targeted edits per round:

- Add a constraint rule (`must` / `never`)
- Strengthen trigger/coverage description
- Add a concrete example to a vague step
- Tighten vague language ("try to" → "must")
- Improve error/edge case handling
- Remove redundant content
- Improve section transitions
- Expand thin sections
- Add cross-references between sections
- Adjust degree-of-freedom calibration

**One mutation per round** — small changes are verifiable; large rewrites are not.

## Project Structure

```
autoresearch-pro/
├── SKILL.md                           # Main skill
├── scripts/
│   └── run_eval.py                   # Evaluation helper
└── references/
    └── mutation_strategies.md         # Mutation strategy guide
```

## Real-World Results

Optimized the `merge-drafts` skill through 30 rounds:
- Description triggers: 6 → 15 variants
- Error handling scenarios: 4 → 13 cases
- Constraint rules: 0 → 10 mandatory rules
- All vague language precisely defined
- Steps fully cross-referenced

## Credits

- **[Karpathy/autoresearch](https://github.com/karpathy/autoresearch)** — the original idea and methodology
- Inspired by the core insight: let an agent improve code/prompts through iterative mutation-testing loops

## License

MIT
