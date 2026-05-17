# Viral Launch：产品发布定位与爆款 Launch 工作流

> 中文优先。English version below.

Viral Launch 是一个面向 Claude Code、Codex、Hermes 等 agent 环境的 Skill，用来把“写一条发布文案”升级成一套完整的 launch 操作系统。

它不会让 agent 一上来直接写文案，而是强制先完成研究、定位、bold claim、hook、demo 叙事、逐句审查和最终交付。

普通 prompt 产出句子。
Viral Launch 产出判断。

## 它适合什么

- X / Twitter 产品发布帖和 thread
- Product Hunt launch copy
- SaaS / AI 产品发布文案
- Demo script 和发布视频脚本
- Founder announcement
- Waitlist、内测、公测、融资公告
- 给旧产品重新定位，再做一次更清楚的发布

## 它最终输出什么

标准模式会输出一整包 launch dossier：

```text
1. Brand Brief
2. Research Summary
3. Bold Claim Candidates
4. Selected Claim
5. Hook Iterations
6. Rejected Versions
7. Demo Flow
8. Review Notes
9. Final Launch Script
10. Human 5% Edit Notes
11. Source Links
```

最终交付不是一条孤零零的文案，而是：

**一条可发布的 launch script，加上一套解释它为什么这样写的研究和审查记录。**

## 核心工作流

1. **选择模式**：根据任务自动选择 `quick`、`standard` 或 `deep`。
2. **Brand Brief**：整理产品、目标用户、发布目标、证据和限制。
3. **Keyword Builder**：拆出品类词、痛点词、竞品词、用户抱怨词和反定位词。
4. **Parallel Research**：并行研究 YouTube、X、Reddit、行业和竞品。
5. **Research Compiler**：提炼市场想要什么、讨厌什么、已经看腻什么。
6. **Bold Claim Candidates**：生成 5-10 个发布主张，找最值得停下来的那句话。
7. **Hook Writer / Manager**：批量写 hook，再淘汰泛化、礼貌、无差异的开头。
8. **Body Writer**：用旧状态、新动作、新结果和证据证明 claim。
9. **Parallel Review**：跑 Weapons Check、Controversy Check、Technical Check、Flow Check、Mom Test、CTA Check。
10. **Final Rewrite**：由主 agent 汇总审查意见，重新写成统一口径。
11. **Deliver**：交付最终稿、研究摘要、淘汰版本、审查记录和来源链接。

## 三种模式

| 模式 | 适合场景 | 研究深度 | Subagents |
|---|---|---|---|
| `quick` | 快速拿第一版 | 轻量研究或已有资料 | 不开 subagent |
| `standard` | 默认发布任务 | 3-5 个来源 | 研究和审查阶段少量并行 |
| `deep` | 重大产品发布 | 多平台研究和完整 paper trail | 研究和审查阶段多路并行 |

如果没有指定模式，默认使用 `standard`。

## 为什么不是 21 个 agent 全开

原始灵感来自“21 个 specialized agents”的 launch 系统，但本 Skill 不会机械地开 21 个 subagents。

正确结构是：

```text
Main Agent
├── Research Subagents
│   ├── YouTube Research
│   ├── X Research
│   ├── Reddit Research
│   ├── Industry Research
│   └── Competitor / Customer Language Research
├── Main Agent: Research Compiler + Bold Claim
├── Main Agent: Hook + Body Draft
├── Review Subagents
│   ├── Weapons Check
│   ├── Controversy Check
│   ├── Technical Check
│   ├── Flow Check
│   ├── Mom Test
│   └── CTA Check
└── Main Agent: Final Rewrite + Deliver
```

研究和审查可以并行。定位、主张、最终重写必须留在主 agent 手里，否则文案会散。

## 安装

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.claude/skills/viral-launch
```

### Codex

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.codex/skills/viral-launch
```

### Hermes Agent

```bash
mkdir -p ~/.hermes/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.hermes/skills/viral-launch
```

### 本地开发

如果你想同时维护源码和多个 agent 入口，可以用软链接：

