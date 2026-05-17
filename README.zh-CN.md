# Viral Launch Skill

一个“先研究、再定位、最后写发布文案”的 agent skill，用来把产品变成更有传播力、更有证据链的 launch narrative。

默认 README 是中文优先的中英文双语版本：见 [README.md](README.md)。

大多数 launch 文案失败，不是因为句子不够华丽，而是因为一上来就写：`Excited to announce...`、泛泛的功能列表、模糊的 AI 承诺、软弱的 CTA。Viral Launch 会强制 agent 先理解产品、研究市场、找到 bold claim、审查 hook、证明 demo 叙事，最后才写最终稿。

它适合 AI 产品、SaaS、开发者工具、Product Hunt 发布、X/Twitter launch post、demo script、founder announcement、waitlist launch，以及任何需要更锐利公开叙事的产品。

## 功能介绍

Viral Launch 把产品发布拆成一套可复用工作流：

1. Brand Brief：明确产品、用户、证据、限制和转化目标。
2. Research Plan：确定行业语境、用户痛点、竞品、陈词滥调和目标用户语言。
3. Parallel Research：按需把 YouTube、X/Twitter、Reddit、行业、竞品研究拆给多个 agent。
4. Bold Claim Candidates：先生成多个定位候选并打分，而不是直接写最终稿。
5. Hook Iteration：批量写 hook、淘汰弱 hook、重写，而不是接受第一句“还行”的开头。
6. Demo-Driven Body：展示旧行为、产品动作、新行为、证据和 CTA。
7. Weapons Check：删除泛 SaaS 词和没有承担功能的句子。
8. Technical Check：防止无证据的 “first / only / autonomous / real-time” 等过度 claim。
9. Mom Test：确保非技术用户也能理解。
10. Final Delivery：交付最终稿、研究摘要、被淘汰版本、审查记录和来源链接。

目标不是让每次发布都更吵，而是让每一句话都能解释为什么留下。

## 仓库结构

```text
viral-launch/
├── SKILL.md
├── references/
│   ├── agents.md
│   ├── research-sources.md
│   └── scorecards.md
├── templates/
│   ├── brand-brief.md
│   ├── research-report.md
│   └── launch-delivery.md
├── evals/
│   └── evals.json
├── README.md
├── README.zh-CN.md
└── LICENSE
```

## Quick Start

### 1. 安装 skill

把本仓库 clone 到你的 agent skills 目录。

Hermes Agent：

```bash
mkdir -p ~/.hermes/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.hermes/skills/viral-launch
```

Claude Code：

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.claude/skills/viral-launch
```

Codex 风格本地 skills：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.codex/skills/viral-launch
```

如果你想同时维护源码和多个 agent 入口，可以用软链接：

```bash
git clone https://github.com/ryrenz/viral-launch.git ~/skills/viral-launch
ln -s ~/skills/viral-launch ~/.claude/skills/viral-launch
ln -s ~/skills/viral-launch ~/.codex/skills/viral-launch
ln -s ~/skills/viral-launch ~/.hermes/skills/viral-launch
```

### 2. 让 agent 使用它

示例 prompt：

```text
Use viral-launch for this product: an AI code review tool that reads a pull request, explains the risk, and suggests the safest merge plan.
Target channel: X.
Goal: waitlist signups.
Mode: standard.
```

```text
Run viral-launch in quick mode for our Product Hunt launch.
Product: a browser extension that turns any YouTube video into a structured study guide.
Goal: upvotes and installs.
```

```text
Use viral-launch deep mode.
Here is our website, demo video, competitor list, and launch goal.
I want the research summary, bold claim candidates, rejected hooks, and final X thread.
```

### 3. 选择模式

| Mode | 适合场景 | 输出深度 |
|------|----------|----------|
| `quick` | 需要快速拿到第一版 | 轻量研究、至少 3 个 bold claims、5 个 hooks、一版审查后文案 |
| `standard` | 大多数产品发布 | 3-5 个来源、5-10 个 bold claims、hook/body critique、最终交付 |
| `deep` | 重大发布或高风险 announcement | 多平台研究、完整 paper trail、更强审查循环 |

如果没有指定模式，默认使用 `standard`。

## 典型输出

一次完整运行应该产出：

```text
Brand Brief
Research Summary
Bold Claim Candidates
Selected Claim
Hook Iterations
Rejected Versions
Review Notes
Final Launch Script
Human 5% Edit Notes
Source Links
```

最终稿只是交付的一部分。被淘汰版本和审查记录同样重要，因为它们说明为什么最终角度能留下。

## 它和普通 launch prompt 的区别

Viral Launch 对发布文案有明确偏见：

- 不要以 `Excited to announce` 开头。
- 不要写泛泛的功能列表。
- 不要用 `AI-powered`、`seamless`、`streamline`、`powerful` 这种没有具体动作的词。
- 不要在没有证据时说 `first`、`only`、`autonomous`、`real-time`、`production-ready`。
- 不要平均研究资料；只保留会改变定位的证据。
- 如果某个 hook 换成任意竞品名字也能用，就淘汰。

## 最适合的场景

- X/Twitter launch posts 和 threads
- Product Hunt 发布文案
- AI SaaS announcement
- 开发者工具发布
- Waitlist launch campaign
- Demo video script
- Founder announcement
- 给旧产品重新定位并再次发布

## 最好提供哪些输入

- 产品名和一句话介绍
- 官网、demo、截图或 docs
- 目标用户
- 发布目标
- 竞品或替代方案
- 证据：用户、benchmark、截图、testimonial、case study
- 限制：不能说什么、合规边界、路线图限制
- 目标渠道和语言

如果缺少关键信息，skill 应该最多问 3 个问题；能继续时就带着显式假设推进。

## 工具说明

这个 skill 可以使用当前 agent 环境里已有的研究工具。`references/research-sources.md` 里提到的 web search、Tavily、XCrawl、YouTube transcript、X/Twitter scraping、Reddit search、GitHub 和本地知识库，都是工具路由建议，不是硬依赖。

如果你的环境没有 subagent 能力，就在同一个 agent 内按角色顺序串行执行。

## License

MIT License. See [LICENSE](LICENSE).
