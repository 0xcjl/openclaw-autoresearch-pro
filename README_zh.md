# autoresearch-pro

> 通过迭代式突变测试，自动优化 OpenClaw skill。
> 灵感来自 [Karpathy/autoresearch](https://github.com/karpathy/autoresearch)。

**autoresearch-pro** 是一个 OpenClaw skill，将 Karpathy 的 autoresearch 方法应用于优化其他 OpenClaw skill——通过系统性的突变测试来改进 prompt、用词、约束规则、示例和工具描述。

## 原理

核心循环：

```
每轮（最多100轮）：
  1. 对目标 skill 的 SKILL.md 做一个小改动
  2. 用 checklist（10个维度）给结果打分
  3. 分数提升？→ 保留改动
  4. 分数下降？→ 撤销改动
  5. 每 30 轮 → 暂停等待人工确认
```

你只需要定义"好"的标准（通过 checklist 问题），其余全部自动完成。

## 安装

### 方式一：通过 ClawHub 安装（推荐）

```bash
clawhub install autoresearch-pro
```

### 方式二：手动安装

```bash
# 克隆到 OpenClaw skills 目录
git clone https://github.com/0xcjl/openclaw-autoresearch-pro.git ~/.openclaw/skills/autoresearch-pro
```

## 使用方法

触发 skill：

```
优化 [skill名称]
autoresearch [skill名称]
改进我的 [skill名称]
```

例如：

```
优化 merge-drafts
autoresearch feishu-calendar
```

Agent 会自动：
1. 读取目标 skill 的 `SKILL.md`
2. 生成 10 个 checklist 问题（你来选择启用哪些）
3. 运行 autoresearch 循环 — 30 轮后暂停确认
4. 最多跑满 100 轮
5. 输出最终改进报告

## Checklist 维度

| # | 维度 | 说明 |
|---|------|------|
| 1 | Description 清晰度 | description 是否准确、可操作？ |
| 2 | 触发覆盖率 | 是否覆盖用户真实使用场景？ |
| 3 | 工作流结构 | 步骤是否清晰、无歧义？ |
| 4 | 错误处理 | 是否覆盖主要错误场景？ |
| 5 | 工具使用准确性 | 工具名称、参数是否正确？ |
| 6 | 示例质量 | 示例是否真实反映使用场景？ |
| 7 | 简洁性 | 内容是否冗余？ |
| 8 | 自由度校准 | 约束/灵活性比例是否恰当？ |
| 9 | 参考质量 | 外部参考是否准确有用？ |
| 10 | 完整性 | 各 section 是否有实质内容？ |

## 突变策略

每轮做一个小改动：

- 添加约束规则（`必须` / `禁止`）
- 强化触发词描述
- 为模糊步骤添加具体示例
- 精化模糊措辞（"尝试" → "必须"）
- 完善错误处理
- 删除冗余内容
- 添加跨章节交叉引用
- 扩充薄弱章节
- 改善章节过渡

**每轮只改一处** — 小改动可验证，大改写无法评估。

## 项目结构

```
autoresearch-pro/
├── SKILL.md                           # 主 skill 文件（加载到 OpenClaw）
├── scripts/
│   └── run_eval.py                    # 可选评估辅助脚本
└── references/
    └── mutation_strategies.md         # 突变策略参考
```

## 实际效果

用这个 skill 优化 `merge-drafts` skill（多稿合并工具）的结果：
- Description 触发词：6 → 15 个变体
- 错误处理场景：4 → 13 种
- 约束规则：0 → 10 条强制规则
- 所有模糊措辞精确化
- 步骤间依赖全部打通

## 致谢

- **Karpathy/autoresearch** — 原始想法：[github.com/karpathy/autoresearch](https://github.com/karpathy/autoresearch)
- 方法论源自 Karpathy 的博文：让 agent 在循环中自动改进代码

## License

MIT
