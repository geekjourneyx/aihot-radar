# AIHot Radar · REPORT_SPEC

## Scheduling and ownership
- Task name: AIHot 强信号雷达.
- Timezone: Asia/Shanghai; every day at **09:00, 14:00, 19:00** including weekends.
- Repository: `geekjourneyx/aihot-radar`; **commit directly to main**, never open a PR.
- Long-term state is GitHub, not a prior chat. Every run must read this specification, today's existing report, yesterday's report and available last-7-day reports.
- Daily report: `reports/YYYY/MM/DD.md`. One file/day, slots are idempotently updated. Repeated runs must not duplicate content.
- Report title and task-visible summary include local date and hour. When complete return commit SHA and a working link; on failure report honestly.

## Official discovery API
- API documentation: https://aihot.news/agent?tab=api
- Agent instructions: https://aihot.news/api/v1/agent
- OpenAPI schema: https://aihot.news/openapi-v1.json
- Base: https://aihot.news/api/v1 (do not use legacy /api/public).
- `/items?mode=selected&window=24h&limit=20`: selected daily discovery; also collect the supported seven-day window and category-specific views as the schema permits.
- `/hot-topics`: trending Top 10 discovery only; never treat popularity as proof.
- `/stories/{publicId}`: use for event timelines, related stories and cross-reporting (only for real public IDs found in data).
- `/dailies/latest`: today's daily after 08:00 Beijing time.
- `/weeklies/latest`: weekly perspective, published Mondays after 10:00.
- `/monthlies/latest`: monthly perspective, published after 10:30 on the first day of each month.
- Retrieve only as justified by the research question; do not blindly hit every endpoint for each candidate. Be mindful that daily/weekly/monthly data are not reissued every few hours.
- Keep original item URLs: v1 uses `links.original`, `links.aihot`, `originalTitle`, `source.name`; pagination uses `page.count`, `page.hasMore`, `page.nextCursor`. Follow the live OpenAPI for exact parameters.
- Use gzip/br, ETag / If-None-Match where practical, honor 304 and 429 Retry-After, avoid over 60 requests/minute/IP and never bypass blocks. If service is unavailable, use previously verified evidence and label stale state clearly. Observe AIHot use and attribution rules; do not wholesale republish their content.

## Questions to answer
1. **Today**: what actually happened since last run, and what changed judgment?
2. **Last 7 days**: how did the story evolve? Show dated evidence, reversals, opposing signals, momentum.
3. **Last ~30 days**: is this a durable emerging trend, a recycled news cycle, an isolated announcement, or still unknown? Only infer within the limits of available archives.
4. **Why this matters**: technical changes, underlying mechanism, who benefits, costs and constraints, product opportunities and business models.
5. **Worth sharing**: what's the concrete non-obvious angle for X; which claims can be backed by firsthand links?

## Topics and priority
Cover all high-value news, with particular attention to AI models and post-training/RL/RSI, coding agents, harness engineering, evaluations, cost/task and long-running reliability, developer tools, open-source repos, distribution, pricing, commercialization, growth, startups, industry shifts and exceptional contrarian opinions. A promising low-heat early project can outrank a viral headline. Don't let interest tags exclude valuable unexpected topics.

## Evidence and noise reduction
- AIHot is a discovery/aggregation layer, not independent verification. Seek the nearest primary source for every formal signal: research paper, author announcement, GitHub repo/release/commit, official docs, benchmark methodology, regulator filing, primary data or direct interview.
- Every substantive signal needs an original clickable source URL and at least one additional independent source or a transparent note that corroboration is missing. For high-consequence or disputed items, look for counterevidence.
- Mark each important claim as `verified_fact`, `author_claim`, `community_evidence`, `inference` or `unknown`. Do not label a company's own claim independently verified.
- Preserve published/event dates separately from fetch dates. Recycled or resurfaced stories must not be titled as fresh news.
- Verify mutable numbers, versions, adoption stats, benchmarks, financing and price against cited, dated sources.
- Cluster duplicates by original link/event/story. Cross-source repeats are one event, not independent breakthroughs.
- Score candidates on novelty (0–5), evidence quality (0–5), durability (0–5), relevance/actionability (0–5), and contrarian insight (0–5), with a noise penalty (0–5). The score is a decision aid; include early-potential signals and do not force quotas.
- Label classes: `strong`, `worth-watching`, `early-potential`, `unverified`; no original source -> not `strong`.
- Distinguish rapid popularity from enduring trajectory: a 7-day/30-day claim requires multiple dated observations; otherwise mark insufficient historical evidence.
- Include 2–5 deep-link references for substantial projects when possible; include supporting and opposing voices. Only quote short excerpts, write independent original synthesis.

## Report structure
```markdown
# AIHot 强信号雷达｜YYYY-MM-DD
> Last updated: YYYY-MM-DD HH:mm Asia/Shanghai
## 今日总判断
## 09:00 上午基线
### 本轮新增强信号
### 模型 / Agent / Harness / 评测
### 开源 / 工具 / 产品机会
### 行业 / 商业模式 / 增长
### 去噪与待验证
## 14:00 下午真实增量
### 新增信号与新证据
### 热点变化 / 反证 / 纠错
### 趋势修正
## 19:00 晚间收盘
### 新增信号与新证据
### 今日最终判断
### 明日关注
## 7 天趋势时间线
## 30 天趋势与证据缺口
## 最值得发 X 的候选主题
## 信号索引与评分
## Evidence Registry
```
If a slot has not run, mark it pending; do not pretend it ran. For each signal use stable `S-001` IDs, title, happened-at date, why-now, evidence class, 1–3 sentence mechanism analysis, implications, confidence/limitations, share angle and source links. Track stable `E-001` evidence IDs in a registry (type, date, URL, supported claim).
The tweet shortlist should contain a sharp hook and 1–2 key evidence URLs, and mark `ready` / `needs-verification`. Do not auto-post.

## Incrementality, persistence and safety
- 09:00 establishes the baseline; 14:00 compares against 09:00; 19:00 compares against 14:00 and finalizes. Each update must preserve previous valid findings and explicit corrections.
- Updates to old themes need material new facts, revised confidence, contradiction, official response or changed implications. A rising heat score alone is not enough.
- Read reports and merge semantically; do not blindly overwrite existing completed slots. Same slot retry is an idempotent replacement. Use current blob SHA for updating a GitHub file. On conflict refetch then reconcile.
- Never fabricate API responses, dates, sources or commits. If GitHub write fails, clearly separate analyzed findings from persistence status.
- After each successful write re-read `reports/YYYY/MM/DD.md` and verify content and commit.
- Chat output stays short: date-hour, report link, counts, at most 3 takeaways, top tweet-worthy topics, commit SHA / failure.
