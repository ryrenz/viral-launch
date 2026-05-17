# Viral Launch Research Sources

目标是找到定位证据，不是堆资料。任何研究都要回答：市场想要什么、讨厌什么、已经看腻什么、这个产品可以怎样显得新。

## Tool Routing

| Source Type | First Choice | Fallback | Use For |
|-------------|--------------|----------|---------|
| AI industry news | `aihot` skill | Tavily Search | AI 产品的行业语境、模型/产品发布、近期趋势 |
| General web search | Tavily Search | XCrawl Search | 发现竞品、文章、Reddit/X/YouTube 结果 |
| Specific web page | XCrawl Scrape | Tavily Extract / baoyu-url-to-markdown / web-access | 官网、文档、竞品页、文章 |
| Site mapping | XCrawl Map | Tavily Map | 找竞品 docs、blog、case studies |
| Multi-page crawl | XCrawl Crawl | Tavily Crawl | 系统性抓竞品网站或文档 |
| YouTube | `baoyu-youtube-transcript`, `yt-dlp` | Tavily Search | 标题、描述、字幕、评论线索、demo flow |
| X/Twitter | `twscrape`, baoyu-url-to-markdown, Chrome/web-access | Tavily Search / XCrawl Search | launch posts、replies、quote language、viral hooks |
| Reddit | Tavily Search with `site:reddit.com` | XCrawl Search/Scrape | 用户抱怨、替代方案、购买阻力 |
| GitHub | `gh` CLI / GitHub app | Tavily Search | developer tools 的 README、issues、stars、user language |
| Local knowledge base | Notes, wiki, raw materials | rg / local search | 过往知识、写作风格、已整理素材 |

## Required Freshness

如果涉及最近行业变化、竞品状态、API、产品能力、价格、融资、发布日程，必须实时查证。不要凭记忆回答。

## AI HOT

适用：

- AI / LLM / agent / developer tool / model release / AI SaaS launch。
- 用户想知道近期行业语境。
- 需要找“为什么现在”的市场背景。

默认：

- 宽问题走 `items?mode=selected`。
- 最近 24 小时、最近 3 天、最近 7 天按用户时间窗加 `since`。
- 关键词查公司或技术名时用 `q` 参数。

输出要提炼：

- 哪些话题正在热。
- 哪些用户痛点被反复讨论。
- 哪个趋势能支撑 launch 的 timing。

## Tavily

适用：

- 快速发现来源。
- 查询通用网页、媒体文章、竞品列表、Reddit/X/YouTube 搜索结果。
- 对多个问题做 research synthesis。

使用建议：

- Search 用于 discovery。
- Extract 用于 URL 已知的正文抓取。
- Crawl/Map 用于竞品站点结构。
- Research 只在需要跨来源综合时使用；不要让它替代自己的 launch 判断。

## XCrawl

适用：

- 需要 JS render 的页面。
- 需要结构化 JSON extraction。
- 需要 crawl / map 竞品网站或文档。
- Tavily 提取不完整时。

要求：

- 使用 `~/.xcrawl/config.json` 中的 key。
- 记录 endpoint、payload 和 URL。
- 具体事实必须保留来源 URL。

## YouTube Research

目标：

- 找 category 中别人怎么包装 promise。
- 看 demo 叙事顺序。
- 从评论里找真实语言。

建议 query：

- `<category> demo`
- `<pain> tool`
- `<competitor> review`
- `<category> AI`
- `<desired outcome> workflow`

输出重点：

- High-performing titles。
- Thumbnails / first 10 seconds 的 promise。
- 评论里的抱怨和惊讶点。
- demo 展示顺序。

## X/Twitter Research

目标：

- 找同类 launch 的第一行。
- 找真实回复里的 buying language。
- 找 quote tweets 中的反应。
- 识别过度使用的 announcement cliches。

工具顺序：

1. 如果有具体 X URL，用 `baoyu-url-to-markdown`。
2. 如果需要搜索公开 tweets，用 `twscrape`，但先确认账号池状态。
3. 如果 `twscrape` 不可用，用 Tavily / XCrawl 搜索。
4. 如果页面需要登录态，用 web-access / Chrome。

注意：

- X 数据源容易不稳定。拿不到时不要卡死，改用搜索结果和浏览器兜底。
- 不要把单条 viral tweet 当唯一规律。

## Reddit Research

目标：

- 找用户对现有方案的真实厌恶。
- 找替代方案和 workaround。
- 找买前顾虑。

建议 query：

- `site:reddit.com <pain> <category>`
- `site:reddit.com <competitor> problem`
- `site:reddit.com best <category> tool`
- `site:reddit.com <workflow> sucks`
- `site:reddit.com alternatives to <competitor>`

输出重点：

- exact language
- repeated complaints
- emotional spikes
- “I wish...” statements
- skepticism

## Competitor Research

目标：

- 知道市场已经怎么说。
- 找出不能再重复的泛话。
- 找可以 counter-position 的陈词滥调。

抓取：

- Homepage hero。
- Pricing。
- Docs / demo。
- Case studies。
- Changelog。
- Product Hunt / launch posts。

输出：

- competitor claim table
- stale words
- user-visible difference
- where this product can be sharper

## Customer Language Mining

来源优先级：

1. 用户提供的真实客户聊天、评论、销售记录。
2. Reddit / X / YouTube comments。
3. Review sites / Product Hunt comments。
4. Competitor issues / GitHub discussions for developer tools。

不要把 marketing copy 当 customer language。

## Source Record Format

所有来源统一记录：

```markdown
| Source | URL | Date Accessed | What It Proves | Confidence |
|--------|-----|---------------|----------------|------------|
```

Confidence:

- `High`: 一手资料、官网、原始用户评论、大量重复证据。
- `Medium`: 多个二手来源一致。
- `Low`: 单一搜索结果或推测。

Low confidence facts 不能进入 final script，只能进入 research notes。
