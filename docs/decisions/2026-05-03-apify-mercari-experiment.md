# Apify Mercari Scraper 30 天实验决策文档

> ⚠️ **本路径违反 deeploop §0 闭环原则**
> 作为短期赚钱实验，不作主路径
> 主路径仍是 [Manga Tracker](./2026-05-03-implementation-guide.md)

---

## 一句话讲清楚

**写一个 Apify 平台上的爬虫工具，专门帮全球 vintage / 日货 reseller 查 Mercari Japan 已售出商品的真实成交价格 + Yahoo Auctions 拍卖结果 + Buyee 现售价 三平台对比，按用量收费。**

---

## 这是个什么产品？（用故事讲）

### 想象一个真实买家

**Tom，32 岁，住在洛杉矶，Etsy 店主**。

他的生意：从 Mercari Japan 进口 vintage Levi's 牛仔裤、BAPE 卫衣、Hello Kitty 周边，加 3-5 倍价卖到 Etsy / eBay。

他的痛点：
- 每周要决定"这周扫什么货"
- 需要知道 Mercari JP 上某款 vintage Levi's **实际成交价**（不是挂牌价，是真正卖出去的价格）
- 他的日语零基础，关键词搜索能力差
- 现有工具：Mercari JP 自家"Price Search"功能**只对日本本土账号开放**，他被锁在外面
- Apify 上有几个 Mercari scraper，但**只抓在售（active），不抓已售（sold）**，对他没用

Tom 每月愿意花 $20-50 拿到这种数据，因为这能帮他决策每周 $5,000+ 的进货预算。

### 你的产品

Tom 在 Apify Store 搜 "Mercari Japan sold price"，搜到你的 Actor。

Tom 输入关键词 "vintage levi's 501 BIG E"，你的 Actor:
1. **自动扩展日语关键词**：リーバイス ビッグE / 66前期 / etc.（你的护城河）
2. 抓 Mercari JP **已售商品**最近 90 天的成交价（中位数 / 平均 / 价格分布）
3. 同时抓 Yahoo Auctions Closed 拍卖落槌价
4. 同时抓 Buyee 当前在售价
5. 输出：**统一表格**，每个商品一行，三平台数据并列

Tom 拿到数据 → 知道 BIG E 中位成交价 ¥18,000 → 决定预算 → 进货 → 转手 $300 一条 → 月入 $4,000 净利。

Tom 每月跑 5,000 行查询 = 付你 $25。

---

## 为什么会赚钱？（具体推理）

### 赚钱的数学

```
月收入 = (月活用户) × (每用户月查询量) × $5/1000 × 80%（Apify 抽 20%）
```

### 你的版本怎么填

**保守估算**：
- 30 天后：5 个付费用户 × 平均 2,000 行/月 × $5/1000 × 80% = **$40/月**
- 90 天后：15 个付费用户 × 平均 3,000 行/月 × $5/1000 × 80% = **$180/月**
- ceiling：30 用户 × 5,000 行 × $5/1000 × 80% = **$600/月**

**为什么我相信这数字**：
- Apify 现有 Mercari Actor (fatihtahta) **11 MAU、5 星评分**——证明这个 niche 有真实付费
- 你做的是他没做的 sold + 跨平台 comp，**召回率 + 数据深度都高 2-3x**
- 你的日语母语让 keyword expansion 更准
- $5/1000 比 fatihtahta 的 $3.99 贵 25%，但价值差 2-3 倍

### 谁会付钱？

- 全球 vintage / Y2K 周边 reseller（最大群体）
- 日本动漫 dropshipper
- 跨境运营外包公司
- Buyee 类竞品做内部数据 feed

这些人**已经在为类似工具付钱**（fatihtahta 已有 2 条 5 星评论 = 真实付费）。

---

## 为什么大公司不做？

- **Mercari 自家 Price Search**：只对日本本土账号开放（**这就是缺口**）
- **大型数据公司（SimilarWeb, SensorTower）**：做品牌级别数据，不做单品 SKU 级
- **传统爬虫服务（Bright Data, Apify 自家）**：做通用 actor，不做 vintage reseller niche
- **Mercari 自己**：不会卖竞争数据给海外 reseller（伤自家市场）

---

## 你具备什么？缺什么？

### ✅ 你有的（直接用）

| 条件 | 你的水平 | 这个项目需要 |
|------|---------|------------|
| Node.js / TypeScript | 20 年全栈 | Apify Crawlee 是 Node 库 |
| **日语 N2** | 母语级别理解 | 关键词 expansion 是核心 wedge |
| **中文母语** | 母语 | 跨境理解（中国转运 / Buyee 用户） |
| Cursor Max | 已订阅 | 写爬虫加速 5x |
| 反爬经验 | 全栈通用 | Mercari 反爬中等 |
| Apify 平台理解 | 已读过文档 | 上手快 |
| 个人时间 | 5-10h/周 | 第 1 周 8h，之后 2-3h |
| 月预算 | $150-350 | 实际花 $99-150 |

### ⚠️ 你需要现学的（≤ 1 周）

