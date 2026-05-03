# Week 3: Paid Conversion（Day 15-21）

> **本周目标**：≥ 1 笔 $50+ 付费 + 1 条 5 星评论
> **总投入**：5-7 小时
> **前置条件**：Week 2 至少 5+ 自然 free users

---

## Day 15（周一晚 1 小时）：私信跟进 free users

### Step 15.1：导出 free users 列表（15 分钟）

Apify Console → Actor → Users：
- 看谁试过你的 actor
- 看他们跑了多少 runs
- 看他们 input 了什么关键词

筛选：跑过 ≥ 5 次的（说明真在用）。预期 2-5 个。

### Step 15.2：私信触达（45 分钟）

通过 Apify 内部消息（每个 actor 用户页面有 message 按钮）发：

```
Hey [username],

Saw you've run my Mercari Sold Comps actor [N] times this week — thanks for trying it!

Quick question: what specific use case are you using it for?
- Vintage reselling?
- Dropshipping?
- Something else?

I'm working on v1.2 and want to prioritize what'd actually help. 
A few things I'm considering:
1. Trend chart (price over last 6 months)
2. Seller reliability score
3. Auto-arbitrage alert (Mercari < eBay by X%)

Also: if you need to scale up runs, the actor is $5/1k results after free credit.
Happy to give you a 30% discount code if that helps you commit. Just reply.

— [你的名字]
```

**关键**：不直接卖，先问需求 + 主动给折扣。

---

## Day 16-17（周二周三晚各 1 小时）：第二轮 Reddit + Discord

### Step 16.1：发 r/IndieHackers（30 分钟）

不是卖货，是分享开发故事：

```markdown
Title: Built a Mercari Japan reseller tool in 7 days using Cursor AI — Apify launch results

Body:

Quick recap for fellow indie devs.

Problem: vintage resellers buying from Mercari JP need SOLD prices, but Mercari's "Price Search" is locked to Japan accounts. Existing Apify scrapers only show active listings.

Solution: Built a Mercari sold + Yahoo Auctions closed + Buyee cross-platform scraper with Japanese keyword auto-expansion (e.g., "vintage levi's" → 8 JP variants).

Stack:
- Apify Crawlee + TypeScript
- Cursor AI for reverse-engineering Mercari's anti-bot
- Day 1-7 timeline with detailed daily breakdown

Results so far:
- Day 14: [N] free users, [M] runs
- Day 21: aiming for first paid conversion ($50+)

Honest stuff:
- This is an experiment, not main product
- Apify takes 20% cut + I pay $49/mo Pro plan
- Closure-loop sacrifice acknowledged (users belong to Apify, not me)

Open to questions on tech / business / cold-start strategy.
```

IndieHackers 圈对"诚实分享"包容度高，转化率比直接广告好。

### Step 16.2：发 Buyee Discord 详细 demo（30 分钟）

不是私信，是公开发：

```
Hey y'all,

Made a tool to compare Mercari Japan sold prices, Yahoo Auctions closed, and Buyee current prices in one go. Free demo:
[live dataset URL for "supreme box logo"]

Notice on row 3: Mercari sold ¥45k vs Buyee current ¥58k vs Yahoo Auctions closed ¥41k.
3-platform spread = 33%. Helps you decide whether to wait or buy now.

If you want me to run [your keyword], drop it in this thread.

Tool: [Apify URL]
```

---

## Day 18（周四晚 1 小时）：直接 sales pitch 给最热门 user

### Step 18.1：识别 power user（15 分钟）

回到 Apify Console → Users → 排序 by run count：
- 找跑了 ≥ 20 次的（重度用户，free credit 快用完）
- 这是最可能付费的人

### Step 18.2：直接报价（45 分钟）

私信：

```
Hey [username],

Saw you've run 23 batches this week — looks like you're scaling up. 

Free credit gives ~100 runs / month. Beyond that, $5/1k results.
For your usage rate, that'd be ~$30-50/mo.

If you can commit to a paid plan now, I'll send you:
- 30% off first 3 months ($3.50/1k instead of $5)
- v1.2 early access (trend chart + arbitrage alerts)
- Direct line to me for custom requests

Want me to set that up? Just say yes and I'll send the discount code.
```

---

## Day 19（周五晚 1 小时）：定价测试

如果到 Day 19 还没付费转化：

### Option A: 降价测试（30 分钟）

Apify Console → Actor → Pricing：
- 改成 $3/1k results
- 通知现有 free users："Price dropped to $3/1k for first 30 days"

### Option B: 加 freemium tier（30 分钟）

修改 actor：
- 默认输出前 50 条免费
- 超过 50 条 → Apify 标准计费

这样能让"试一下"和"真用"分层。

### Step 19.2：决定走哪条（30 分钟）

看 Day 14-19 的数据：
- runs 多但 users 少 → 走 Option B（让现有用户跑更多）
- users 多但 runs 少 → 走 Option A（降价让人愿意付）
- 两个都少 → 看 Day 21 决策

---

## Day 20（周六，2 小时）：v1.2 发布

### Step 20.1：实现 trend chart 功能（90 分钟）

让 Cursor 加：
```
在 Mercari sold scraper 输出加：

新字段：
- price_trend_30d: { date: "YYYY-MM-DD", median_price: number, count: number }[]
- price_trend_90d: 同上

逻辑：
- 抓回 90 天 sold data 后，按周聚合 median price
- 输出 weekly trend
- 用于 reseller 看价格走势
```

### Step 20.2：发布 v1.2 + 通知（30 分钟）

```bash
apify push
```

Apify Console 写 changelog：
```
v1.2 (Day 20): Added 30-day and 90-day price trends. 
For resellers tracking demand cycles.
```

发邮件给现有 power users：
```
Subject: v1.2 just shipped — price trends added

Hey,

Just shipped v1.2 with weekly price trends (30d / 90d).
Check your last batch's output — new fields are there.

Trying to make this useful for actual reseller workflows.
Any features you'd want next? Reply directly.
```

---

## Day 21（周日，1 小时）：Week 3 决策点

### Step 21.1：填决策表

| 指标 | Day 21 数据 | 状态 |
|------|---------|-----|
| 总 free users | ___ | |
| 总 runs | ___ | |
| **付费 users** | ___ | |
| **第一笔付费** | $___ | |
| 5 星评论 | ___ | |
| Reddit / Discord 互动 | ___ | |

### Step 21.2：决策（最关键）

**≥ 1 笔 $50+ 付费 + 1 条好评** → ✅ **GO Week 4：扩量**

**0 付费但 ≥ 10 free users + 反馈积极** → ⚠️ **延期 1 周**：
- 问每个 free user "什么阻止你付费"
- 修最大障碍（价格 / 缺字段 / 信任）
- Day 28 再决策

**< 10 free users + 0 付费** → ❌ **NO-GO 信号明确**
- 不再投入开发
- Day 22-30 维护现状，回 Manga Tracker

```bash
git add . && git commit -m "Week 3 done"
```

---

## 下一步

打开 [week4-decision.md](./week4-decision.md)。
