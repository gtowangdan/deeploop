# 最终方向决定：漫画+轻小说追更 App

> 决定日期：2026-05-03
> CLAUDE.md 版本：v1.6
> 决策方法：§8.1.12 四维调研 × 2 个并行 agent，最终对决

---

## 决定：GO

**主路径**：漫画 + 轻小说 + 普通书三合一追更 App，iOS 原生 + Web 配套，主战场日本 + 全球华人/英语圈双语市场

**Backup 路径**（仅 Path B 失败时启动）：AI Pixel Art / 2D Sprite 生成器（Aseprite 集成）

---

## 核心定位（一句话）

> "the reading tracker that handles manga, light novels, and books in one place — with chapter-level alerts and JP/EN/CN trilingual support"

---

## 单一 wedge（差异化护城河）

1. **漫画 + 轻小说 + 书三合一**
   - Bookly 只做书（$60K/月）
   - MangaTime/ManGo 只做漫画
   - ブクログ/読書メーター 不做漫画追更（漫画 metadata 体系完全不同）
   - 没有任何竞品做这三合一

2. **章节级别追更通知**
   - ManGo 用户："anime notification feature **does not work properly about 80% of the time**"
   - MangaTime 用户："**wished there was a countdown to next chapter release**"
   - **核心未满足痛点**

3. **JP/EN/CN 三语 metadata**
   - 所有独狼级竞品都是单语
   - 用户的中文母语 + 日语 N2 = 直接护城河

---

## 闭环三问打分

- **A 流量：9/10** —— ASO + 章节通知病毒传播 + Web SEO，全球三语市场覆盖
- **B 交易：8/10** —— Apple Small Business Program 15% + Web 端美国区 0 抽成 + RevenueCat 跨平台
- **C 能用：9/10** —— 用户最强项 iOS + AniList/MAL/楽天 API 都开放 + 不涉及法规雷区

---

## 真实竞品 Top 5

| App | 营收估算 | 弱点（你的进入点）|
|---|---|---|
| **Bookly (TBR)** | **$60K/月**，4 万下载/月（appstorespy 2024） | 不做漫画/轻小说，只英文书 |
| **StoryGraph** | ~$200K/月（4M users × $4.99/月 × 1% 转化） | 英文圈，无章节追更，无日漫 |
| **MangaTime** | 估 $3-8K/月 | 只漫画无书；通知不可靠 |
| **ManGo** | 估 $2-5K/月 | 通知 80% 失败 |
| **ブクログ**（Web 主体） | 200 万 MAU 但 freemium 弱 | 不做漫画连载追更，无英文 |

**3 个 solo dev 成功对标**：
- Bookly（罗马尼亚团队，$60K/月）
- Habit Pixel（solo，8 个月 $1K MRR）
- 30-app portfolio（$25K MRR 验证 iOS 独狼模型）

---

## 为什么大厂不做（用户进入空间）

- **AniList**：开源社区，没产品化动力
- **MAL（Kadokawa 资产）**：长年不更新（用户原话："updates lag behind"）
- **ブクログ/読書メーター**：不做漫画追更（漫画 metadata 体系和书完全不同，做需要重建）
- **Apple Books / Kindle / LINE 漫画**：做生态闭环（卖内容），不做跨平台追踪

→ **没有大厂 + 现有 indie 竞品都做不到三合一+三语+章节通知** = 用户能切的真实空间

---

## 30 天首次收入路径

### Week 1-2：MVP 核心
- iOS 原生 + Cloudflare Workers 后端
- 接 AniList GraphQL（漫画/轻小说）+ 楽天ブックス API（日本书）+ Open Library（英文书）
- 三个 tab：閲読中 / TBR / 完読
- Push 通知章节更新（**核心 wedge**）

### Week 3：Web 配套
- Next.js + 同一后端，sync via iCloud + 邮箱
- 公开页 SEO：每本作品一个 SEO 落地页（"〇〇 最新 chapter when"）

### Week 4：上架 + 冷启动
- **ASO 关键词**：漫画 記録 / manga tracker / light novel / 読書記録 / book log
- **主推日本区**（关键词竞争 < 美国），CPP 三套：日本/中国港台/英文
- **冷启动 4 渠道**：
  - r/manga + r/lightnovels（软发帖 Show HN 风格）
  - 5ch 漫画板 + Twitter #漫画記録
  - 小红书"读书记录 App"标签
  - Hacker News Show HN

**100 装机 = 4 渠道 × 25 个，14 天可达**
**第一付费 = 100 装机 × 6% ≈ 6 个，30 天可达**

---

## 12 个月行动清单