| 技能 | 学习成本 | 学习方式 |
|------|---------|--------|
| Apify Crawlee 库 | 1-2 天 | [官方教程](https://crawlee.dev/) + Cursor 加速 |
| Apify CLI + actor.json | 半天 | [Apify SDK docs](https://docs.apify.com/sdk/js/) |
| Apify Store 上架流程 | 1 天 | 实操 |
| Mercari JP 反爬应对 | 1-2 天 | 试错 + Residential proxy |

### ❌ 你不具备但**这个项目不需要**

- ~~不需要营销~~（Apify Store 内置搜索）
- ~~不需要英文 Twitter~~（README 写好+少量 Reddit 软发即可）
- ~~不需要个人 IP/出镜~~
- ~~不需要付款集成~~（Apify 平台代收）

---

## 风险表

| 风险 | 概率 | 对冲 |
|------|-----|------|
| **Mercari ToS DMCA takedown** | 中 | UA 标识 Apify + 2s rate limit + 不存 PII；Apify 平台给一层缓冲 |
| **反爬升级，actor 失效** | 中 | 加 Residential proxy ($50/月 add-on)；监控 actor health |
| **30 天没人付费** | 中 | 这就是实验目标——验证假设。$150 损失可承受 |
| **fatihtahta 抢做 sold + 跨平台** | 低 | 他土耳其开发者，做不到日语 keyword expansion |
| **Apify 平台政策变（降分成）** | 低 | 80/20 多年稳定 |

---

## 失败迹象（提前止损）

### Day 14 检查
- < 5 个用户试用过你的 actor → ASO 优化（README + 关键词 + 截图）

### Day 21 决策点（最关键）
- 总 users < 10 → **NO-GO，立即停**
- 试用过没付费 → 价格降到 $2/1k 试一周
- < $50 收入 → **D22 起停止开发，专心 Manga Tracker**

### Day 30 总评
- ≥ $100 + 1 个 5 星评论 → 90 天扩到 $500 MRR
- $50-$100 → 加第二个 actor（Buyee 独立 actor）
- < $50 → 关停，资源回 Manga Tracker

---

## 与主路径 Manga Tracker 的协同

实验期间，**绝不冲击 Manga Tracker 主线**：
- Manga Tracker 投入 15-18h/周
- Apify 实验 5-10h/周（**主要在周末**）
- 总投入 ≤ 25h/周

**积极协同点**：
- 学到的 Apify 爬虫技术 → Manga Tracker 后端章节抓取也能用
- Mercari + Yahoo + Buyee 的数据源经验 → Manga Tracker 加楽天オークション 漫画抓取
- Apify 实验失败也是积累（懂了 Apify 模式 = 未来不再误推荐）

---

## Q&A

### Q：30 天 $100-300 真的现实吗？
A：现实但不保证。Apify 现有 Mercari fatihtahta 11 MAU × $4/1k × 平均 3000 行 = ~$130/月（粗算）。你做的是 sold + 跨平台 = 优于他，但要靠 README + ASO 慢慢爬上来。**第 1 个月 $40-100 是现实，$300 是上限**。

### Q：Mercari 真的会封我吗？
A：Apify 平台已有 5+ 个 Mercari actor 在跑，Mercari **没有公开起诉过**。但他们可以随时封 IP。对策：
- 用 Apify Residential Proxy（轮换 IP）
- 2s 间隔（不冲流量）
- 不存 seller PII（敬畏个人情報法）
- 接 Apify 平台缓冲（投诉先到 Apify，不到你）

### Q：我不懂 reseller 圈子，能做这产品吗？
A：能。你不需要懂 reseller，只需要懂数据。**你的角色是数据供应商，不是 reseller**。
关键：README 写得清楚（用 fatihtahta 的 README 做参考），让 reseller 自己看懂。

### Q：第一笔付费从哪来？
A：3 条最可能路径：
1. **Apify Store 自然搜索**（用户在 Apify 内搜 "Mercari sold" 找到你）
2. **Reddit r/Flipping / r/Mercari 软发帖**（"我做了个免费 demo dataset，想要的报关键词"）
3. **Buyee Discord** / Yahoo Japan Auctions 跨境圈

### Q：如果 Day 21 还没收入怎么办？
A：CLAUDE.md 已经写好失败应对：
- 价格降到 $2/1k 试一周
- 或加新功能（用户要的 seller location/shipping cost）
- D22 仍 < $50 → **认输，停止，全力 Manga Tracker**

不要心理战拖到 60 天。30 天实验就是 30 天。

### Q：和 Manga Tracker 比，哪个更重要？
A：**Manga Tracker 是主路径，Apify 是实验**。
- Manga Tracker：12 月 $4-10K MRR + 闭环资产 + 长期复利
- Apify：30 天 $100-300 + 学技术 + 验证假设

如果时间冲突，**Manga Tracker 优先**。

---

## 立即可做的 1 件事（这周末）

打开 [docs/playbook/apify-mercari-experiment/00-overview.md](../playbook/apify-mercari-experiment/00-overview.md)，按 Day 1 注册 Apify Pro plan + 跑通 fatihtahta 的 actor 看输出格式。

**2 小时内能做完。**

如果做完后觉得"我没动力理解 reseller / 不想做不是自己用户的产品"——立即停，回 Manga Tracker。

---

## 数据来源

详见 [research/path-validation/07-apify-mercari-experiment.md](../research/path-validation/07-apify-mercari-experiment.md)
