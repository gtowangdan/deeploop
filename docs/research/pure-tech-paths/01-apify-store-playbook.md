# Apify Store 完整赚钱手册

> 主推荐路径：纯技术变现，平台算法分发流量，AI 放大产能 5-10 倍

---

## 平台基础

### 什么是 Apify Store

[Apify](https://apify.com) 是一个"爬虫即服务"平台。开发者把爬虫（叫 **Actor**）发布到 [Apify Store](https://apify.com/store)，用户付费运行你的 Actor 来获取数据。

**对你而言它就是**：你写代码 → 上架 → 平台带流量 → 用户付费 → 你拿 80%

### 收入分成

- **80/20**：开发者拿 80%，Apify 平台拿 20%
- 用户支付的"compute units"和"proxy费"先扣除（这是平台运行成本），剩余的按 80/20 分

### 真实赚钱数据

| 案例 | 数据 | 来源 |
|------|------|------|
| 头部独立创作者 | **$10K+ MRR** | [Apify 官方](https://apify.com/partners/actor-developers) |
| **ParseForge** | 6 个月 124 个 Actor、1.9K 用户、单 Actor 最高 $1K MRR、单月最大客户 $8K | [Apify Blog](https://blog.apify.com/parseforge-actor-factory/) |
| 大量普通创作者 | $1K-$2K MRR | Apify 官方说法 |

### 平台规模

- 50K+ MAU 还在增长
- Actor Store 已有数千个 Actor
- 大客户包括财富 500 强企业（持续付费的稳定基础）

---

## 为什么这是你的最优路径

| 你的特征 | Apify 路径要求 | 匹配度 |
|---------|-------------|------|
| 20 年全栈经验 | Node.js/Python 写爬虫 | ✅ 过剩 |
| Claude Max + Cursor Max | AI 写爬虫效率 5-10 倍 | ✅ 红利最大 |
| 日本华人 | 日本网站爬虫 = 英语圈做不动的护城河 | ✅ 核心杠杆 |
| 不善英文推广 | Actor 文档 AI 写 + 平台内部 SEO | ✅ |
| 不愿出镜 | 平台算法分发，零个人品牌 | ✅ |
| 每周 15-20h | ParseForge 6 个月做 124 个证明产能上限远超 | ✅ |
| 预算 $150-$350/月 | 用户付费里扣平台费，开发者无需垫付 | ✅ |

---

## 12 个月行动清单

### 第 0 月：环境搭建（1 周）

- [ ] 注册 [Apify 账号](https://console.apify.com/sign-up)（免费）
- [ ] 阅读 [Apify SDK 文档](https://docs.apify.com)
- [ ] 跑通 1-2 个官方 [Web Scraper](https://apify.com/apify/web-scraper) 教程
- [ ] 安装 Apify CLI：`npm install -g apify-cli`
- [ ] 写一个 Hello World Actor 并部署
- [ ] **理解 Apify SDK 的核心概念**：Actor、Dataset、Key-Value Store、Request Queue、Proxy

### 第 1 月：第一个 Actor

#### 选目标网站（最关键）

**优先级排序**：
1. **日本本地网站**（你的护城河）
2. **B2B 数据**（付费意愿强）
3. **避开**：LinkedIn、Twitter（红海）、Amazon US（已有大量 Actor）

**推荐起步目标（按容易度）**：
- メルカリ（C2C，结构清晰）
- SUUMO（不动产，数据规整）
- 食べログ（餐饮）
- 価格.com（比价）
- リクナビ / マイナビ（招聘）

#### 写 Actor

```bash
apify create my-mercari-scraper
cd my-mercari-scraper
# 用 Cursor Max 写主逻辑
apify run  # 本地测试
apify push  # 推送到平台
```

**用 Cursor Max 的工作流**：
1. 让 Claude 分析目标网站结构（截图 + URL）
2. Cursor 生成爬虫骨架
3. 你调试反爬和边界情况（这部分 AI 最弱，需要你的经验）
4. AI 写 README 和示例输入

**预期时间**：第一个 Actor 2-3 天（含调试）

#### 定价策略

- 起步：**$1 / 1000 results**
- 复杂的（需要登录、反爬强）：$2-$5 / 1000 results
- 一次性数据集（如"全日本 1 万家咖啡店"）：$50-$200 一次性

### 第 2-3 月：节奏化生产

- [ ] **每周 1-2 个 Actor**
- [ ] 第 3 月底总数 5-10 个
- [ ] 优先做"系列"：如先 メルカリ → 然后 ヤフオク → 然后 ラクマ（同类型不同平台）
- [ ] **关键操作**：每发布一个新 Actor，在 README 里互相引用（内部 SEO）

### 第 4-6 月：深耕 + 优化

- [ ] **看数据决定方向**：
  - Apify 后台能看每个 Actor 的运行次数、收入
  - 出单的 Actor → 围绕它做"系列"
  - 不出单的 Actor → 不要继续投入，但不下架（保留长尾）
- [ ] **优化高产 Actor**：
  - 加更多输出字段
  - 加详细 README（用 Claude 写英文 + 你写日语版）
  - 加截图、示例输出
- [ ] **修反爬**：每月留 20% 时间维护已上架 Actor
- [ ] **第 6 月目标**：15-25 个 Actor，MRR $1K-$3K

### 第 7-9 月：垂直化 + 数据集

- [ ] **数据集销售**：把热门 Actor 的输出转成现成数据集
  - 例：把"日本 1 万家咖啡店"作为一次性下载卖 $99
  - 上 [Datarade](https://datarade.ai) 同步引流
- [ ] **找企业客户**：
  - Apify 平台内消息大客户
  - 提供定制版（年付 $5K-$20K）
- [ ] **第 9 月目标**：MRR $3K-$5K

### 第 10-12 月：组合策略

- [ ] **总 Actor 数**：30-40 个
- [ ] **Top 5 营收来源**做成 Pro 版
- [ ] **Actor 套件打包**：如"日本不动产全套"$199 一次性
- [ ] **第 12 月目标**：MRR $5K-$10K

---

## Actor 选题清单（候选 50 个）

### 日本本地（最优先）

**EC / 比价**：
1. メルカリ商品搜索
2. ヤフオク商品搜索
3. ラクマ商品搜索
4. 楽天商品价格追踪
5. Amazon JP 价格追踪
6. 価格.com 价格历史
7. Yahoo!ショッピング搜索

**不动产**：
8. SUUMO 物件检索
9. HOME'S 物件检索
10. AtHome 物件检索
11. LIFULL HOME'S 投资物件
12. アットホーム 中古マンション

**美食**：
13. 食べログ店舗
14. ぐるなび店舗
15. Retty レビュー
16. ホットペッパー店舗

**招聘**：
17. リクナビ求人
18. マイナビ求人
19. Indeed Japan
20. doda求人
21. Wantedly企業
22. ビズリーチ求人

**企业数据库**：
23. 日本企業ナビ
24. 東商信用録（如可访问）
25. EDINET 上市企業情報

### B2B 数据（次优先）

26. Crunchbase 公司搜索（替代 LinkedIn）
27. AngelList 创业公司
28. ProductHunt 历史榜单
29. G2 软件评分
30. Capterra 软件搜索

### AI 训练数据（新兴）

31. arXiv 论文摘要
32. GitHub Trending
33. Hacker News 历史
34. Reddit 子板块归档

### 中国市场（华人优势）

35. 小红书笔记搜索（注意合规）
36. 知乎话题
37. B站视频元数据
38. 豆瓣电影/书籍

### 工具型（小众但稳）

39. Whois 批量查询
40. SSL 证书有效期检查
41. 域名可用性检查
42. 网站技术栈检测

---

## 成功 Actor 的共同特征

研究 Apify Store 内月入 $1K+ 的 Actor，找到这些共同点：

1. **目标网站清晰、结构稳定**：不是天天改版的
2. **输出字段丰富**：不只是基础字段，加上评分、价格历史、关联数据
3. **README 详细**：示例输入/输出、应用场景、定价透明
4. **支持过滤参数**：让用户精细控制
5. **错误处理优雅**：失败时给清楚的错误信息

---

## AI 加速的具体场景

### 场景 1：分析新目标网站（30 分钟 → 5 分钟）

```
1. 截图目标页面 → 喂给 Claude
2. Claude 给出 DOM 结构分析
3. 你确认关键 selector
4. Cursor 生成爬虫骨架
```

### 场景 2：写 Actor 主逻辑（2-3 天 → 半天）

```
1. 在 Cursor 里描述需求："爬 SUUMO 物件，输入区域，输出标题/价格/链接/平米"
2. Cursor 生成 Apify SDK 代码骨架
3. 你调试反爬和边界
4. Cursor 写 unit tests
```

### 场景 3：写 README（1-2 小时 → 15 分钟）

```
1. Claude 写英文版 README（含示例输入/输出/应用场景）
2. 你校对 + 加日语版
3. 加截图
```

### 场景 4：维护反爬变化（半天 → 1 小时）

```
1. Actor 失败 → 看错误日志
2. 喂给 Claude 让它分析变化
3. Cursor 修复 selector
```

---

## 风险与对策

| 风险 | 概率 | 对策 |
|------|------|------|
| 目标网站改版反爬 | 中 | 每月维护时间预留 20%；用 Apify 自带反爬基础设施（residential proxy） |
| 选错目标无人买 | 高 | 第 1-3 月撒网式做 5-10 个，看哪个出单再深耕；不出单的不删但不投入 |
| Apify 平台政策变化 | 低 | 80% 分成多年稳定；平台对开发者友好 |
| 法律风险（爬公开网站） | 低 | 只爬公开数据；ToS 透明告知；不爬登录后内容；不存储个人信息 |
| 大客户压价定制 | 中 | 标准 Actor 不打折；定制版年付 $5K+ 起 |

---

## 立即可做的 3 件事

1. **本周末**：
   - 注册 [Apify](https://console.apify.com/sign-up)
   - 装 CLI：`npm install -g apify-cli`
   - 跑通官方 Web Scraper 教程

2. **下周**：
   - 选第一个目标（建议 **メルカリ** —— 结构清晰、用户多、付费意愿强）
   - 用 Cursor Max 写 Actor（预期 2-3 天）

3. **下下周**：
   - 上架，定价 $1 / 1000 results
   - 写完整 README + 加截图
   - 在 Apify Store 内部搜你的关键词，看排名

---

## 核心数据来源

- [Apify - Become an Actor Developer](https://apify.com/partners/actor-developers)
- [Apify Help - Make Money Publishing Actors](https://help.apify.com/en/articles/8684010-make-money-publishing-your-actors-on-apify-store)
- [ParseForge Case Study - 124 Actors in 6 months](https://blog.apify.com/parseforge-actor-factory/)
- [Apify SDK Docs](https://docs.apify.com)
- [Apify Store](https://apify.com/store)
- [Apify Pricing](https://apify.com/pricing)