| 月 | 目标 | 关键动作 |
|---|---|---|
| M1 | MVP + 100 装机 | iOS + Web + AniList/楽天 集成 |
| M2 | 1K 装机 / 5 付费 | 加章节通知，日本 ASO 优化 |
| M3 | 5K 装机 / 50 付费（$200 MRR） | 加 Widget + Live Activity（iOS 强项） |
| M4-6 | 1K 付费（$4K MRR） | Claude API 做"你可能喜欢"AI 推荐 |
| M7-9 | 3K 付费（$12K MRR） | Web SEO 上量，日 100 自然访问 |
| M10-12 | 6K 付费（$24K MRR） | 横向扩 韩漫（네이버웹툰）/ 中文网文 |

**12 月目标**：$20-25K MRR（Bookly $60K/月的 1/3，保守可信）

---

## 起步预算（$310/月，< $350 安全）

| 项目 | 月支出 |
|------|------|
| Apple Developer | $8（$99/年摊） |
| Cloudflare Workers + D1 + R2 | $5 |
| Claude API（推荐 + 内容总结） | $50 |
| OpenAI（备份） | $20 |
| RevenueCat | $0（< $10K MRR 免费） |
| Mailgun（章节通知备路） | $15 |
| 域名 + Vercel | $20 |
| ASO 工具（Astro / AppFollow lite） | $40 |
| 备用 buffer | $100 |
| **合计** | **$258** + buffer |

---

## 最大 3 个风险 + 对冲

| 风险 | 概率 | 对冲方案 |
|------|------|---------|
| **AniList API 政策变化或限流**（最高） | 中 | 同时接 MAL + Kitsu + 楽天 + 自建 metadata 兜底；缓存所有数据到 D1 |
| **Apple 拒审**（漫画版权擦边） | 中低 | **绝不内嵌阅读器**，纯追踪（MangaTime/Bookly 都这样过审）；漫画封面用官方授权图源（楽天/AniList CDN） |
| **ブクログ 反扑做漫画功能** | 低 | ブクログ 是 Web 老厂，移动端慢；锁定 Widget + Live Activity + 章节通知 这些 iOS-native 体验做防御 |

---

## 失败迹象（提前止损）

- **M3 末 < 20 付费订户**：wedge 不对，立即调整定价或核心功能
- **M6 末 MRR < $1K**：渠道全失效，启动 Backup（AI Pixel Art）
- **AniList + MAL 双 API 限流**：转向纯日本市场用楽天 API 兜底
- **ブクログ 出漫画追更**：差异化消失，立即横向扩到韩国（네이버웹툰）

---

## Backup 路径：AI Pixel Art / 2D Sprite 生成器

仅在 Path B 失败迹象触发时启动。

**核心定位**：Aseprite 插件 + Tileset 一致性 + Sprite Sheet 帧一致性 + Palette Lock

**对标**：PixelLab.ai $50/月、Scenario.com $45/月

**12 月目标**：$15-25K MRR

详细分析：[../research/path-validation/](../research/path-validation/)（Path A Photo AI 模式调研）

---

## 立即可做的 3 件事（这周）

1. **本周末**：注册 Apple Developer（$99）+ 注册域名 + 接 AniList GraphQL 跑通"输入作品名 → 拉到章节列表"
2. **下周**：iOS MVP 起手（三个 tab + AniList 集成），目标 7 天写出可用 demo
3. **下下周**：Web Next.js 同后端 + Cloudflare Workers 部署，章节通知逻辑跑通

---

## 数据来源

完整调研报告与数据：
- [Path A 调研](../research/path-validation/) - Photo AI 模式 / AI Pixel Art
- [Path B 调研] - HabitKit 模式 / Manga Tracker（详见本文档引用）

关键 URL：
- [Bookly App Store](https://apps.apple.com/us/app/bookly-book-tracker/id1085047737)
- [Bookly 营收数据 - AppstoreSpy](https://appstorespy.com/ios-apple-store/1085047737-trends-revenue-statistics-downloads-ratings)
- [AniList GraphQL API](https://anilist.co/graphiql)
- [楽天ブックス API](https://webservice.rakuten.co.jp/documentation/books-total-search)
- [ManGo App Store](https://apps.apple.com/us/app/mango-anime-manga-tracker/id1604385869)
- [MangaTime App Store](https://apps.apple.com/us/app/mangatime-manga-tracker/id6740176167)
- [Top 15 Most Profitable Indie Apps - Market Clarity](https://mktclarity.com/blogs/news/indie-apps-top)
- [読書メーター vs ブクログ 比較](https://www.digital-dokusho.jp/magazine-hikaku/bookmeter-booklog/)

---

## 决策签名

按 CLAUDE.md v1.6 §8.1.12 四维调研标准产出。
两个并行 agent 各自验证一个 Path，每个 agent 内部对决 8-13 个候选 niche。
最终 Path A vs Path B 12 维对决，Path B 8 项胜出。

**这次推荐基于真实数据，不是凭感觉。**
