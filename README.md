# AIHot Radar

> 把 AI 行业实时热点，沉淀成有证据、可追踪、可复用的长期趋势判断。

每天 **09:00 / 14:00 / 19:00（北京时间）** 自动扫描 [AIHot](https://aihot.news/agent?tab=api)，从最新资讯、精选、热点事件、日报、周报和月报里寻找真正有价值的变化，再回到论文、代码、发布公告和其他一手来源核验。

## What matters
- 今日发生什么、新增什么，哪些是旧闻重复传播？
- 过去 7 天有没有出现更强证据、反证、转折？
- 最近约 30 天是否形成趋势，还是短暂热度？
- AI 模型、Agent Harness、评测、开源工具、产品商业化，有哪些实质变化？
- 哪些值得发 X，哪些适合进一步深度研究、尝试做产品？

原则：**Signal Value > Heat Score**；一手证据优先；对争议保留反证；不强行凑满条数；AIHot 负责发现、分析要独立核实。

## Daily cadence
- 09:00 今日基线：精选 + 热点 + 日报 + 近期趋势。
- 14:00 午后增量：对比上午，只记录实质新信号与纠错。
- 19:00 晚间收盘：最终判断 + 推文候选 + 次日观察。

每日仅一份报告：`reports/YYYY/MM/DD.md`，三次运行幂等更新同一文件。自动化任务通过 GitHub 连接**直接提交 main**，不走 PR；仓库是唯一持久状态源，聊天只返回简报与提交 SHA。

## Data/API
- [Agent 接入指南](https://aihot.news/agent?tab=api)
- [Agent 提示](https://aihot.news/api/v1/agent)
- [OpenAPI v1](https://aihot.news/openapi-v1.json)

API v1 匿名只读。使用 `/api/v1/items`、`/hot-topics`、`/stories/{publicId}`、`/dailies/latest`、`/weeklies/latest`、`/monthlies/latest`，根据问题选接口，遵守访问频率和 ETag 机制。

## Contract
**[REPORT_SPEC.md](REPORT_SPEC.md)** 是自动任务的强约束：路径、报告结构、证据标签、去重、增量规则、趋势时间线、写入与验收都以它为准。

同类实践：[HNews Radar](https://github.com/geekjourneyx/hnews-radar)。AIHot Radar 作为 AI 全域信号视角，与 HN 的社区/项目讨论视角互补，而不简单重复。