```bash
git clone https://github.com/ryrenz/viral-launch.git ~/skills/viral-launch
ln -s ~/skills/viral-launch ~/.claude/skills/viral-launch
ln -s ~/skills/viral-launch ~/.codex/skills/viral-launch
ln -s ~/skills/viral-launch ~/.hermes/skills/viral-launch
```

## 使用示例

```text
$viral-launch
我们要发布一个 AI 工具，可以把 founder 的 Loom demo 自动改成 X launch script 和产品发布视频。帮我找 launch angle，并写最终发布帖。
```

```text
$viral-launch
给一个开发者工具写 Product Hunt launch。它能把 GitHub issues 自动整理成产品 roadmap。
```

```text
$viral-launch deep
我们要发布一个 B2B AI sales copilot。请做 Reddit、X、YouTube、竞品研究，并给完整 demo narrative。
```

## 最好提供哪些输入

- 产品名和一句话介绍
- 官网、demo、截图或文档
- 目标用户
- 发布目标
- 竞品或替代方案
- 证据：用户、benchmark、截图、testimonial、case study
- 限制：不能说什么、合规边界、路线图限制
- 目标渠道和语言

如果缺少关键信息，Skill 应该最多问 3 个问题；能继续时就带着显式假设推进。

## 文件结构

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

## 工具说明

这个 Skill 可以使用当前 agent 环境里的研究工具。`references/research-sources.md` 里提到的 web search、Tavily、XCrawl、YouTube transcript、X/Twitter scraping、Reddit search、GitHub 和本地知识库，都是工具路由建议，不是硬依赖。

如果你的环境没有 subagent 能力，就在同一个 agent 内按角色顺序串行执行。

## 设计原则

- 不要先写，先研究。
- 不要追求漂亮，先找停留理由。
- 不要平均所有资料，只保留能改变定位的证据。
- 不要把 AI 当 writer，要把它当 launch operator。
- 不要让 claim 超过产品事实。
- 不要只交付最终稿，要保留 paper trail。

## 注意事项

这个 Skill 不保证 viral。没有任何系统能保证 viral。

它真正提升的是 launch 的基本质量：研究更深、定位更准、hook 更尖、废话更少、技术 claim 更安全、最终稿更像一个经过审查的发布资产，而不是一条随手生成的 AI 文案。

## License

MIT License. See [LICENSE](LICENSE).

---

# Viral Launch: Product Launch Positioning and High-Conviction Launch Workflow

Viral Launch is a Skill for Claude Code, Codex, Hermes, and similar agent environments. It turns launch writing into a structured operating system: research, positioning, bold claim extraction, hook writing, demo narrative, line-level review, and final delivery.

It does not ask the agent to “just write a launch post.” It forces the agent to understand why anyone should stop scrolling before writing the final script.

Regular prompts produce copy.
Viral Launch produces judgment.

## What it is for

- X / Twitter product launch posts and threads
- Product Hunt launch copy
- SaaS and AI product announcements
- Demo scripts and launch video narratives
- Founder announcements
- Waitlist, beta, public launch, or funding announcement angles
- Repositioning an existing product for a sharper public launch

## What it outputs

In standard mode, the Skill produces a complete launch dossier:

```text
1. Brand Brief
2. Research Summary
3. Bold Claim Candidates
4. Selected Claim
5. Hook Iterations
6. Rejected Versions
7. Demo Flow
8. Review Notes
9. Final Launch Script
10. Human 5% Edit Notes
11. Source Links
```

The final deliverable is not just a launch post. It is a publishable launch script plus the research and critique trail that explains why the script is shaped that way.

## Workflow

1. **Mode selection**: choose `quick`, `standard`, or `deep`.
2. **Brand Brief**: capture the product, audience, goal, proof, and constraints.
3. **Keyword Builder**: build category, pain, competitor, complaint, and anti-positioning keywords.
4. **Parallel Research**: research YouTube, X, Reddit, industry context, and competitors.
5. **Research Compiler**: extract what the market wants, hates, and has already seen too many times.
6. **Bold Claim Candidates**: create 5-10 launch claims and find the strongest one.
7. **Hook Writer / Manager**: write hooks, then kill generic or polite openings.
8. **Body Writer**: prove the claim through old behavior, product action, new behavior, and proof.
9. **Parallel Review**: run Weapons Check, Controversy Check, Technical Check, Flow Check, Mom Test, and CTA Check.
10. **Final Rewrite**: the main agent rewrites the draft into one coherent final version.
11. **Deliver**: provide the final script, source links, rejected versions, and review notes.

