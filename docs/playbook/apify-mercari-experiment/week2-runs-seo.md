# Week 2: Runs & SEO（Day 8-14）

> **本周目标**：5+ 自然试用用户 + Apify Store SEO 优化 + 公开 demo dataset
> **总投入**：5-7 小时
> **前置条件**：Week 1 全部通过

---

## Day 8（周一晚 1 小时）：自跑 50 次生成 demo dataset

### Step 8.1：跑 5 个 reseller 高频关键词（45 分钟）

每个跑 10 行 results。打开 Apify Console → 你的 Actor → Run：

| Keyword | Max Items | 期望 Output |
|---------|-----------|-----------|
| vintage levi's | 10 | sold price 历史 + JP variants 召回 |
| supreme box logo | 10 | sold + Yahoo Auctions |
| bape full zip | 10 | 三平台 |
| 鬼滅の刃 figure | 10 | sold + Buyee（动漫周边） |
| ガンプラ 限定 | 10 | sold（日本特化） |

每跑完 → 在 Apify Console 看 dataset → 确认数据完整。

### Step 8.2：导出 demo dataset 公开（15 分钟）

每个 dataset 都设为 public：
- Apify Console → Datasets → 选某个 → Settings → "Make public"
- 复制 public URL（例：`https://api.apify.com/v2/datasets/{id}`）

把 5 个 public dataset URL 加到 README 里：

```markdown
## Sample Output

Live demo datasets (no signup needed):
- [Vintage Levi's sold history](https://api.apify.com/v2/datasets/...)
- [Supreme box logo cross-platform comp](https://api.apify.com/v2/datasets/...)
- ...
```

`apify push` 重新部署。

---

## Day 9（周二晚 1 小时）：Apify Store SEO 关键词优化

### Step 9.1：研究关键词（30 分钟）

打开 Apify Store 搜索：
- https://apify.com/store?search=mercari → 看排名 top 5 的 actor
- 看他们的 description 用了什么词
- 看他们 README 标题
- 看他们 tags

记录：
```
高频关键词 (Apify Store 内部 SEO):
- mercari japan
- mercari sold price
- vintage import
- reseller intelligence
- japan recommerce
- yahoo auctions japan
- buyee
- jp scraper
- cross-platform price comp
```

### Step 9.2：优化 Apify Store metadata（30 分钟）

打开 Console → Actor → Settings：

**Title**：`Mercari Japan SOLD Comps - Cross-platform Reseller Data`

**Description**（150 字符内）：
```
Get Mercari Japan SOLD prices + Yahoo Auctions closed + Buyee comp. JP keyword auto-expansion. For vintage resellers, dropshippers, BI dashboards.
```

**Categories**：E-commerce, Data extraction, Marketing

**Tags**：mercari, japan, sold-price, vintage, reseller, yahoo-auctions, buyee, cross-platform

**README 重写**：
- H1：`Mercari Japan SOLD Comps Scraper - Reseller Intelligence`
- H2 包含关键词："Why Use This Over Other Mercari Scrapers"
- 段落 1 重复关键词 5+ 次（自然）

`apify push` 重部署。

---

## Day 10（周三晚 1 小时）：Reddit 软发帖

### Step 10.1：账号准备（15 分钟）

如果你 Reddit 账号 Karma < 50 / 账号 < 30 天：
- 先在 r/Flipping、r/Mercari、r/ResellerCommunity 评论 5-10 条好回复（不发帖，只评论）
- 1-2 周后再发帖

如果 Karma 够：直接发帖。

### Step 10.2：发 r/Flipping（30 分钟）

**严格按这个模板**（不能直接广告）：

```markdown
Title: Built a free Mercari Japan SOLD price tool — sharing demo dataset

Body:

Hey r/Flipping,

I've been doing some Mercari Japan reselling on the side and got tired of:
- Mercari JP "Price Search" being locked to Japan accounts
- Existing scrapers only showing active listings, not sold history
- Having to manually check Yahoo Auctions closed for the same item

So I built a tool that pulls:
- Mercari JP SOLD prices (90-day history)
- Yahoo Auctions Closed (final bid prices)
- Buyee current prices
in one unified output.

Auto-expands keywords to Japanese (e.g., "vintage levi's" → リーバイス ヴィンテージ + BIG E + 66前期 + 501XX) so you don't miss listings.

Free demo dataset (no signup): [your public dataset URL for vintage levi's]

If you want me to run a batch for your specific keyword, drop it in comments — I'll DM you the dataset.

Note: Tool is on Apify Store ($5/1k results after free credit) — being upfront about that. But the demo dataset is genuinely free, no email needed.

Curious what fields you'd find most useful. Considering adding:
- Seller average shipping time
- Item condition breakdown
- Trend chart (price over time)

Feedback welcome.
```

