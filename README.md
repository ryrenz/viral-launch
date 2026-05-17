# Viral Launch Skill

A research-first agent skill for turning a product into a high-conviction launch narrative.

Most launch copy fails because it starts with writing: “Excited to announce…”, a generic feature list, a vague AI promise, and a weak CTA. Viral Launch forces the agent to slow down first: understand the product, research the market, find a bold claim, stress-test the hook, prove the demo story, and only then write the final launch script.

It is designed for AI products, SaaS, developer tools, Product Hunt launches, X/Twitter launch posts, demo scripts, founder announcements, waitlist launches, and any product that needs a sharper public narrative.

## What it does

Viral Launch turns a product launch into a repeatable operating system:

1. Brand Brief — clarify the product, audience, proof, constraints, and conversion goal.
2. Research Plan — identify industry context, customer pain, competitors, stale claims, and audience language.
3. Parallel Research — optionally split YouTube, X/Twitter, Reddit, industry, and competitor research into focused agent tasks.
4. Bold Claim Candidates — generate and score multiple launch positions before choosing one.
5. Hook Iteration — write, kill, and rewrite hooks instead of accepting the first decent line.
6. Demo-Driven Body — show the old behavior, product action, new behavior, proof, and CTA.
7. Weapons Check — remove generic SaaS language and lines that do not earn attention.
8. Technical Check — prevent unsupported claims, fake “first” language, and overpromising.
9. Mom Test — make sure a non-technical reader can understand the launch.
10. Final Delivery — output the final script plus the reasoning trail, rejected versions, review notes, and source links.

The goal is not to make every launch louder. The goal is to make every sentence defensible.

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

## Quick start

### 1. Install the skill

Copy or symlink this repository into your agent's skills directory.

For Hermes Agent:

```bash
mkdir -p ~/.hermes/skills
ln -s /path/to/viral-launch ~/.hermes/skills/viral-launch
```

For Claude Code:

```bash
mkdir -p ~/.claude/skills
ln -s /path/to/viral-launch ~/.claude/skills/viral-launch
```

For Codex-style local skills:

```bash
mkdir -p ~/.codex/skills
ln -s /path/to/viral-launch ~/.codex/skills/viral-launch
```

You can also copy the folder instead of symlinking it:

```bash
cp -R /path/to/viral-launch ~/.hermes/skills/viral-launch
```

### 2. Ask your agent to use it

Example prompts:

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

### 3. Choose a mode

| Mode | Best for | Output depth |
|------|----------|--------------|
| `quick` | You need a solid first version fast | Light research, at least 3 bold claims, 5 hooks, one reviewed script |
| `standard` | Most launches | 3-5 sources, 5-10 bold claims, hook/body critique, final delivery |
| `deep` | Major launches or high-stakes announcements | Multi-platform research, full paper trail, stronger review loop |

If you do not specify a mode, the skill defaults to `standard`.

## Example output

A good run should produce something like:

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

The final script is only one part of the output. The rejected versions and review notes are part of the value: they show why the final angle survived.

## What makes it different

Viral Launch is opinionated about launch writing:

- Do not start with “Excited to announce.”
- Do not write a generic feature list.
- Do not use “AI-powered”, “seamless”, “streamline”, or “powerful” unless the line shows a concrete user action.
- Do not claim “first”, “only”, “autonomous”, “real-time”, or “production-ready” without proof.
- Do not average research findings. Keep only the evidence that changes positioning.
- Do not let a hook survive if any competitor could swap in its name and use the same line.

## Best use cases

- X/Twitter launch posts and threads
- Product Hunt launch copy
- AI SaaS announcements
- Developer tool launches
- Waitlist launch campaigns
- Demo video scripts
- Founder announcements
- Repositioning an existing product for a sharper launch

## Inputs that help

The skill works best when you provide:

- Product name and one-liner
- Website, demo, screenshots, or docs
- Target audience
- Launch goal
- Competitors or alternatives
- Proof: users, benchmarks, screenshots, testimonials, case studies
- Constraints: claims you cannot make, compliance boundaries, roadmap limitations
- Target channel and language

If key information is missing, the skill should ask at most three questions, then proceed with explicit assumptions.

## Notes on tools

The skill can use whatever research tools your agent environment provides. The included `references/research-sources.md` mentions common options such as web search, Tavily, XCrawl, YouTube transcripts, X/Twitter scraping, Reddit search, GitHub, and local knowledge bases. These are routing suggestions, not hard dependencies.

If your environment does not support subagents, run the same roles sequentially in one agent.

## License

MIT License. See [LICENSE](LICENSE).

## Chinese documentation

中文说明见 [README.zh-CN.md](README.zh-CN.md).
