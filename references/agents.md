# Viral Launch Agent Roles

这些是角色，不是必须全部并行的 subagents。主 agent 负责调度、汇总和最终判断。

## Execution Shape

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

## Role Map

| # | Role | Owner | Purpose |
|---|------|-------|---------|
| 1 | Brand Brief | Main | 把用户输入变成可执行 brief |
| 2 | Keywords | Main | 拆研究关键词 |
| 3 | YouTube Research | Research subagent | 找视频 outliers、标题、评论和 demo 叙事 |
| 4 | X/Twitter Research | Research subagent | 找同类 launch、爆款开头、评论语言 |
| 5 | Reddit Research | Research subagent | 找真实抱怨、痛点和反感词 |
| 6 | Industry Research | Research subagent | 找行业趋势、品类陈词滥调、时机 |
| 7 | Research Compiler | Main | 压缩研究，只保留影响定位的证据 |
| 8 | Hook Writer | Main | 基于 bold claim 批量写 hook |
| 9 | Hook Manager | Main | 淘汰弱 hook，明确重写方向 |
| 10 | Giveaway Writer | Main | 设计评论、领取、waitlist、demo call 诱因 |
| 11 | Giveaway Manager | Main | 审核 giveaway 是否服务转化目标 |
| 12 | Body Writer | Main | 写 demo-driven body |
| 13 | Weapons Specialist | Review subagent | 检查 invention novelty 和 copy intensity |
| 14 | Controversy Specialist | Review subagent | 找反共识和共同敌人 |
| 15 | Technical Specialist | Review subagent | 检查技术事实和 claim 边界 |
| 16 | Flow Specialist | Review subagent | 检查叙事顺序和展示逻辑 |
| 17 | Body Manager | Main | 汇总 body feedback 并重写 |
| 18 | Mom Test | Review subagent | 用非技术读者视角检查可理解性 |
| 19 | Call Supervisor | Review subagent | 检查 CTA、转化路径、评论诱因 |
| 20 | Final Review | Main | 最终复审，不再引入新方向 |
| 21 | Deliver | Main | 交付 final script 和 paper trail |

## Research Subagent Contract

每个 research subagent 必须返回同一结构：

```markdown
# <Research Area> Memo

## Scope
- Query / URLs used:
- Tools used:
- Time window:

## Strongest Findings
- ...

## Exact Audience Language
| Quote / Phrase | Source | Why it matters |
|----------------|--------|----------------|

## Viral / High-Response Patterns
| Pattern | Example | Reusable lesson |
|---------|---------|-----------------|

## Competitor Cliches
- ...

## Anti-Positioning Opportunities
- ...

## Evidence Links
- [title](url)

## Recommended Launch Angles
- ...
```

不能做：

- 不要写最终文案。
- 不要把搜索结果列表当研究结论。
- 不要引用没有来源的具体事实。
- 不要为了支持产品强行解释证据。

## Review Subagent Contract

每个 review subagent 必须返回：

```markdown
# <Review Area> Review

## Verdict
Pass / Needs Rewrite / Reject

## Highest Priority Fixes
- ...

## Line-Level Notes
| Line / Section | Problem | Rewrite Direction |
|----------------|---------|-------------------|

## Suggested Rewrites
- ...

## Do Not Change
- ...
```

不能做：

- 不要直接合并最终稿。
- 不要重写成另一个战略方向，除非当前方向明显不成立。
- 不要只说“更有冲击力”，必须指出哪一行弱，为什么弱。

## Role Details

### 1. Brand Brief

Input: 用户原始信息、链接、产品资料。

Output:

- product one-liner
- target audience
- current alternative
- new behavior
- proof assets
- launch goal
- restrictions

Reject if:

- 不知道产品替代什么旧行为。
- 不知道 CTA。
- 不知道用户是谁。

### 2. Keywords

Input: Brand Brief。

Output:

- category keywords
- pain keywords
- competitor keywords
- customer complaint keywords
- anti-positioning keywords
- novelty keywords

Reject if:

- 关键词只有产品自夸词，没有用户抱怨词。

### 3. YouTube Research

Input: keywords、competitors、category。

Look for:

- high-view videos in the category
- titles and thumbnails with strong promises
- comment language
- before/after demo structure
- objections in comments

### 4. X/Twitter Research

Input: keywords、competitors、founder names、category。

Look for:

- viral launches
- successful first lines
- quote tweets and replies
- phrases people repeat
- claims that feel stale

### 5. Reddit Research

Input: pain keywords、category、competitors。

Look for:

- repeated complaints
- phrases with emotional charge
- buyer skepticism
- workaround behavior
- why existing tools are hated

### 6. Industry Research

Input: category、market timing、AI relevance。

Look for:

- recent shifts
- category fatigue
- new enabling technology
- regulation or platform changes
- why now

### 7. Research Compiler

Input: research memos。

Output:

- market wants
- market hates
- stale claims
- fresh claims
- evidence-backed opportunities
- risky claims

Reject if:

- 输出只是摘要，没有转化成定位判断。

### 8. Hook Writer

Input: selected bold claim candidates。

Output:

- 10-20 hooks in standard/deep
- 5 hooks in quick
- grouping by angle

Hooks must answer:

- what is launched
- why it matters
- why it feels new

### 9. Hook Manager

Input: hook list。

Output:

- keep / kill / rewrite table
- top 3 hooks
- rewrite notes

Reject if:

- 第一行可以被任意竞品替换使用。

### 10. Giveaway Writer

Input: launch goal。

Output:

- comment CTA
- waitlist CTA
- demo CTA
- free teardown / template / audit CTA if relevant

### 11. Giveaway Manager

Input: giveaway options。

Output:

- CTA ranking
- friction assessment
- spam risk
- alignment with launch goal

### 12. Body Writer

Input: selected hook、demo assets、proof。

Output:

- body script
- demo sequence
- proof placement
- CTA placement

### 13. Weapons Specialist

Input: draft。

Judge every line by:

- invention novelty
- copy intensity
- specificity
- emotional force
- whether the line earns its place

Kill:

- filler
- generic SaaS phrases
- obvious explanation that should be shown visually

### 14. Controversy Specialist

Input: draft and research compiler。

Find:

- enemy
- category lie
- old-world behavior
- hidden cost
- status quo absurdity

Guardrail:

- 不造冲突，不捏造竞品缺陷。

### 15. Technical Specialist

Input: draft、product facts、docs。

Check:

- claim is technically true
- product can do what script implies
- no overclaim
- no vague benchmark
- no unsupported “first” claim

### 16. Flow Specialist

Input: draft and demo flow。

Check:

- old behavior appears before new behavior
- demo order is understandable
- viewer knows what to look at
- no explanation before visual proof when demo can show it

### 17. Body Manager

Input: body draft + review notes。

Output:

- revised body
- accepted/rejected feedback
- unresolved risk

### 18. Mom Test

Input: draft。

Assume reader:

- non-technical
- short attention
- no category jargon
- only understands concrete actions

Flag:

- undefined acronyms
- abstract nouns
- unclear pronouns
- multi-step logic hidden in one sentence

### 19. Call Supervisor

Input: CTA and launch goal。

Check:

- one clear action
- low friction
- matches audience
- not asking for too much too early
- captures interest from readers who are not ready to buy

### 20. Final Review

Input: final candidate。

Check:

- bold claim still visible
- hook survives
- body proves hook
- CTA matches goal
- no facts without source
- no generic launch language

### 21. Deliver

Output:

- final launch script
- research summary
- bold claim rationale
- rejected versions
- review notes
- human edit checklist
- source links