## Modes

| Mode | Best for | Research depth | Subagents |
|---|---|---|---|
| `quick` | A fast first version | Light research or existing material | None |
| `standard` | Default launch work | 3-5 sources | Some parallel research and review |
| `deep` | Major launches | Multi-platform research and full paper trail | More parallel research and review |

If no mode is specified, the Skill defaults to `standard`.

## Why not 21 agents at once

The inspiration comes from a launch system with many specialized roles. This Skill treats those roles as workflow checkpoints, not as 21 agents that should all run in parallel.

The recommended structure is:

```text
Main Agent
├── Research Subagents
│   ├── YouTube Research
│   ├── X Research
│   ├── Reddit Research
│   ├── Industry Research
│   └── Competitor / Customer Language Research
├── Main Agent: Research Compiler + Bold Claim
├── Main Agent: Hook + Body Draft
├── Review Subagents
│   ├── Weapons Check
│   ├── Controversy Check
│   ├── Technical Check
│   ├── Flow Check
│   ├── Mom Test
│   └── CTA Check
└── Main Agent: Final Rewrite + Deliver
```

Research and review can run in parallel. Positioning, the selected claim, and final rewrite should stay with the main agent.

## Installation

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.claude/skills/viral-launch
```

### Codex

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.codex/skills/viral-launch
```

### Hermes Agent

```bash
mkdir -p ~/.hermes/skills
git clone https://github.com/ryrenz/viral-launch.git ~/.hermes/skills/viral-launch
```

### Local development

If you want one source checkout and multiple agent entry points, symlink the repo:

```bash
git clone https://github.com/ryrenz/viral-launch.git ~/skills/viral-launch
ln -s ~/skills/viral-launch ~/.claude/skills/viral-launch
ln -s ~/skills/viral-launch ~/.codex/skills/viral-launch
ln -s ~/skills/viral-launch ~/.hermes/skills/viral-launch
```

## Examples

```text
$viral-launch
We are launching an AI tool that turns a founder's Loom demo into an X launch script and launch video. Find the launch angle and write the final post.
```

```text
$viral-launch
Write Product Hunt launch copy for a developer tool that turns GitHub issues into a product roadmap.
```

```text
$viral-launch deep
We are launching a B2B AI sales copilot. Research Reddit, X, YouTube, and competitors, then give me the complete demo narrative.
```

## Helpful inputs

- Product name and one-liner
- Website, demo, screenshots, or docs
- Target audience
- Launch goal
- Competitors or alternatives
- Proof: users, benchmarks, screenshots, testimonials, case studies
- Constraints: claims you cannot make, compliance boundaries, roadmap limitations
- Target channel and language

If key information is missing, the Skill should ask at most three questions, then proceed with explicit assumptions when possible.

## Repository structure

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

## Notes on tools

The Skill can use whatever research tools your agent environment provides. The included `references/research-sources.md` mentions common options such as web search, Tavily, XCrawl, YouTube transcripts, X/Twitter scraping, Reddit search, GitHub, and local knowledge bases. These are routing suggestions, not hard dependencies.

If your environment does not support subagents, run the same roles sequentially in one agent.

## Design principles

- Research before writing.
- Find the reason to stop scrolling before polishing the prose.
- Keep only evidence that changes positioning.
- Treat the AI as a launch operator, not just a writer.
- Never let a claim outrun product facts.
- Deliver the paper trail, not only the final script.

## Notes

This Skill does not guarantee virality. No launch system can guarantee that.

What it improves is the baseline quality of the launch: deeper research, sharper positioning, stronger hooks, fewer filler lines, safer technical claims, and a final script that feels reviewed instead of generated.

## License

MIT License. See [LICENSE](LICENSE).
