# Apify Mercari Japan SOLD Scraper 调研报告

> 调研日期：2026-05-03
> **Verdict: GO（30 天实验，$100-500 目标）**
> **闭环妥协**：本路径**违反 deeploop 闭环原则**（流量+交易在 Apify 平台），作为 30 天验证实验执行

---

## 闭环妥协的明牌说明

这条路违反 CLAUDE.md §0 闭环原则：
- 流量：Apify Store 内部搜索 = 不在你手里
- 交易：用户付钱给 Apify，Apify 抽 20% + compute units = 不在你手里
- 积累：用户账号、品牌信誉都在 Apify

**接受这个妥协的唯一理由**：
- 30 天能客观验证"AI 加速产能能否变现"假设
- 不需要营销/出镜（用户最弱项）
- 失败成本可控（$150 预算）
- 主路径 Manga Tracker 不动

---

## WINNER: Mercari Japan SOLD Comps Scraper

### 不是再做一个普通 Mercari listings actor

而是做"**已售出商品价格 + 卖家速度 + 跨平台 comp（Mercari JP × Yahoo Auctions Closed × Buyee）**"的 reseller intelligence actor。

### 30 天目标
- **$100-300**（保守）
- **$500**（上限）

### 90 天目标
- **$500 MRR**（成立 ceiling）

---

## 候选淘汰记录

| 候选 | 现有 MAU | 价格 | 评分 | 淘汰原因 |
|---|---|---|---|---|
| Tabelog (cloud9_ai) | 5 | $3/1k | 0.0 | 餐厅数据没人付费用 |
| Tabelog (piquno) | 3 | $80/1k | 0.0 | 定价高 27 倍仍只 3 MAU = 需求弱 |
| SUUMO (cloud9_ai) | 2 | $4/1k | 0.0 | 不动产合规雷区，buyer 是日本本土 |
| Yahoo Auctions Closed (contented_eyebrow) | 1 | $0.50/1k | 0.0 | 价格已卷到地板 |
| Mercari Listings (parseforge) | 0 | $7/月+usage | 0.0 | listings only 没价值 |
| **Mercari Japan SOLD (cloud9_ai)** | **4** | **$4/1k** | **5.0** | **唯一 sold + 5 星，但 4 MAU = 留给你空间** |
| Mercari Japan (fatihtahta) | **11** | $3.99/1k | **5.0 (2 reviews)** | 头部，但**不区分 sold vs active** = 你的差异化点 |
| 小红书 / Xiaohongshu | 5+ actors 已饱和 | -- | -- | 红海+反爬+合规 |

---

## 关键数据

- Mercari Japan 总 C2C 用户 **20M+**
- 日本 recommerce 市场 2025 达 **$6.16B**（10.2% YoY）
- 全球 reseller 真实痛点：**"知道 Mercari JP 实际成交价 vs 美国 eBay/Mercari 现售价的差"**，3X+ rule 是行业标准
- Mercari JP 自己有 "Price Search" **只对日本本土卖家开放**，海外 reseller 看不到 → 这就是缺口
- Apify 现有头部 Mercari actor (fatihtahta) **不专门做 sold + 不做跨平台 comp**

---

## 三个真实买家用例

### 1. 美国 vintage denim reseller（最大群体）
- 要批量查 Mercari JP "Levi's 501 BIG E" 已售价 + 卖家发货速度
- 决定每周扫货预算
- **愿意付 $20-50/月**用 actor + 自家 Airtable

### 2. 日本动漫周边 dropshipper（数量第二）
- 抓 "鬼滅の刃 figure" / "Bandai 限定" 的 sold price + 卖家 rating
- Feed 到 Shopify
- Apify fatihtahta 已有 2 条 5 星评论，证明此 buyer 真在付钱

### 3. 跨境运营外包公司 / Buyee 类竞品
- 要构建"日本商品价格指数"做内部 BI dashboard
- **愿意付 $100-500 一次性 + $50/月**

---

## 你的 actor 必须比头部 (fatihtahta) 多三件事

否则就是 me-too：

### 1. SOLD-only mode + 90 天价格历史
- fatihtahta 不强调 sold 字段
- 你做 sold 历史 + 平均成交价 + 中位数 + 卖家平均发货时长

### 2. 跨平台 comp
- 同一个 keyword 同时返回：Mercari JP sold + Yahoo Auctions closed + Buyee 现售价
- 输出**单条 unified record**
- **Apify 现在没有任何 actor 做到这点**

### 3. 日语 keyword 智能扩展（你的语言护城河）
- 用户输入 "vintage levi's"
- 你 actor 内部映射到日语别称：
  - リーバイス ヴィンテージ
  - BIG E / ビッグE
  - 66 前期
- 搜索召回率比英语-only actor **高 2-3x**
- fatihtahta（土耳其开发者）做不到

### 定价
- **$5/1k results**（比 fatihtahta 贵 25%）
- 靠跨平台 comp + 召回率正当化

---

## 技术难度评估

