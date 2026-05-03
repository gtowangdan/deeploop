# Week 4: 冷启动 + 第一笔收入（Day 22-30）

> **本周目标**：100 装机量 + 6-10 个付费用户（约 $30-$50 第一笔收入）
> **总投入**：10-12 小时
> **前置条件**：苹果审核通过，App 已上架

---

## 上线前最后检查（Day 22 早上 30 分钟）

- [ ] App Store URL 能打开（搜 ChapterPing 能搜到）
- [ ] 5 套 CPP（自定义产品页）已发布
- [ ] 4 个语言版本描述都已审核通过
- [ ] 测试机能下载安装
- [ ] 付费流程能走通
- [ ] 章节通知端到端跑通
- [ ] App Store 评分页面能打开

---

## Day 22（周一）：Reddit r/manga 软发帖

### Step 22.1：账号准备（已有则跳过，30 分钟）

1. Reddit 账号年龄 > 30 天 + Karma > 50（不够的话先在 r/manga 评论 10-20 条好回复养号）
2. 加入这些 sub：
   - r/manga（200 万订阅）
   - r/lightnovels（30 万）
   - r/MangaPiracy（150K，注意：他们对正版工具友好）
   - r/IndieDev（700K，独立开发者）

### Step 22.2：发帖文案（30 分钟）

**严格按这个模板**（不要自吹自擂，要诚实）：

```markdown
Title: [iOS] I built a manga & light novel tracker because ManGo's notifications didn't work

Body:

Hi r/manga,

Long-time lurker, first-time poster. I made an iOS app called ChapterPing because I was tired of:

- Missing chapter releases (ManGo's notifications fail ~80% of the time, lots of similar reports here)
- No app handling manga + light novels + regular books in one place
- Bookly is great for English books only, MangaTime is manga-only

What it does:
- Track manga (AniList data), light novels (AniList + Rakuten), books (Open Library)
- Reliable chapter alerts via push (cron + Cloudflare Workers, not in-app polling)
- Works in 3 languages: 呪術廻戦 / Jujutsu Kaisen / 咒术回战 — same series
- iOS Widget + Live Activity (lock screen shows "3 series updated today")

Free for up to 5 series. Pro is $4.99/mo for unlimited.

Honest stuff:
- Solo dev, this is my first iOS subscription app
- I don't embed any manga content (Apple compliance)
- Beta-quality, expect bugs the first week
- I genuinely want to know what's missing — drop suggestions

Link: [App Store URL]

Happy to answer anything.
```

### Step 22.3：发帖时机（30 分钟监控）

**最佳时间**：美国东部 9-11AM（PT 6-8AM）周一/三/五

发完：
- 不要刷自己的帖（Reddit 算法会降权）
- 看到回复 5 分钟内回应（正反都回，态度真诚）
- 收集前 10 条反馈到 Notion

### Step 22.4：监控数据

打开 App Store Connect Analytics:
- 当天看 Impressions, Product Page Views, Downloads
- **预期**：100-500 装机量（Reddit 主流 sub 帖能爆）

---

## Day 23（周二）：Hacker News Show HN

### Step 23.1：HN 账号准备（如果没有，30 分钟）

1. https://news.ycombinator.com/login → 注册
2. 账号 < 30 天直接发 Show HN 容易沉，**最好提前在 HN 评论 5-10 条**

### Step 23.2：写 Show HN（45 分钟）

**HN 文化**：技术细节 > 营销话术。诚实 + 有趣 + 短。

```markdown
Title: Show HN: Manga and book tracker with reliable chapter alerts (iOS)

Body:

I built ChapterPing to scratch my own itch — I was using ManGo to track manga, but
the chapter notifications failed about 80% of the time (others report the same).

Tech stack:
- iOS native (SwiftUI), iOS 17+
- Backend: Cloudflare Workers + KV + Cron Triggers (every 30 min)
- Data sources: AniList GraphQL, Mangadex, Rakuten Books, Open Library
- Notifications: APNs from Workers (no in-app polling, battery-friendly)
- Tri-lingual metadata: JP / EN / CN (same series, three names)

The tricky part was chapter detection. AniList chapters field is often null for
ongoing manga. Mangadex API gives more reliable chapter timestamps. I cache to KV
and only push when last_chapter_id changes.

Web companion (Next.js) coming soon for cross-device sync.

Free tier: 5 series. Pro $4.99/mo or $29.99/yr.

App Store: [URL]
GitHub (open-sourcing the Workers backend in a few weeks): [planned]

Feedback welcome.
```

