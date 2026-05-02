# 纯技术变现：靠 Claude Max + Cursor Max 放大产能赚钱的路径

> 调研日期：2026-05-02
> 用户画像：20年全栈+iOS、日本华人、不善英文推广、不愿出镜、每周15-20h、Claude Max + Cursor Max 订阅、预算 $150-350/月
> 核心需求：**纯技术杠杆 —— 平台分发流量，不需要营销，不需要个人品牌，拼技术和效率**

---

## 一句话答案

**主仓位走 [Apify Store](https://apify.com/store)（爬虫即 Actor），副仓位做 Chrome 扩展，长期实验仓玩 [Algora bounties](https://algora.io/bounties) 验证 AI 加速假设。**

这个组合的特点：
- ✅ **平台算法替你分发流量**，不需要英文 Twitter/出镜
- ✅ **AI 放大产能 5-10 倍**，每周 15-20h 完全够
- ✅ **预算够用**：$150-350/月覆盖一切（Claude Max 和 Cursor Max 已包月）
- ✅ **验证速度快**：1-2 周可以看到第一笔收入

---

## 全部候选路径打分（残酷诚实）

| 渠道 | AI放大潜力 | 不需营销度 | 综合 | 状态 |
|------|----------|----------|------|------|
| **Apify Store（爬虫）** | 10 | 9 | **9.5** | ⭐⭐⭐ 主仓位 |
| **Chrome 扩展** | 9 | 9 | **9.0** | ⭐⭐⭐ 副仓位 |
| **MQL5 Market（量化）** | 9 | 9 | 9.0 | 长期实验仓（需对量化有兴趣） |
| **TradingView Paid Spaces** | 9 | 7 | 8.0 | 同上 |
| **iOS App Store（纯 ASO）** | 7 | 7 | 7.5 | 备选（你有 iOS 经验） |
| **RapidAPI** | 9 | 6 | 7.5 | 备选 |
| **Algora.io 悬赏** | 9 | 6 | 7.5 | 即时现金流验证 |
| **Mac App Store + Setapp** | 6 | 7 | 6.5 | 长期被动 |
| **Polar.sh 悬赏** | 8 | 6 | 7.0 | 同 Algora |
| **JetBrains Marketplace** | 6 | 7 | 6.5 | niche |
| **Figma Plugin** | 5 | 6 | 5.5 | 受众小 |
| **AI 内容站 + 广告** | 6 | 5 | 4.0 | ❌ HCU 后已死 |
| **GitHub Sponsors** | 5 | 3 | 4.0 | ❌ 依赖个人IP |
| **VS Code Extension** | 4 | 7 | 4.0 | ❌ 无官方付费机制 |
| **Raycast Store** | 3 | 7 | 3.0 | ❌ 无付费机制 |
| **Replit Bounties** | - | - | - | ❌ 2025/9 已停服 |
| **Shopify App Store** | 5 | 3 | 4.0 | ❌ 需英文运营客服 |
| **WordPress Plugin** | 4 | 5 | 4.5 | ❌ 红海 + 老品牌垄断 |

---

## 主仓位：Apify Store（爬虫即 Actor）⭐⭐⭐

### 为什么是它

**真实数据（带来源）**：
- 头部独立创作者 **$10K+ MRR**（[Apify 官方](https://apify.com/partners/actor-developers)）
- **ParseForge 案例**：6个月发布 124 个 Actor、1.9K 用户、单 Actor 最高 $1K MRR、单月最大客户 $8K（[Apify Blog](https://blog.apify.com/parseforge-actor-factory/)）
- 抽成：**80/20**（开发者拿 80%）
- 平台 50K+ MAU 还在增长

### 为什么完美匹配你

| 你的优势 | Apify 路径要求 | 匹配 |
|---------|-------------|------|
| 20 年全栈 | Node.js/Python 写爬虫 | ✅ 过剩 |
| Claude Max + Cursor Max | "识别网站 → 写爬虫 → 处理反爬 → 部署"周期从一周压到几小时 | ✅ AI 红利最大 |
| 日本华人 | **食べログ/SUUMO/メルカリ/楽天/価格.com 日本本地数据** = 英语圈对手做不动的护城河 | ✅ 这是核心杠杆 |
| 不善英文推广 | Actor 文档用 AI 写 + Apify 内部 SEO 替你分发 | ✅ |
| 不愿出镜 | 平台算法分发，无需个人品牌 | ✅ |
| 每周 15-20h | ParseForge 6 个月做 124 个，你每周做 1-2 个 Actor 节奏轻松 | ✅ |
| 预算 $150-350/月 | Apify 平台代理费用从用户付的 $ 里扣，开发者无需垫付基础设施 | ✅ |

### 核心赚钱逻辑

```
用户搜"我要爬 LinkedIn 公司列表" → Apify 内部搜索/Google 搜索匹配你的 Actor
→ 用户运行 Actor → 按 results 数量付费给你
→ Apify 平台抽 20%，你拿 80%
```

**关键洞察**：
- **不需要你做任何营销** —— Apify 内部就是搜索引擎，用户主动找
- 定价 $0.5-$5 / 1000 results，被动收入
- 一个 Actor 写完后基本不用维护（除非目标网站改版）
- **多个 Actor 叠加** = 累积 MRR

### 12 个月行动清单

#### 第 0-1 月：环境 + 第一个 Actor
- [ ] 注册 [Apify 账号](https://console.apify.com/sign-up)（免费）
- [ ] 跑通官方教程 Actor（1-2 天）
- [ ] **选第一个目标网站**：建议从 **日本网站**起步（メルカリ、食べログ、SUUMO 之一）
- [ ] 用 Cursor Max 写第一个 Actor（**预期 2-3 天完成**，靠 AI 加速）
- [ ] 发布到 Apify Store，定价 $1/1000 results
- [ ] **第一个月目标**：1 个 Actor 上架

#### 第 2-3 月：节奏化生产
- [ ] **每周 1-2 个 Actor**，目标月底总数 5-10 个
- [ ] 关键词战略：选 Apify Store 内**搜索量大但供给少**的目标网站
- [ ] 优先做"日本本地数据 + B2B 数据"，避开 LinkedIn/Twitter（红海）
- [ ] 候选目标清单：
  - 日本企業数据库（東商信用録、企業ナビ）
  - 不动产（SUUMO、HOME'S、AtHome）
  - 招聘（リクナビ、マイナビ、Indeed Japan）
  - EC（楽天、Amazon JP、Yahoo!ショッピング）
  - 美食（食べログ、ぐるなび、Retty）
- [ ] **第 3 月目标**：5-10 个 Actor，首批 MRR $100-$500

#### 第 4-6 月：深耕 + 优化
- [ ] 看哪些 Actor 出单 → 围绕它做"系列"（如食べログ Actor 火 → 加 ぐるなび、Retty）
- [ ] 加 README 教程（用 Claude 写英文 + 你的日语版）
- [ ] 关注 Actor 评论，及时修反爬变化
- [ ] **第 6 月目标**：15-25 个 Actor，MRR $1K-$3K

#### 第 7-9 月：垂直化 + 数据集
- [ ] 把热门 Actor 的输出转成"现成数据集"卖（一次性下载）
- [ ] 上 [Datarade](https://datarade.ai) / Kaggle 同步引流
- [ ] 找 5 个企业客户私聊（Apify 平台内消息），做定制版
- [ ] **第 9 月目标**：MRR $3K-$5K

#### 第 10-12 月：组合策略
- [ ] 总 Actor 数 30-40 个
- [ ] 找出 Top 5 营收来源 → 做成"Pro 版"加价
- [ ] 考虑发布"Actor 套件"（如"日本不动产全套"打包）
- [ ] **第 12 月目标**：MRR $5K-$10K

### 风险与对策

| 风险 | 概率 | 对策 |
|------|------|------|
| 目标网站改版反爬 | 中 | 每月维护时间预留 20%；用 Apify 自带反爬基础设施 |
| 选错目标无人买 | 高 | 第 1-3 月撒网式做 5-10 个，看哪个出单再深耕 |
| Apify 平台政策变化 | 低 | 平台对开发者友好，80% 分成已经稳定多年 |
| 法律风险（爬公开网站） | 低 | 只爬公开数据，不爬登录后内容；每个 Actor 加 ToS 说明 |

### 立即可做的 3 件事

1. **本周末**：注册 Apify，跑通 1 个官方教程 Actor
2. **下周**：选 1 个日本网站，用 Cursor Max 写第一个 Actor
3. **本月内**：上架，定价 $1/1000 results，看是否有第一个用户

---

## 副仓位：Chrome 扩展 ⭐⭐⭐

### 为什么是它

**真实赚钱案例（带来源）**：
- **GMass**（Gmail 群发）：$130K-$200K MRR
- **Eightify**（YouTube AI 摘要）：$45K/月、50% 毛利
- **Easy Folders**（ChatGPT/Claude 文件夹）：$3.7K MRR、上线 6 个月（[Indie Hackers](https://www.indiehackers.com/product/easy-folders/6-months-post-launch-my-chrome-extension-has-hit-3-700-in-mrr-and-42-000-in-total-revenue--O3qs28VAnAkcJw0j--M)）
- **Tailscan**（前端审查工具）：$30K ARR、95% 毛利

### 当前窗口（重要）

- MV3 已强制（2024 全面、2025/06 移除所有 MV2 残留）
- **大量旧扩展开发者懒得迁移，留下空位**（[Indie Hackers 机会帖](https://www.indiehackers.com/post/software-opportunity-thousands-of-chrome-extensions-are-about-to-disappear-85DQAl9yaLglihq0kkkP)）
- AI 类扩展是当前最强风口

### 3 个最值得做的方向

#### 方向 1：AI 平台增强（Easy Folders 模式）
- 寄生在 Claude / ChatGPT / Gemini 之上
- 做"提示词管理 / 文件夹组织 / 批量导出 / 历史搜索"
- Easy Folders 6 个月做到 $3.7K MRR 已证明可行

#### 方向 2：日本本地服务增强（你的护城河）
- 楽天/Amazon JP/メルカリ 比价
- 価格.com 自动跟踪
- freee/MoneyForward 自动整理收据
- 日本招聘网站（Wantedly、リクルート）自动填充
- **几乎没有竞争**

#### 方向 3：开发者工具
- JSON/YAML 美化、API 调试
- Tailwind 检查器（Tailscan 模式）
- Git 工具增强
- API key 管理

### 12 个月行动清单（精简版）

| 阶段 | 时间 | 目标 |
|------|-----|------|
| 起步 | 第 1 月 | $5 注册 Chrome 开发者 + 第一个扩展上线（用 ExtensionPay 集成支付）|
| 验证 | 第 2-3 月 | 跑 100 装机量，验证有人愿意付费 |
| 增长 | 第 4-6 月 | freemium 转付费率优化，目标 MRR $500-$1K |
| 扩展 | 第 7-9 月 | 第二个扩展（同主题/不同平台），MRR $1K-$3K |
| 矩阵 | 第 10-12 月 | 3-5 个扩展组合，MRR $3K-$5K |

### 立即可做的 1 件事

**用 1-2 周做一个 "Claude 提示词管理器"扩展**：
- 你每天用 Claude，痛点你最清楚
- 上 Chrome Store + Product Hunt + Reddit r/ClaudeAI
- 这是验证整套流程最快的练手项目

---

## 长期实验仓：Algora.io 悬赏（验证 AI 加速假设）

### 为什么放在这里

- **即时现金流**：单条 bounty $50-$5000，1-2 周可拿到第一笔
- **零售门槛**：不需要发布产品，看到喜欢的 issue 直接做
- **AI 加速最大场景**：Claude Code 直接读 issue + repo 自动出 PR，**20年经验+AI 完成普通贡献者2-3天的活只要几小时**

### 真实数据

- Algora 累计支付 $65K（2023 数据，仍在增长）
- 头部贡献者一年 $20K-$50K
- 单条 bounty 中位数 $200-$500

### 怎么做

1. **本周**：注册 [Algora.io](https://algora.io/bounties) + 关联 GitHub
2. **盯 5-10 个活跃悬赏 repo**：Tembo、Twenty、Million.js、Cal.com、Trigger.dev
3. **用 Claude Code 一晚做 1-2 个中等 issue**（$200-$500 段位）
4. **目标**：第一个月赚 $500-$1000，验证"AI 放大产能能不能变现"

### 注意

- PR 描述、issue 沟通需要英文（但都是技术词，AI 翻译够用）
- 认领后被 maintainer 接受率 30-50%（高竞争）
- **不能当主路径**，但**最适合验证 AI 是否真能放大你的产能**

---

## 已排除的路径（明确告诉你为什么不推荐）

### ❌ AI 内容站 + 广告变现（HCU 后已死）

- 2024 年 3 月 Google HCU 后，独立站流量损失 30-90%
- 2025 年全球 publisher Google 流量下降 33%
- AI Overviews 出现的查询 zero-click 率 83%
- Mediavine/Raptive 主动拒绝 AI 内容站（2025 年 13% 申请因 AI 内容被拒）
- **结论**：纯做这条路 = 死路。但**日语技术 newsletter（beehiiv）**是变种，可作为副线

### ❌ Replit Bounties（已停服）

2025/9/6 关停（[HN 讨论](https://news.ycombinator.com/item?id=44643875)）

### ❌ GitHub Sponsors（依赖个人IP）

- Caleb Porzio $112K/年靠 Laravel/Livewire 维护者身份 + Twitter
- 与"不出镜不品牌"画像完全冲突

### ❌ VS Code Extension（无官方付费机制）

Microsoft 没内置付费，必须自建支付系统（[GitHub Issue 111800](https://github.com/microsoft/vscode/issues/111800)）

### ❌ Raycast Store（无付费机制）

截至 2025/2026，无官方扩展付费分成

### ❌ Shopify App Store（需英文运营）

天花板高（顶 25% $14K/月）但**商家支持是日常英文沟通**，与画像不符

### ❌ HackerOne 安全悬赏（技能错位）

需要专精 web 漏洞挖掘，与全栈/iOS 经验不直接对口

---

## 你的最优组合策略

### 主线 + 副线 + 验证线 三仓制

```
主线：Apify Store（每周 12h）
  ├── 第 1 月：1 个 Actor 上架，验证流程
  ├── 第 3 月：5-10 个 Actor，MRR $100-$500
  ├── 第 6 月：15-25 个 Actor，MRR $1K-$3K
  └── 第 12 月：30-40 个 Actor，MRR $5K-$10K

副线：Chrome 扩展（每周 6h）
  ├── 第 1 月：Claude 提示词管理器 v1
  ├── 第 3 月：100 装机量，验证付费
  ├── 第 6 月：MRR $500-$1K
  └── 第 12 月：MRR $3K-$5K（多扩展矩阵）

验证线：Algora bounties（每周 2h，前 4 周）
  ├── 第 1 月：3-5 个 bounty，赚 $500-$1500
  ├── 验证 AI 加速假设
  └── 验证完后停掉，资源全投主+副线
```

### 12 个月预期总收入

- 保守估计：**MRR $3K-$5K**
- 乐观估计：**MRR $8K-$15K**
- 一次性收入（bounty + 数据集销售）：$2K-$5K

### 总投入

- 时间：每周 15-20h × 50 周 = 750-1000h
- 现金：~$150-$350/月（Claude Max + Cursor Max + Apify 平台费 + 域名）
- 学习成本：1 周学 Apify 平台、1 周学 Chrome MV3、本身的技术 0 学习成本

---

## 关键判断：为什么这条路真的成立

回到你的核心问题：**"靠 Claude Max + Cursor Max 自主开发产品挣钱有吗？"**

**有，而且这是当前 AI 时代独立开发者最适合的路径**。逻辑是：

1. **Apify/Chrome 扩展商店替代了"营销"**
   - 用户在平台内主动搜索，不需要你做内容/SEO/Twitter
   - 你的代码本身就是产品

2. **AI 把"做产品"成本压到极低**
   - Cursor Max 一周一个爬虫 Actor
   - 你 20 年经验 + AI = 单兵 5-10 倍产能
   - 这是 Damon Chen 当年没有的杠杆

3. **日本华人身份是天然护城河**
   - 日本网站爬虫 = 英语圈做不动
   - 日本本地服务扩展 = 几乎零竞争
   - 不是劣势，是核心差异化

4. **不缺钱付订阅 ≠ 不缺钱**
   - 这条路**不需要 $10K 域名**
   - 月预算 $150-350 完全够
   - 你的限制和这条路完美匹配

---

## 立即可做的 5 件事

1. **本周**：注册 [Apify 账号](https://console.apify.com/sign-up)、关联 [Algora.io](https://algora.io)
2. **本周**：选定第一个 Apify 目标网站（建议 メルカリ 或 SUUMO）
3. **下周**：用 Cursor Max 写第一个 Actor（预期 2-3 天）
4. **下周**：在 Algora 接 1 个 $200-$500 的 bounty（验证 AI 加速）
5. **本月内**：第一个 Actor 上架 + 第一笔 bounty 收入

---

## 详细参考文档

- [Apify Store 详细操作手册](./01-apify-store-playbook.md)
- [Chrome 扩展详细手册](./02-chrome-extension-playbook.md)
- [其他备选路径详细分析](./03-other-paths-details.md)
- [上一份调研：Damon Chen 路径（已被替代）](../methodology/00-master-how-they-make-money.md)

---

## 核心数据来源

- [Apify - Monetize Actors](https://apify.com/partners/actor-developers)
- [ParseForge Actor Factory Case](https://blog.apify.com/parseforge-actor-factory/)
- [Apify Help - Make Money Publishing Actors](https://help.apify.com/en/articles/8684010-make-money-publishing-your-actors-on-apify-store)
- [extensionpay.com - Browser Extensions Revenue](https://extensionpay.com/articles/browser-extensions-make-money)
- [Easy Folders MRR Update](https://www.indiehackers.com/product/easy-folders/6-months-post-launch-my-chrome-extension-has-hit-3-700-in-mrr-and-42-000-in-total-revenue--O3qs28VAnAkcJw0j--M)
- [Algora.io Bounties](https://algora.io/bounties)
- [Chrome MV3 Migration Opportunity](https://www.indiehackers.com/post/software-opportunity-thousands-of-chrome-extensions-are-about-to-disappear-85DQAl9yaLglihq0kkkP)
- [Press Gazette - Google Traffic Down 33% in 2025](https://pressgazette.co.uk/media-audience-and-business-data/google-traffic-down-2025-trends-report-2026/)
