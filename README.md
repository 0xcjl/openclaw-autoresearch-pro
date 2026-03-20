# autoresearch-pro

> Automatically improve any OpenClaw skill, prompt, or article through iterative mutation-testing loops.
> Inspired by [Karpathy/autoresearch](https://github.com/karpathy/autoresearch).

**Language:** [English](#english) · [中文](#中文) · [日本語](#日本語) · [Español](#español) · [Français](#français)

---

## English

### Overview

**autoresearch-pro** applies Karpathy's autoresearch methodology to optimize any text-based content — OpenClaw skills, prompts, or articles — through systematic mutation-testing.

### Three Optimization Modes

| Mode | Use when | Input |
|------|----------|-------|
| **Skill** | "optimize merge-drafts" | A skill's SKILL.md |
| **Prompt** | "optimize this prompt" | Any prompt text |
| **Article** | "polish this article" | Any document/text |

### How It Works

```
For each round (up to 100):
  1. Make ONE small edit to the target content
  2. Score the result against a checklist (10 criteria)
  3. Score went up? → Keep the change
  4. Score went down? → Revert it
  5. Every 30 rounds → pause for human review
```

You define **what "good" looks like** via checklist questions. The agent handles the rest.

### Installation

```bash
# Via ClawHub (recommended)
clawhub install autoresearch-pro

# Manual
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

### Usage

```
optimize merge-drafts
autoresearch feishu-calendar
optimize this prompt: [paste your prompt]
polish this article: [paste article text]
```

### Checklist Questions

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

### Mutation Strategies

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

### Real-World Results

Optimized the `merge-drafts` skill through 30 rounds:
- Description triggers: 6 → 15 variants
- Error handling scenarios: 4 → 13 cases
- Constraint rules: 0 → 10 mandatory rules
- All vague language precisely defined
- Steps fully cross-referenced

### Credits

- **[Karpathy/autoresearch](https://github.com/karpathy/autoresearch)** — the original idea
- Method: let an agent improve code/prompts through iterative mutation-testing loops

### License

MIT

---

## 中文

### 概述

**autoresearch-pro** 将 Karpathy 的 autoresearch 方法应用于优化任何基于文本的内容 — OpenClaw skill、prompt 或文章 — 通过系统性突变测试提升质量。

### 三种优化模式

| 模式 | 使用场景 | 输入 |
|------|----------|------|
| **Skill** | "优化 merge-drafts" | 技能的 SKILL.md |
| **Prompt** | "优化这个 prompt" | 任意 prompt 文本 |
| **Article** | "润色这篇文章" | 任意文章/文档 |

### 原理

```
每轮（最多100轮）：
  1. 对目标内容做一个小改动
  2. 用 checklist（10个维度）给结果打分
  3. 分数提升？→ 保留改动
  4. 分数下降？→ 撤销改动
  5. 每 30 轮 → 暂停等待人工确认
```

你只需要定义"好"的标准，其余全部自动完成。

### 安装

```bash
# 通过 ClawHub 安装（推荐）
clawhub install autoresearch-pro

# 手动安装
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

### 使用方法

```
优化 merge-drafts
autoresearch feishu-calendar
优化这个 prompt：[粘贴 prompt]
润色这篇文章：[粘贴文章]
```

### Checklist 维度

**Skill 模式：** Description清晰度 / 触发词覆盖 / 工作流结构 / 错误处理 / 工具准确性 / 示例质量 / 简洁性 / 自由度校准 / 参考质量 / 完整性

**Prompt 模式：** 目标清晰度 / 角色语气 / 输入格式 / 输出格式 / 约束边界 / 上下文充分性 / 边缘情况 / 简洁性 / 可操作性 / 必要元素完整

**Article 模式：** 标题质量 / 开篇吸引力 / 逻辑结构 / 论证支撑 / 简洁性 / 过渡流畅 / 结尾力度 / 语气一致 / 可读性 / 读者匹配

### 突变策略

每轮只做一个小的精准改动：添加约束规则、强化触发词、为模糊步骤添加示例、精化模糊措辞、完善错误处理、删除冗余、改善过渡、扩充薄弱章节。

**每轮只改一处** — 小改动可验证，大改写无法评估。

### 实际效果

优化 `merge-drafts` skill（30轮）：Description触发词从6个扩展到15个，错误处理从4种扩展到13种，新增10条约束规则，所有模糊措辞精确化。

### 致谢

- **[Karpathy/autoresearch](https://github.com/karpathy/autoresearch)** — 原始想法

### License

MIT

---

## 日本語

### 概要

**autoresearch-pro**は、Karpathyのautoresearch手法を応用し、OpenClawスキル、 프롬프트、文章などのテキストベースのコンテンツを反復的な突然変異テストによって最適化します。

### 3つの最適化モード

| モード | 使い時 | 入力 |
|--------|--------|------|
| **Skill** | "optimize merge-drafts" | スキルのSKILL.md |
| **Prompt** | "optimize this prompt" | 任意の 프롬프트テキスト |
| **Article** | "polish this article" | 任意の文章/ドキュメント |

### 動作原理

```
各ラウンド（最大100ラウンド）：
  1. 対象コンテンツに小さな編集を1つ加える
  2. チェックリスト（10基準）でスコア付け
  3. スコア向上？→ 変更を保持
  4. スコア低下？→ 変更を元に戻す
  5. 30ラウンドごと → 人間のレビューで一時停止
```

「良い」の基準をチェックリスト質問で定義すれば、後はエージェントが自動的に処理します。

### インストール

```bash
# ClawHubを使用（推奨）
clawhub install autoresearch-pro

# 手動
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

### 使用例

```
optimize merge-drafts
autoresearch feishu-calendar
optimize this prompt: [프롬プトを貼り付け]
polish this article: [記事を貼り付け]
```

### 突然変異戦略

各ラウンドで1つの小さな編集のみ：制約ルールの追加、トリガー強化、例追加、曖昧な表現の明確化、エラー処理の改善、冗長性の削除、セクション移行の改善。

**1ラウンド1つの編集** — 小さな変更は検証可能、大規模な書き直しは評価不能。

### クレジット

- **[Karpathy/autoresearch](https://github.com/karpathy/autoresearch)** — 元のアイデア

### License

MIT

---

## Español

### Descripción general

**autoresearch-pro** aplica la metodología de autoresearch de Karpathy para optimizar cualquier contenido basado en texto — skills de OpenClaw, prompts o artículos — mediante pruebas de mutación sistemáticas.

### Tres modos de optimización

| Modo | Cuándo usarlo | Entrada |
|------|---------------|---------|
| **Skill** | "optimize merge-drafts" | SKILL.md de un skill |
| **Prompt** | "optimize this prompt" | Cualquier texto de prompt |
| **Article** | "polish this article" | Cualquier documento/texto |

### Cómo funciona

```
Por cada ronda (hasta 100):
  1. Haz UNA pequeña edición en el contenido objetivo
  2. Califica el resultado contra una lista de verificación (10 criterios)
  3. ¿Puntuación subió? → Mantén el cambio
  4. ¿Puntuación bajó? → Revierte el cambio
  5. Cada 30 rondas → pausa para revisión humana
```

Tú defines **qué significa "bueno"** mediante preguntas de checklist. El agente hace el resto.

### Instalación

```bash
# Vía ClawHub (recomendado)
clawhub install autoresearch-pro

# Manual
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

### Uso

```
optimize merge-drafts
autoresearch feishu-calendar
optimize this prompt: [pega tu prompt]
polish this article: [pega el artículo]
```

### Estrategias de mutación

Una pequeña edición por ronda: agregar regla de restricción, fortalecer triggers, añadir ejemplos, precisar lenguaje vago, mejorar manejo de errores, eliminar redundancia, mejorar transiciones.

**Una mutación por ronda** — cambios pequeños son verificables; reescrituras grandes no lo son.

### Créditos

- **[Karpathy/autoresearch](https://github.com/karpathy/autoresearch)** — la idea original

### Licencia

MIT

---

## Français

### Vue d'ensemble

**autoresearch-pro** applique la méthodologie d'autoresearch de Karpathy pour optimiser tout contenu textuel — skills OpenClaw, prompts ou articles — par des tests de mutation itératifs.

### Trois modes d'optimisation

| Mode | Quand l'utiliser | Entrée |
|------|------------------|--------|
| **Skill** | "optimize merge-drafts" | SKILL.md d'un skill |
| **Prompt** | "optimize this prompt" | Texte de prompt quelconque |
| **Article** | "polish this article" | Document/texte quelconque |

### Comment ça fonctionne

```
Pour chaque tour (jusqu'à 100):
  1. Faites UNE petite modification sur le contenu cible
  2. Évaluez le résultat avec une liste de vérification (10 critères)
  3. Score augmenté ? → Gardez la modification
  4. Score baissé ? → Revenez à la version précédente
  5. Toutes les 30 rounds → pause pour révision humaine
```

Vous définissez **ce que "bon" signifie** via des questions de checklist. L'agent gère le reste.

### Installation

```bash
# Via ClawHub (recommandé)
clawhub install autoresearch-pro

# Manuelle
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

### Utilisation

```
optimize merge-drafts
autoresearch feishu-calendar
optimize this prompt: [collez votre prompt]
polish this article: [collez l'article]
```

### Stratégies de mutation

Une petite modification par tour : ajouter une règle de contrainte, renforcer les déclencheurs, ajouter des exemples, préciser le langage vague, améliorer la gestion des erreurs, supprimer les redondances, améliorer les transitions.

**Une mutation par tour** — les petits changements sont vérifiables ; les réécritures complètes ne le sont pas.

### Crédits

- **[Karpathy/autoresearch](https://github.com/karpathy/autoresearch)** — l'idée originale

### Licence

MIT