### Step 23.3：发帖时间

**最佳**：周二 7-9 AM PT（美西时间）= 日本时间 23-25 时

### Step 23.4：监控 + 互动

- HN 前 1 小时决定是否上首页
- 上首页 = 5K-50K 装机
- 没上首页 = 50-300 装机（也 OK）
- 评论必回，技术问题详细回答

---

## Day 24（周三）：5ch + 小红书

### Step 24.1：5ch 漫画板（45 分钟）

5ch 文化：**严禁纯广告**，必须像普通用户聊天。

板块：[5ch 漫画板](https://medaka.5ch.net/comic/)

找一个**章节通知**相关的话题（搜「アプリ」「通知」），跟帖：

```
通知ちゃんと来るアプリないかなって思ってたら、
ChapterPing っていうの見つけた。
追加5部までは無料で、月額600円で無制限。
通知の精度はManGoより良かった。
個人開発っぽいから今後どうなるかわからんけど、
今のとこ満足してる。

(URL: appstore link)
```

**绝对不要**：
- 自夸「最高」「最強」
- 暴露自己是开发者
- 在多个帖子重复

### Step 24.2：小红书（45 分钟）

注册「日漫追番工具分享」账号（如果没有），发图文笔记：

```
标题：终于找到能同时追漫画+轻小说的 App

封面：截图（中文版主界面 + 大字「漫画+轻小说+书 三合一」）

正文：
之前一直用 MAL（MyAnimeList）追漫画，但是：
1️⃣ 没有轻小说分类
2️⃣ 通知经常不来
3️⃣ 界面是 2010 年的

最近发现一个 ChapterPing，亮点：
✅ 漫画 + 轻小说 + 书 一个 App 搞定
✅ 章节更新立刻通知
✅ 中日英三语都能搜（呪術廻戦/咒术回战/Jujutsu Kaisen 都能找到）
✅ iOS Widget 主屏显示

免费版能追 5 部，重度用户买 Pro（4.99/月）

#日漫 #漫画推荐 #追番 #iOS #App推荐
```

发 3-5 张截图（中文 CPP 截图）。

### Step 24.3：Twitter / X 日文（30 分钟）

发短文（日文）：

```
個人開発でiOSアプリ「ChapterPing」をリリースしました📚

漫画・ライトノベル・本を一つのアプリで追跡。
章節更新を Push で即通知。
日中英 三言語検索対応。

無料版5作品まで、Pro月600円。

[App Store URL]

#個人開発 #iOSアプリ #漫画
```

转发：找日本独立开发者圈（@daichifukui, @yoheinakajima 等）@ 一下

---

## Day 25-28（周四到周日）：反馈处理

### Step 25.1：每天监控（每天 30 分钟）

打开这些 dashboard 巡视：
- App Store Connect Analytics（装机量、转化率、关键词排名）
- RevenueCat（付费订阅、留存）
- Reddit / HN 评论
- App Store 评论

### Step 25.2：紧急 bug 修复（每天 1-2 小时）

前 7 天最常见 bug：
- 章节通知不来（数据源差异）
- 搜索某些作品搜不到（AniList 数据缺失）
- Widget 不刷新
- 付费流程闪退

每个紧急 bug 修复 → Xcode Archive → Submit → 加急审核（联系 Apple 通常 1 天通过）

### Step 25.3：评价回复（每天 20 分钟）

App Store 每条评论必回。1 星评论尤其重要：

```
ご意見ありがとうございます。
[具体问题] については次のアップデートで対応します。
お手数ですが support@chapterping.com までご連絡いただければ詳しくお話できます。
```

### Step 25.4：第二轮发帖（Day 27 周六）

如果 Day 22-24 反响平淡（< 100 装机），第二轮：

- r/IndieDev：Show your project（独立开发者圈互相支持）
- Indie Hackers：Build in public 长帖
- Product Hunt：周二上线

---

## Day 29-30（周末）：盘点 + 决策

### Step 29.1：数据汇总（30 分钟）

填这个表（Google Sheet 或 Notion）：

| 指标 | 30 天数据 |
|------|---------|
| 总装机量 | ___ |
| 转化率（装机 → 付费）| ___ % |
| Pro 订阅数 | ___ |
| MRR（月收入）| $___ |
| 月留存（D7） | ___ % |
| App Store 评分 | ___ / 5 |
| 关键词 Top 10 | ___ |

### Step 29.2：决策

**乐观情况（100+ 装机 + 6+ 付费 + $30+ 收入）** → ✅ **GO 第二月**
- 继续优化 ASO
- 写 v1.1 升级（Web 端 / 韩漫支持）

**中等情况（50-100 装机 + 1-5 付费）** → ⚠️ **GO 但调整**
- 渠道哪个最有效继续投
- 分析为什么转化低（试用太短？文案不清楚？）
- 加 14 天免费试用

**差情况（< 50 装机）** → ⚠️ **不是死，继续调**
- 第 5 周再发一轮：Indie Hackers 长帖 + Product Hunt + AppSumo
- 调 ASO 关键词
- 检查是否被 App Store 隐藏（搜 ChapterPing 能否搜到）

**极差情况（连续 1 个月装机 < 30 + 0 付费）** → ❌ **wedge 不对**
- 重新评估：是产品问题还是渠道问题？
- 用户访谈 5 个真实下载用户问"为什么删了"
- 决定 pivot 还是关停

---

## Week 4 后第二个月（Day 31-60）

### 优先级 1：扩 Web 端
- Next.js + Cloudflare Workers（同后端）
- 域名（chapterping.app 或 chapterping.com）
- Web 端 Stripe 直收（绕开美国区 Apple 30%）
- SEO 长尾页（每作品一页）

### 优先级 2：v1.1 功能
- 韩国 webtoon 支持（네이버웹툰 RSS）
- 中文网文支持（起点国际 / 番茄海外 API）
- 朋友追番 social（轻量）

### 优先级 3：内容营销
- Note.com 月更 1 篇（开发日记 + 案例）
- Twitter 日文每周 1 条（更新 changelog）
- 不出镜，纯文字图

---

## 12 个月里程碑（截至此处都达成则继续）

| 月 | MRR 目标 | 关键事件 |
|---|---------|---------|
| M1 | $30-100 | 上线 + 第一笔 |
| M2 | $200-500 | Web 端上线 + 韩漫支持 |
| M3 | $500-1500 | 关键决策点：< 20 付费就 pivot |
| M6 | $4K | 关键决策点：< $1K MRR 启动 Backup |
| M12 | $20-25K | 加 AI 推荐 + 拓中文网文 |

---

## 一直要做的事（每周 2 小时）

- 周一：看上周数据，决定本周重点
- 周三：处理用户反馈 + 修紧急 bug
- 周五：发 1 条 Twitter / 1 条 5ch / 1 条小红书更新
- 周日：写一周复盘到 PROGRESS.md

---

## 现金跟踪

| 月 | 支出 | 收入 | 净 |
|---|------|------|---|
| M1 | $149（Apple+域名+API）| $30-100 | -$50 |
| M3 | $50/月稳定 | $500 | +$450 |
| M6 | $80/月（用户多 API 多） | $4K | +$3920 |
| M12 | $150/月 | $24K | +$23850 |

---

## 失败诚实清单

如果 Week 4 完成后觉得这个项目没希望，问自己：

1. **是产品问题还是渠道问题？**
   - 5 个真实用户访谈
   - 看 Reddit / HN 评论的关键词

2. **wedge 还成立吗？**
   - 章节通知准确率（你的 vs ManGo）
   - 三语搜索是否真有需求
   - 漫画+轻小说+书三合一是否真痛点

3. **能修复吗？**
   - 如果是产品问题 → v1.1 改 → 第 2-3 月
   - 如果是渠道问题 → 第 5-8 周新渠道
   - 如果是 wedge 错 → pivot 到 Backup（AI Pixel Art）

4. **资源够撑多久？**
   - 看 PROGRESS.md 现金支出
   - $310/月 × 12 月 = $3,720
   - 到 6 月还没起色就启动 Backup

---

## End of Playbook

到这里你已经：
- ✅ Apple Developer 账号
- ✅ 真实可跑的 iOS App
- ✅ 真实付费用户
- ✅ Web 端配套（Day 31+）
- ✅ 流量+交易+积累 三合一闭环

剩下就是：**重复**。
重复 ASO 优化、重复内容营销、重复 v1.x 升级、重复用户反馈→改进。

---

回到 [00-overview.md](./00-overview.md) 看整体。

如果到 M6 还没起色，回到 [path-validation/](../research/path-validation/) 看 Backup 路径。
