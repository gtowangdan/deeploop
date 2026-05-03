# Apify Mercari Scraper 30 天实验 - 总览

> ⚠️ **本路径违反 §0 闭环原则**，作为 30 天验证实验，主路径是 [Manga Tracker](../../decisions/2026-05-03-implementation-guide.md)
> ⚠️ **如果时间冲突，Manga Tracker 优先**

---

## 30 天总览

| 周 | 目标 | Deliverable | 失败应对 |
|---|------|----------|---------|
| Week 1 | Build & Ship | Actor 上架 Apify Store + 跑通 50 次 demo | 反爬卡死 → 加 Residential proxy |
| Week 2 | Runs & SEO | 5+ 自然试用用户 + README 完整 | < 5 用户 → 优化 README + 关键词 |
| Week 3 | Paid Conversion | ≥ 1 笔 $50+ 付费 + 1 条 5 星评论 | 0 付费 → 价格降到 $2/1k |
| Week 4 | Decision | 决定继续 OR 关停 | $50 阈值决定 |

**总投入**：5-10h/周 × 4 周 = **25-35 小时**
**总现金支出**：Apify Pro $49 + Residential proxy $50 + 备用 $50 = **$149**

---

## 项目代号

**MercariSold-Comps**

---

## 周计划详细文档

- [Week 1: Build & Ship](./week1-build-ship.md) — Actor 开发 + 上架（Day 1-7）
- [Week 2: Runs & SEO](./week2-runs-seo.md) — 跑首批 + Apify Store SEO（Day 8-14）
- [Week 3: Paid Conversion](./week3-paid-conversion.md) — 第一笔付费（Day 15-21）
- [Week 4: Decision](./week4-decision.md) — 决策点（Day 22-30）

---

## 第 1 优先级（这个周末就做）

打开 [week1-build-ship.md](./week1-build-ship.md)，按 Day 1 步骤照做。**2 小时内完成**。

---

## 失败迹象 + 立即行动

| 时点 | 信号 | 立即做 |
|------|-----|------|
| Day 7 | Actor 跑不通（反爬卡死） | 加 Residential proxy；如仍不通 → 转 Yahoo Auctions Closed 单独 actor |
| Day 14 | < 5 用户试用 | 优化 README（加截图 + 5 个 use case）+ 加更多 SEO 关键词 |
| Day 21 | 0 付费 | 价格降到 $2/1k 试一周 |
| Day 30 | < $50 收入 | **关停，回 Manga Tracker** |

---

## 工具清单（开工前先准备好）

| 工具 | 用途 | 费用 |
|------|-----|------|
| Apify Pro Plan | Actor 部署 + Compute Units | **$49/月** |
| Apify Residential Proxy | 反爬 IP 轮换 | $50/月 add-on |
| Cursor Max | 写 TypeScript 加速 | 已订阅 |
| Claude Max | 关键词扩展 + README 写作 | 已订阅 |
| Apify CLI | Actor 部署 | 免费 |
| Crawlee（Apify 自家库） | 爬虫框架 | 免费 |
| Node.js 20+ | 运行环境 | 免费 |

---

## 关键判断（不要改）

- **不做 Mercari listings**（active listings），**只做 sold**（核心 wedge）
- **跨平台 comp**：Mercari sold + Yahoo Auctions Closed + Buyee
- **日语 keyword 自动扩展**（你的护城河）
- **不存任何 PII**（seller real name、地址等绝不存）
- **2s 间隔**（敬畏 Mercari ToS）
- **README 写英文**（buyer 都是英语 reseller）

---

## 与 Manga Tracker 时间分配

| 时间 | 投入 |
|------|------|
| 工作日晚上（Mon-Fri） | Manga Tracker 主线 |
| 周末上午 | Manga Tracker 主线 |
| **周末下午（4-6h）** | **Apify 实验** |

**绝不超过 10h/周**给 Apify。

---

## 接下来打开 [week1-build-ship.md](./week1-build-ship.md) 开始 Day 1。
