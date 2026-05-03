# Week 4: Decision（Day 22-30）

> **本周目标**：决定继续 Apify 实验 OR 关停 + 全力 Manga Tracker
> **总投入**：3-5 小时（监控 + 决策，不再大开发）

---

## Day 22-26（工作日晚监控，每天 30 分钟）

### Step 22.1：每天 5 分钟看数据

打开 Apify Console → Actor → Analytics：
- Daily users
- Daily runs
- Daily revenue（关键）

记录到 `PROGRESS.md`：
```markdown
## Day 22
- Users: 12 (+2 from Day 21)
- Runs: 156 (+34)
- Paid: $45 (+$0)
- Reviews: 1 (5 star)

## Day 23
...
```

### Step 22.2：处理紧急 bug（每天 25 分钟）

预期常见 bug：
- Mercari 偶尔反爬升级 → actor 跑空
- Yahoo Auctions Closed 页面结构改 → 解析错
- Buyee 限流 → 部分商品抓不到

应对：
- 看 Apify Console → Logs
- 让 Cursor 修最影响付费用户的 bug
- `apify push`

**绝不开新功能**。本周是决策周，不是开发周。

---

## Day 27-29（周末 + 工作日，3 小时）：Decision Gate

### Step 27.1：用户访谈（90 分钟）

挑 3 个最活跃 user（包括付费的），私信：

```
Hey [username],

Quick question — would you mind 5 mins of your time?

Trying to decide whether to keep building this actor or shift focus.
Three quick Q's:

1. What problem are you solving with this tool?
2. What would make you cancel / churn?
3. If price doubled to $10/1k, would you still use it?

Just reply in any order. No pressure if too busy.
```

预期回应：
- "I use it for [specific niche]" → 给你方向
- "I'd churn if [condition]" → 给你保留策略
- 价格弹性测试

### Step 27.2：盘算总账（60 分钟）

填这个表：

| 项 | 值 |
|---|---|
| **总收入（Day 1-30）** | $___ |
| Apify 抽 20% | -$___ |
| Apify Pro plan | -$49 |
| Residential Proxy add-on | -$___（用了多少）|
| **净收入** | $___ |
| **总投入时间** | ___ 小时 |
| **时薪** | $___ / 小时 |

如果时薪 < $10 = 这个实验经济上不划算
如果时薪 ≥ $20 = 值得继续
如果中间 = 看 Day 30 决策表

### Step 27.3：90 天预测（30 分钟）

基于 Day 30 数据线性预测：

| 30 天数据 | 60 天预测 | 90 天预测 | 决定 |
|---------|---------|---------|-----|
| 1-3 付费 / $50-150 | 5-10 / $200-500 | 10-20 / $500-$1000 | **继续小投入** |
| 0-1 付费 / $0-50 | 1-3 / $50-150 | 3-5 / $150-300 | **关停** |
| 5+ 付费 / $200+ | 15+ / $700+ | 30+ / $1500+ | **加资源** |

---

## Day 30（最终决策日）

### 决策矩阵

| 30 天数据 | 决定 | 行动 |
|---------|-----|------|
| **≥ $200 收入 + 3+ 付费** | ✅ 继续 | 第二个月加 1 个 actor（Buyee 单独 actor） |
| **$50-$200 + 1-3 付费** | ⚠️ 维持 | 不再大开发，每月 1h 维护，被动收入 |
| **$0-$50 + 0-1 付费** | ❌ 关停 | 关闭 Pro plan，actor 留公开（不下架但不维护）|

### 决定后立即做

**继续**：
- 复用 Mercari scraper 代码做 Buyee 独立 actor（Day 31-37）
- 价格 $4/1k（Buyee 量大单价低）

**维持**：
- Apify Pro plan 降到 Free tier（如果可以）
- 留 README 链接到主路径 Manga Tracker landing page（间接引流）

**关停**：
- Apify Console → Settings → Cancel Pro plan
- Actor 保持公开（被动 free credit user 偶尔会跑，不维护）
- 把代码推到 GitHub 公开仓库（学习资料）
- **下午开始全力 Manga Tracker**

---

## 复盘文档（决策后 1 周内写）

写到 `docs/decisions/2026-XX-XX-apify-experiment-results.md`：

```markdown
# Apify Mercari 实验结果（30 天）

## 数据
- 净收入：$___
- 时薪：$___
- 总用户：___
- 付费用户：___

## 学到什么（带回 Manga Tracker 的资产）
- Apify 平台机制（如何上架 / 计费 / 评分）
- Mercari / Yahoo Auctions 反爬技术（爬虫工程经验）
- 跨平台数据 unify 设计模式
- README + ASO 写作经验
- Reddit / Discord cold-start 触达方式

## 决定
[继续 / 维持 / 关停]

## 反思
- 闭环原则的代价：[具体感受]
- 时间冲击 Manga Tracker 多少：[具体小时]
- 下次再做实验之前：[原则]
```

---

## 与 Manga Tracker 主路径的关系

**最终一定要回 Manga Tracker**。Apify 实验不论成败都是过渡：

| Apify 结果 | Manga Tracker 优先级 |
|----------|------------------|
| 关停 | 100% 全力 |
| 维持 | 95% 主力（5% Apify 维护） |
| 继续 | 70% 主力（30% Apify 扩展，但严格限时） |

**绝不允许 Apify 吞掉 Manga Tracker 时间**。CLAUDE.md §0 闭环原则是项目核心。

---

## End of Apify Playbook

到这里你已经完成 30 天实验，知道了：
- ✅ 是否能在不出镜不营销的情况下从 Apify 赚到钱
- ✅ Apify 平台的真实规则（不是看文档，是亲身做完）
- ✅ Mercari + Yahoo + Buyee 反爬经验（带回 Manga Tracker 用）
- ✅ 闭环原则的代价（亲身体会"为什么平台依赖是死路"）

无论结果如何，**这 $149 + 30 小时**是项目积累，不是浪费。

---

## 下一步

回 [Manga Tracker week1-tech-validation.md](../week1-tech-validation.md)（如果还没开始）
或继续 [Manga Tracker week N](../week2-ios-mvp.md) 当前阶段。

**永远记住**：Manga Tracker 是主路径，Apify 是旁支。