| 项 | 难度 | 备注 |
|---|---|---|
| Mercari JP 反爬 | 中 | 用 Cloudflare 但不严，Apify Residential Proxy 能过 |
| Yahoo Auctions Closed | 低 | 已稳跑 |
| Buyee 跨链接匹配 | 中-高 | URL 可机械映射 |
| 数据更新维护 | 低-中 | 选择器变了改一次代码 |
| 周时长投入 | 5-10h/周 | 第 1 周 8h，之后 2-3h/周维护 |

---

## $150 预算分配

- Apify Pro plan **$49/月** × 1 = $49（必须，Free tier 不够）
- Residential proxy add-on ≈ **$50**（Mercari 偶尔需要）
- 备用 **$51**（域名/landing page/X ads test）

---

## 闭环三问打分

- **流量 A：3/10**（Apify Store 内部搜索 = 平台拥有）
- **交易 B：5/10**（80/20 分成 + compute fees，不算坏但不在你手里）
- **积累 C：3/10**（用户账号在 Apify，下架就归零）

→ **总分远低于 Manga Tracker（8.5/10）**，因此只作 30 天实验，不作主路径

---

## 法律 + 合规

| 项 | 状态 | 对策 |
|---|---|---|
| Mercari ToS | **明确禁止 scraping** | UA 标识 Apify，2s+ rate limit，不存 PII |
| Yahoo Auctions JP | ToS 类似 | 同上 |
| 日本個人情報保護法 2025 | 加强跨境数据 | 不抓 seller 实名/地址（只 username），不存 EU/JP 用户数据 |
| 起诉历史 | **无** Mercari 起诉 Apify actors 的公开记录 | Mercari JP 可随时封 IP / 发 cease-and-desist。Apify 平台给一层缓冲 |

**最坏情况**：Mercari 给 Apify 发 DMCA-style takedown，actor 下架。损失 = $150 + 30h 时间。**可承受**。

---

## 失败迹象 + 红线

### 红线指标（Day 21 检查）
- Apify Store 总 users < 10 → **NO-GO，立即停**
- 跑过 free credit 但没人付费 → 价格降到 $2/1k 试一周
- Day 21 仍 < $50 → **D22 起停止开发，专心 Manga Tracker**

### 绿灯信号
- Day 14 ≥ 3 个用户主动私信问"可以加 X 字段吗" → 走对了
- Day 21 ≥ 1 个 $50+ 付费 + 1 条 5 星评论 → 90 天 $500 MRR 可达

---

## Bottom Line

- **GO 前提**：第一周 5-8h 写完 MVP（你 20 年全栈 + Cursor Max，Crawlee + TS 这点活很轻）
- **NO-GO 触发**：如果第一反应是"不是我自己用户，要花精力理解 reseller" → 直接 NO-GO，闭环原则赢，全力 Manga Tracker
- **此 niche 真实空间**：30 天 $100-300 + 90 天 $500 MRR ceiling
- **不要追求 $10K MRR**，那是 ParseForge 100+ actor 矩阵路线，会冲击主路径

---

## 数据来源

- [Apify Mercari Japan Scraper - cloud9_ai](https://apify.com/cloud9_ai/mercari-scraper)
- [Apify Mercari Japan Scraper - fatihtahta](https://apify.com/fatihtahta/mercari-japan-scraper)
- [Apify Mercari Scraper - parseforge](https://apify.com/parseforge/mercari-scraper)
- [Apify Tabelog - cloud9_ai](https://apify.com/cloud9_ai/tabelog-scraper)
- [Apify Tabelog - piquno](https://apify.com/piquno/tabelog-japan-restaurant-scraper)
- [Apify SUUMO - cloud9_ai](https://apify.com/cloud9_ai/suumo-scraper)
- [Apify Yahoo Auctions Closed](https://apify.com/contented_eyebrow/yafuoku-closedsearch-crawler)
- [Apify Buyee Scraper](https://apify.com/123webdata/buyee-scraper/api)
- [Mercari Japan Import Reselling Guide 2026 - Underpriced](https://www.underpriced.app/blog/mercari-japan-import-reselling-guide-2026)
- [The Real Mercari Guide 2026 - CLOSO](https://closo.co/blogs/blog/the-real-mercari-guide-japan-imports-seller-fees-and-avoiding-scams-in-2026)
- [Japan Recommerce Intelligence Report 2025](https://www.globenewswire.com/news-release/2025/07/16/3116206/28124/en/Japan-Recommerce-Intelligence-Report-2025.html)
- [Mercari ToS - Prohibited Conduct](https://www.mercari.com/us/help_center/topics/account/policies/prohibited-conduct/)
- [Mercari Japan Price Search Launch](https://www.valueaddedresource.net/mercari-japan-launches-price-search/)
- [Most Popular Apify Actors 2026](https://use-apify.com/docs/best-apify-actors/most-popular-actors)
- [Apify Review 2026 - Hackceleration](https://hackceleration.com/apify-review/)
