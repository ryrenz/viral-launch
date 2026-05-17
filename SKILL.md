---
name: viral-launch
description: Build high-conviction launch positioning, X/Twitter launch posts, Product Hunt launches, demo scripts, SaaS launch copy, and viral product announcement narratives. Use this skill whenever the user asks for a product launch, viral launch, launch script, launch thread, demo launch, Product Hunt copy, founder announcement, waitlist launch, AI product launch, or asks to turn a product into a launch narrative. This skill should trigger even when the user only says they are launching something and wants the angle, hook, positioning, or script.
---

# Viral Launch

把产品发布从“写一条文案”改成“研究、定位、bold claim、hook、demo 叙事、审查、交付”的完整工作流。不要把自己当 writer；把自己当 launch operator。

## Core Rule

不要直接写最终稿。先建立研究和定位，再写文案。

每次输出都围绕一个问题：**为什么这个东西现在值得别人停下来？**

## Operating Modes

根据用户语义选择模式。用户没有指定时默认 `standard`。

| Mode | Use When | Research Depth | Subagents |
|------|----------|----------------|-----------|
| `quick` | 用户说快速版、MVP、不深挖、只要一版 | 轻量搜索或已有资料 | 不开 subagent，主 agent 串行完成 |
| `standard` | 默认模式 | 3-5 个来源，覆盖行业、竞品、用户语言 | 研究阶段 3-5 个并行 subagents；审查阶段 2-4 个并行 subagents |
| `deep` | 用户要完整 launch、重大产品发布、希望深挖市场 | 多平台研究，保留完整 paper trail | 研究阶段 4-6 个并行 subagents；审查阶段 4-6 个并行 subagents |

如果当前平台没有 subagent 能力，就在主 agent 内按同样角色顺序执行，不要省略检查。

## Inputs

先收集够用信息，不要为了完美信息卡住。缺少关键输入时，最多问 3 个问题；如果能从链接或资料里查到，就自己查。

优先收集：

- Product: 产品名、官网、demo、核心功能、目标用户。
- Launch goal: 浏览、waitlist、demo call、Product Hunt、融资 announcement、用户注册。
- Audience: 面向 founders、developers、marketers、consumers、enterprise buyers 还是 mass market。
- Proof: 已有用户、数据、案例、截图、demo flow、benchmark。
- Constraints: 不能说什么、合规限制、技术能力边界、目标语言和渠道。

用 `templates/brand-brief.md` 记录输入。

## Workflow

### 1. Brand Brief

把用户输入整理成 brief。必须明确：

- 这是什么产品。
- 它替代了什么旧行为。
- 它让用户第一次能做什么。
- 它不应该被说成什么泛化品类。
- launch 成功的转化动作是什么。

### 2. Keyword Builder

从 brief 中拆出关键词：

- category keywords
- pain keywords
- competitor keywords
- customer complaint keywords
- anti-positioning keywords
- novelty keywords

### 3. Parallel Research

`standard` 和 `deep` 模式优先并行派 subagents。不要把 manager/compiler 派出去；主 agent 保持最终判断权。

推荐结构：

```text
Main Agent
├── YouTube Research
├── X Research
├── Reddit Research
├── Industry Research
└── Competitor / Customer Language Research
```

每个 research subagent 只交付 memo，不写最终文案。memo 必须包含：

- strongest audience pains
- exact customer language
- existing viral patterns
- competitor cliches
- anti-positioning opportunities
- evidence links
- launch angle recommendations

工具路由见 `references/research-sources.md`。

### 4. Research Compiler

主 agent 汇总研究，不要平均每个 subagent 的观点。只保留能改变 positioning 的证据。

输出：

- 市场已经厌倦的说法。
- 用户真实抱怨。
- 最强 pain。
- 可以 counter-position 的敌人。
- 产品真正新的行为。
- 可被证明的 claim。

### 5. Bold Claim Candidates

写 5-10 个 `BOLD CLAIM`。quick 模式至少 3 个。

