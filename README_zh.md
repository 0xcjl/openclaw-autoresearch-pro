# autoresearch-pro

> 通过迭代式突变测试，自动优化 OpenClaw skill、prompt 或文章。
> 灵感来自 [Karpathy/autoresearch](https://github.com/karpathy/autoresearch)。

**autoresearch-pro** 将 Karpathy 的 autoresearch 方法应用于优化任何基于文本的内容 — OpenClaw skill、prompt 或文章 — 通过系统性突变测试提升质量。

## 三种优化模式

| 模式 | 使用场景 | 输入 |
|------|----------|------|
| **Skill** | "优化 merge-drafts" | 技能的 SKILL.md |
| **Prompt** | "优化这个 prompt" | 任意 prompt 文本 |
| **Article** | "润色这篇文章" | 任意文章/文档 |

## 原理

```
每轮（最多100轮）：
  1. 对目标内容做一个小改动
  2. 用 checklist（10个维度）给结果打分
  3. 分数提升？→ 保留改动
  4. 分数下降？→ 撤销改动
  5. 每 30 轮 → 暂停等待人工确认
```

你只需要定义"好"的标准，其余全部自动完成。

## 安装

### 方式一：通过 ClawHub 安装（推荐）

```bash
clawhub install autoresearch-pro
```

### 方式二：手动安装

```bash
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

## 使用方法

**Skill 模式：**
```
优化 merge-drafts
autoresearch feishu-calendar
改进我的 feishu-task skill
```

**Prompt 模式：**
```
优化这个 prompt：[粘贴你的 prompt]
改进我的 prompt
```

**Article 模式：**
```
润色这篇文章：[粘贴文章内容]
改进这篇文章
```

Agent 会自动：
1. 读取目标内容，生成 10 个 checklist 问题
2. 你选择启用哪些标准（默认全部启用）
3. 运行循环 — 30 轮后暂停确认
4. 最多跑满 100 轮
5. 输出最终改进报告

## Checklist 维度

**Skill 模式：**

| # | 维度 |
|---|------|
| 1 | Description 清晰度和可操作性 |
| 2 | 触发词覆盖真实使用场景 |
| 3 | 工作流步骤清晰、无歧义 |
| 4 | 错误处理完整性 |
| 5 | OpenClaw 工具使用准确性 |
| 6 | 示例质量和真实性 |
| 7 | 内容简洁性（无冗余） |
| 8 | 自由度校准（约束/灵活性平衡） |
| 9 | 参考质量准确性 |
| 10 | 各 section 实质内容完整性 |

**Prompt 模式：**

| # | 维度 |
|---|------|
| 1 | 目标清晰度和具体性 |
| 2 | 角色/语气说明 |
| 3 | 输入格式描述 |
| 4 | 输出格式说明 |
| 5 | 约束边界定义 |
| 6 | 上下文充分性（避免幻觉） |
| 7 | 边缘情况处理 |
| 8 | 简洁性（无矛盾指令） |
| 9 | 可操作性（具体 vs 模糊） |
| 10 | 必要元素完整性 |

**Article 模式：**

| # | 维度 |
|---|------|
| 1 | 标题清晰度和价值主张 |
| 2 | 开篇吸引力 |
| 3 | 逻辑结构 |
| 4 | 论点有证据/推理支撑 |
| 5 | 简洁性（无冗余填充） |
| 6 | 段落过渡流畅 |
| 7 | 结尾总结力度 |
| 8 | 语气一致性 |
| 9 | 可读性（句式变化） |
| 10 | 目标读者匹配度 |

## 突变策略

每轮只做一个小的精准改动：

- 添加约束规则（`必须` / `禁止`）
- 强化触发词描述
- 为模糊步骤添加具体示例
- 精化模糊措辞（"尝试" → "必须"）
- 完善错误/边缘情况处理
- 删除冗余内容
- 改善段落过渡
- 扩充薄弱章节
- 添加跨章节交叉引用
- 调整约束/灵活性比例

**每轮只改一处** — 小改动可验证，大改写无法评估。

## 项目结构

```
autoresearch-pro/
├── SKILL.md                           # 主 skill 文件
├── scripts/
│   └── run_eval.py                    # 评估辅助脚本
└── references/
    └── mutation_strategies.md         # 突变策略参考
```

## 实际效果

用这个 skill 优化 `merge-drafts` skill（30轮）：
- Description 触发词：6 → 15 个变体
- 错误处理场景：4 → 13 种
- 约束规则：0 → 10 条强制规则
- 所有模糊措辞精确化
- 步骤间依赖全部打通

## 致谢

- **[Karpathy/autoresearch](https://github.com/karpathy/autoresearch)** — 原始想法和方法论
- 核心思想：让 agent 在循环中自动改进代码/prompt

## License

MIT