发完不要刷自己帖。等 24 小时看回复。

### Step 10.3：发 r/Mercari（15 分钟）

类似模板，重点放在"我帮你跑数据"角度。

---

## Day 11（周四晚 1 小时）：Buyee Discord 软渗透

### Step 11.1：找 Buyee 相关 Discord（15 分钟）

搜：
- https://disboard.org/search?keyword=buyee
- https://disboard.org/search?keyword=mercari
- r/Mercari pinned post 里有 Discord 邀请

加入 3-5 个 reseller Discord。

### Step 11.2：观察 1 周（不发广告）（45 分钟）

- 看大家在问什么（一定有人问"怎么知道 sold price"）
- 找到 1-2 个具体提问 → **私信回答**（不公开发广告）：

```
Hey, saw you asking about Mercari sold prices.
I built a tool for this — three-platform comp (Mercari sold + Yahoo Auctions + Buyee).
If you want, I can run [keyword] for you and DM the dataset (no charge).
Demo: [public dataset URL]
```

如有人回应 → 跑数据 → 给他看 → 引导到 Apify actor link。

---

## Day 12（周五晚 1 小时）：监控 + 第一波反馈

### Step 12.1：检查 Apify Console（20 分钟）

打开 Apify Console → Actor → Analytics：
- Total users（试用过的人）
- Total runs（自然搜索带来的）
- Top input keywords（看大家在搜什么）

**预期 Day 12 数据**：
- 5-10 个 free users
- 30-100 runs

如果 < 3 users → SEO 还不够，回 Day 9 重做关键词。

### Step 12.2：处理 Reddit / Discord 反馈（40 分钟）

- 回所有 Reddit comments（即使是负面）
- 私信回 Discord 互动
- 收集 feature request 到 PROGRESS.md

---

## Day 13（周六，2 小时）：根据反馈迭代

### Step 13.1：实现用户最高频请求字段（90 分钟）

预期高频请求：
- "seller average shipping time" → 解析卖家页 reviews 推算
- "shipping cost" → 解析详情页 shipping section
- "item condition breakdown" → 已有，但加 percentage 统计

让 Cursor 加新字段：

提示词：
```
在 Mercari sold scraper 加新字段：
1. seller_avg_shipping_days：从卖家详情页 reviews 抓 "発送までの日数"，取最近 20 条平均
2. shipping_cost：从商品详情页 "送料" section 抓
3. item_condition：标准化为 ["新品", "未使用に近い", "目立った傷なし", "やや傷あり", "傷や汚れあり"]

更新 dataset schema
```

### Step 13.2：发布 v1.1（30 分钟）

```bash
apify push

# 在 Apify Console 写 changelog：
# v1.1 (Day 13): Added seller_avg_shipping_days, shipping_cost, item_condition standardization
```

---

## Day 14（周日，1 小时）：Week 2 决策点

### Step 14.1：填决策表

| 指标 | Day 14 数据 |
|------|---------|
| Apify Store free users | ___ |
| 总 runs | ___ |
| Reddit 帖子 upvotes | ___ |
| Discord 私信回应数 | ___ |
| 用户主动私信问"加 X 字段" | ___ |
| **付费转化** | 0（正常，下周才转化）|

### Step 14.2：决策

**5+ users + 1+ feature request** → ✅ **走对了，下周做付费转化**

**< 5 users 但 reddit 有正向回复** → ⚠️ **优化 Apify Store SEO**：
- 改 title（加更精准关键词）
- README 加更多 use case
- 多发 1 篇 Reddit（r/IndieHackers / r/EntrepreneurRideAlong）

**0 users + 0 reddit 反响** → ⚠️ **检查根因**：
- Apify Store 搜你的 actor 能搜到吗？
- README 是英文的吗？
- 价格 $5/1k 是否过高？降到 $3/1k 试一周

```bash
git add . && git commit -m "Week 2 done"
```

---

## 下一步

打开 [week3-paid-conversion.md](./week3-paid-conversion.md)。