每个 claim 必须回答：

- What is being launched?
- Why does it matter?
- Why has this never existed before, or why does it feel newly possible now?

用 `references/scorecards.md` 的 `Bold Claim Scorecard` 打分。不要选最高分但无法证明的 claim。

### 6. Hook Writer + Hook Manager

围绕最强 1-2 个 bold claims 写 hooks。

Hook Manager 必须淘汰：

- 泛化 announcement。
- “excited to announce” 式礼貌开场。
- 任何竞品换名字也能用的开头。
- 看完第一句不知道为什么要继续看的开头。

### 7. Body Writer

正文只有一个任务：让 bold claim 变真实。

优先写 demo-driven narrative：

1. Show old behavior.
2. Show product action.
3. Show new behavior.
4. Show why this changes the category.
5. Show proof.
6. Ask for the next action.

### 8. Parallel Review

初稿出来后并行派审查 subagents。每个 reviewer 只做 critique 和 rewrite suggestions，不直接合并最终稿。

推荐结构：

```text
Review Subagents
├── Weapons Check
├── Controversy Check
├── Technical Check
├── Flow Check
├── Mom Test
└── CTA Check
```

必须覆盖：

- `Weapons Check`: invention novelty + copy intensity。
- `Controversy Check`: 是否有反共识、共同敌人或品类骗局，但不能造假。
- `Technical Check`: claim 是否被产品事实支撑。
- `Flow Check`: demo 顺序是否能被跟上，哪里该展示而不是解释。
- `Mom Test`: 非技术用户是否能懂。
- `CTA Check`: 注意力是否转成评论、注册、预约或购买。

评分细则见 `references/scorecards.md`。

### 9. Final Rewrite

主 agent 汇总 review feedback，自己做最终重写。不要拼贴 reviewer 原文。

重写时优先级：

1. 事实准确。
2. Bold claim 清晰。
3. 第一行有停留理由。
4. Demo flow 能看见旧世界和新世界。
5. 每句话都增加 novelty、proof、desire 或 action。
6. 删除 filler。

### 10. Deliver

最终交付不只是一条文案。按 `templates/launch-delivery.md` 输出：

- Brand Brief
- Research Summary
- Bold Claim Candidates
- Selected Claim
- Hook Iterations
- Rejected Versions
- Review Notes
- Final Launch Script
- Human 5% Edit Notes
- Source Links

如果用户要求保存，默认保存到：

```text
drafts/<slug>/viral-launch/
```

如果当前不在内容工作区或用户指定了目录，就按用户目录保存。

## Subagent Policy

只有在用户明确允许或当前任务明显需要并行 agent work 时使用 subagents。使用时遵守：

- 研究 subagents 和审查 subagents 可以并行。
- `Research Compiler`、`Bold Claim`、`Final Rewrite`、`Deliver` 留给主 agent。
- 不要开 21 个 subagents。21 个是角色，不是并行数量。
- 每个 subagent 任务必须有明确输入、输出和边界。
- Research subagents 不写最终文案。
- Review subagents 不改最终稿，只交 critique。

建议并行上限：

- `quick`: 0
- `standard`: 4-7 total
- `deep`: 8-12 total

## Required Reference Loading

按需读取，不要一次性加载所有文件：

- 执行研究前读 `references/research-sources.md`。
- 分派角色或串行模拟角色前读 `references/agents.md`。
- 进入 claim、hook、body、review 前读 `references/scorecards.md`。
- 保存或交付前读对应模板。

## Quality Bar

最终稿不能出现这些问题：

- 第一行只是 announcement，没有差异化。
- 使用 `platform`、`streamline`、`seamless`、`powerful`、`AI-powered` 这类泛词但没有具体动作。
- Claim 听起来大，但产品能力支撑不了。
- 只讲功能，不展示旧行为和新行为的差异。
- 没有真实用户语言。
- 没有 CTA 或 CTA 和 launch 目标不一致。
- 具体事实没有来源。

如果任一问题存在，回到对应步骤重写。
