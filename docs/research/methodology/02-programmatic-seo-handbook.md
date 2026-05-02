# Programmatic SEO 实操手册

> 调研日期：2026-05-02
> 这是 Marc Lou、Danny Postma、Damon Chen 共同使用的核心赚钱武器

---

## A. 什么是 Programmatic SEO（pSEO）

### 核心定义

**1 个 HTML 模板 × N 条数据 = N 个 SEO 页面**

公式：
- 普通 SEO：1 篇文章 = 1 个关键词
- pSEO：1 个模板 = 1000+ 关键词

### vs 普通 SEO 的对比

| 维度 | 普通 SEO | pSEO |
|------|---------|------|
| 单位产出 | 1 篇文章 = 1 个关键词 | 1 个模板 = 1000+ 关键词 |
| 内容来源 | 人工写 | 数据库填充 |
| 关键词类型 | 头部 + 中尾 | 长尾 + 极长尾（"head + modifier"） |
| 时间成本 | O(N) | O(1) 建模板 |
| 风险 | 内容质量 | 被判 "scaled content abuse" |

### 为什么对独立开发者特别有效

1. **不需要内容团队**：1 个开发者 + 1 个周末 = 1000 个页面
2. **复利效应**：模板写一次，加数据就扩张
3. **拦截"购买决策瞬间"流量**：长尾关键词意图明确（如 "best X in San Francisco"）
4. **不依赖广告预算**：Marc Lou 的 LogoFast 0 广告，5 万次 logo 生成

---

## B. 经典案例（带具体数据）

### B1. Zapier（鼻祖）

- **页面数**：5000+ 集成 App，组合生成 **50,000+ "App A to App B" 集成页**，累计约 **800,000 页**
- **模板**：`/apps/[app-a]/integrations/[app-b]`
- **流量**：月 organic **2.6M～5M**，关键词覆盖 360 万+
- **关键**：每个页面有真实的 trigger/action 数据，不是空模板

### B2. Marc Lou 的微站矩阵（最适合学习的模板）

**核心策略：3 个 HTML 模板 = 1334 个排名页**

**Rage Rooms 案例**（[Marc Lou newsletter](https://newsletter.marclou.com/p/how-to-grow-a-micro-startup-with-programmatic-seo)）：
- 模板 1：主页（1 页）
- 模板 2：`/[city]/` —— **333 个城市页**（人口 10 万+ 美国城市）
- 模板 3：`/rage-room/[business-name]/` —— **约 1000 个店铺页**
- 数据来源：**Google Maps API**（店名、价格、评分、位置）
- AI 用法：ChatGPT 只用来写 meta description，正文用真实数据

**Marc 的项目流量**：
- BooksCalculator：15,600 月访客
- GamifyList：9,000 月访客（数据是 $150 外包 VA 收集的 600 个 app）
- WorkbookPDF：4,500 月访客（1 个模板 25 个语言页）
- LogoFast → ShipFast 引流：5 万次生成，5000 美元转化

**Marc 的 KD/Volume 阈值**：
- KD < 20（"10 个反链以内能排上"）
- 单国搜索量 > 500/月（或全球 1500/月）
- 至少 20 个相关长尾关键词

### B3. Danny Postma 的 HeadshotPro

- **核心关键词**：`professional headshots`（21K 月搜索，KD 23）—— Top 10
- **pSEO 部署**：**200+ 城市/地区页**
- **流量结果**：3K 月 organic 访客，覆盖 **1000+ 关键词**
- **DR 增长**：35 → 44（4 个月内），2 个月 120 个反链域

### B4. Damon Chen 的 PDF.ai

- **核心赌注**：花 $10K 买下 `pdf.ai` 精品域名
- **pSEO 路径**：构建一套**免费 PDF 工具集**（merge/split/rotate/compress/chat），每个工具一个独立着陆页
- **逻辑**：每个工具页 = 1 个长尾关键词
- **结果**：$80K → $1.5M ARR
- **特点**：**不是空 SEO landing page，而是真正的产品入口**

---

## C. pSEO 技术实现 6 步

### 1. 选模板关键词

找到 "head term + modifier" 结构：
- `[head] in [city]` → 地理型
- `[product] vs [competitor]` → 比较型
- `convert [format A] to [format B]` → 转换型
- `best [tool] for [use case]` → 推荐型
- `[number] [thing]` → 数据型

### 2. 找数据源（按推荐顺序）

1. **专有数据**（最强护城河）：用户上传/产品自身数据 —— Wise 的实时汇率、Zillow 的房产数据
2. **公开 API**：Google Maps、OpenWeather、政府开放数据
3. **爬虫 + VA**：Marc Lou 花 $150 外包 600 条记录
4. **AI 生成**（最弱、最危险）：仅用于辅助文本，绝不能是正文主体

### 3. 技术栈选择（按规模）

- **1～100 页**：Google Sheets + WordPress（WP All Import 插件）/ Webflow CMS
- **100～1000 页**：Airtable + Webflow CMS + Zapier 同步
- **1000+ 页**：**Next.js + getStaticPaths + getStaticProps**（独立开发者首选）
- 终极方案：Next.js 15 ISR + 数据库（PostgreSQL/Supabase）+ Vercel

### 4. Next.js 批量生成核心代码

```js
// pages/[city].tsx
export async function getStaticPaths() {
  const cities = await fetchCities();  // 333 个城市
  return {
    paths: cities.map(c => ({ params: { city: c.slug } })),
    fallback: 'blocking'
  };
}

export async function getStaticProps({ params }) {
  const data = await fetchCityData(params.city);
  return {
    props: { data },
    revalidate: 86400
  };
}
```

### 5. 内部链接 & sitemap

- **Sitemap 限制**：单个 sitemap 最多 50,000 URL / 50MB，超过要分片，再用 sitemap index
- **内链策略**：构建 silo（主题筒仓）—— 所有德州城市页互相链接，且都链接到 "Texas" 主页
- **务必**：从已有流量的博客页 → 链向新 pSEO 页（传 PageRank）
- **避免**：所有 pSEO 页只内部互链而不接收外部页链接（Google 视作孤岛）

### 6. 避免被判垃圾的硬指标

- 每页 **≥60% 内容差异**（不止换城市名）
- 每页拉 **3+ 数据源**（评分、价格、距离、评论…）
- 单页 **500-1000 字以上**实际内容
- 提供**模板搜索结果之外的额外价值**（计算器、对比工具、地图）
- **分阶段上线**：不要一次性 publish 10 万页 —— 每周几百页逐步放出

---

## D. 关键词调研 SOP

### 工具 + 操作步骤

1. **Ahrefs Keywords Explorer**（或 Semrush / 免费的 Keyword Surfer）
2. 输入种子词（如 `rage room`、`professional headshots`、`merge pdf`）
3. 切到 **"Matching terms"** 报告
4. 加 Include filter：`in` / `for` / `vs` / `near me` / `[city]`
5. 设过滤器：
   - **KD < 20**（独立开发者初期）；DR 弱可降到 < 10
   - **Volume 50-500/月**（单关键词），但**总和** > 几万
   - **Top-ranking sites DR < 30**（真正可竞争）
6. 检查 SERP **意图一致性**：随机抽 5 个变体，确认 Google 显示的页面类型一致

### 避坑

- 不要做"年份"型关键词（"best X 2024" 会过期）
- 不要做 SERP 已被大站垄断的（Top 10 全是 DR 80+ 站点）
- 警惕 search volume 数据虚高

---

## E. ⚠️ AI 时代的 pSEO（HCU 后的新规则）

### Google March 2024 Helpful Content Update 的杀伤

- 新增 **"Scaled Content Abuse"** 政策：批量生成"内容仅微差"的页面 = 直接 deindex
- Originality.ai 研究：3 月份扫描 79,000 站，**1,446 个站被人工降权**
- 一个电商站做了 18,000 个分类组合页，流量 **-73%**
- 某 SaaS 50,000 长尾页 **3 个月内 deindex 98%**
- HCU 是**全站分类器**：一个烂 pSEO 模块会拖累整个域名

### AI 生成内容的安全用法

1. **用 AI 做 meta description 和摘要**（次要文本），不用 AI 写正文
2. **AI + 真实数据混合**：先有数据，AI 只做改写润色
3. **加入"独有角度"**：用 AI 生成本地化建议、个性化推荐 —— 但前提是有真实数据支撑
4. **每页人工审核 1-3% 抽样**

### Google E-E-A-T 现在的硬要求

- Experience（亲身经验）/ Expertise / Authoritativeness / Trust
- 每个 pSEO 页要有：作者信息、数据来源链接、更新时间、用户评价

---

## F. 真实失败案例

| 站点 | 做法 | 结果 |
|------|------|------|
| Zacjohnson.com | AI + 模板大量生成 | March 2024 后 **被完全 deindex** |
| 某电商 18K 组合页 | 分类 × 城市纯模板 | -73% 流量 |
| 某 SaaS 50K AI 长尾页 | AI 全自动写 | **98% 被 deindex** |
| G2、ZoomInfo | 大量薄弱比较页 | 多次 Core Update 后大幅下滑 |

**John Mueller 原话**："Programmatic SEO is often a fancy banner for spam."

---

## G. 2026 年 pSEO 还有效吗？

### ✅ 仍然有效的领域

1. **真实数据驱动**：Wise（汇率）、Zillow（房产）、Nomad List（城市数据）—— 数据本身就是产品
2. **工具型 pSEO**：PDF.ai 模式 —— 每个页面是真实工具入口
3. **本地服务 / 商业意图**：转化型查询（"plumber in [city]"），AI Overview 介入少
4. **比较型**：`X vs Y`、`alternatives to X`

### ❌ 已死的玩法

1. 纯文本模板，每页只换城市名/产品名
2. 全 AI 写的"how to" 长博文 farm
3. 信息型查询（"what is X"）—— AI Overview 直接吃掉点击
4. 没有任何专有数据的 listicle 站

### AI Overview / SGE 冲击实测

- AI Overview 出现的 SERP，CTR 下降 **30-60%**
- 但**商业意图查询**（含 "buy"、"hire"、"compare"、"vs"、"best"）—— AI Overview 出现率低，pSEO 仍可吃流量
- 被 AI Overview **引用**（cite）反而能带来高质量点击

### ROI 真实评估（2026）

- **预期周期**：上线后 **3-6 个月**才开始排名
- **成功率**：粗估 < 30%
- **资源投入**：1 个开发者 2-4 周可上线 1000 页
- **关键变量**：**数据质量 > 模板美观 > 页面数量**

---

## H. 日语 / 亚洲市场 pSEO

### 日语市场特点

- 尚无类似 Marc Lou / Danny Postma 级别的公开成功案例
- 日本 Google 用同一套核心算法，**HCU 同步生效**
- **日语 SEO 难点**：分词（形态素解析）、敬语、汉字/假名混用 —— 模板需要本地化校对
- **机会领域**：
  - 地方都市服务页（"[市区町村] 整体院"、"[駅名] 居酒屋"）—— 大型聚合站尚未完全覆盖
  - B2B SaaS 集成页（日语版稀缺）
  - 翻译 / 转换工具页（PDF.ai 模式可复制）

### 中文 pSEO 特殊考虑

- 百度算法独立，对模板批量生成更敏感（百度"飓风算法"针对采集站）
- 简繁体差异、地域差异大
- 国内市场更适合微信生态/小红书 SEO，传统 pSEO ROI 较低

---

## 实操手册：从 0 到上线 pSEO 站点

### 阶段 1：选题（1-3 天）

- [ ] 选定一个细分领域（你的产品/兴趣相关）
- [ ] Ahrefs Keyword Explorer 找种子词
- [ ] 找到 head + modifier 模式（≥ 20 个长尾变体）
- [ ] 验证：KD < 20，单词 Vol > 50，总 Vol > 5,000/月
- [ ] 抽 5 个 SERP 检查意图一致性
- [ ] 检查 Top 10 站点 DR < 30

### 阶段 2：数据（3-7 天）

- [ ] 列出每页需要的字段（至少 5-7 个）
- [ ] 找数据源：API > 公开数据 > VA 整理 > 爬虫
- [ ] 整理成 CSV/JSON/Database
- [ ] 数据量 ≥ 50（先小试）

### 阶段 3：模板（3-5 天）

- [ ] 选栈：Next.js + Vercel
- [ ] 手工写 3-5 个示例页（不要直接生成）
- [ ] 每页 ≥ 500 字，含表格/图表/地图
- [ ] H1、Title、meta description 模板化
- [ ] 内链结构：silo + crossover
- [ ] schema.org 结构化数据（LocalBusiness/Product/FAQ）

### 阶段 4：上线（1-2 天）

- [ ] 部署 → 生成 sitemap.xml（分片 < 50K URL）
- [ ] 提交 Google Search Console
- [ ] **分阶段发布**：第 1 周 50 页 → 第 2 周 200 页 → 逐步放开
- [ ] 手动 Request Indexing 抽样 10-20 页

### 阶段 5：反链 + 监测（持续）

- [ ] Product Hunt 上线（拿 follow 反链）
- [ ] 提交目录站（TIAAFT、BACKL.IO、Indie Hackers）
- [ ] 目标：30 天内 ≥ 10 个反链
- [ ] GSC 监控：覆盖率、平均排名、CTR
- [ ] 3 个月后审计：删低质量页（< 10 月访的考虑 noindex）

### 阶段 6：迭代

- [ ] 找出 Top 20% 流量页 → 加深内容
- [ ] AI Overview 出现页 → 优化为可被引用的结构
- [ ] 持续更新数据（新鲜度 = 排名加分）

---

## 当前有效性最终判断（2026）

| 指标 | 判断 |
|------|------|
| pSEO 是否还有效？ | ✅ **有效，但门槛大幅提高** |
| 适合独立开发者吗？ | ✅ **仍是最佳武器之一**（前提：有真实数据/工具） |
| ROI | 中位数低，但头部成功者仍能 $10K-$100K MRR |
| 风险等级 | 🔴 **高**（HCU 一刀致命） |
| 关键护城河 | 专有数据 > 真实工具 > 模板设计 |
| 与 Marc Lou 时代对比 | 数据/工具型仍可复制；纯模板型已死 |

**一句话总结**：2026 年的 pSEO 不再是"批量生成页面"，而是"**用工程方式批量提供真实价值**"。Marc Lou 路线（免费工具 + 数据型 pSEO）依然有效，纯文本模板路线已被 Google 打死。

---

## 数据来源

- [Marc Lou - How to Grow With Programmatic SEO](https://newsletter.marclou.com/p/how-to-grow-a-micro-startup-with-programmatic-seo)
- [Marc Lou - Free Tool Marketing](https://newsletter.marclou.com/p/marketing-for-product-obsessed-developers)
- [Indie Hackers - Danny Postma's SEO strategy](https://www.indiehackers.com/post/breaking-down-danny-postmas-seo-strategy-for-headshotpro-300k-in-1-year-fad0af94d2)
- [Starter Story - HeadshotPro $300K/Month](https://www.starterstory.com/stories/headshotpro-breakdown)
- [Starter Story - Marc Lou ShipFast](https://www.starterstory.com/marc-lou-shipfast)
- [Starter Story - PDF.ai $1.5M ARR](https://www.starterstory.com/pdf-ai-breakdown)
- [Ahrefs - Programmatic SEO Explained](https://ahrefs.com/blog/programmatic-seo/)
- [Backlinko - Programmatic SEO 2026](https://backlinko.com/programmatic-seo)
- [Zapier Programmatic SEO Case Study](https://practicalprogrammatic.com/examples/zapier)
- [Search Engine Journal - pSEO Deindexed Bounced Back](https://www.searchenginejournal.com/why-website-deindexed-by-google-for-programmatic-seo-bounced-back/552179/)
- [Metaflow - pSEO 2026 Avoiding Scaled Content Abuse](https://metaflow.life/blog/what-is-programmatic-seo)
- [The Blog Smith - Google March 2024 Core Update](https://www.theblogsmith.com/blog/google-march-2024-core-update/)
- [Nico Digital - Programmatic SEO 2026 Playbook](https://www.nicodigital.com/digital-marketing/programmatic-seo-2026-playbook/)
- [Search Engine Land - SEO in 2026 AI Influence](https://searchengineland.com/seo-2026-higher-standards-ai-influence-web-catching-up-473540)
- [DEV - Programmatic SEO with Next.js](https://dev.to/agamm/programmatic-seo-with-nextjs-pmh)
- [Untalked SEO - pSEO Next.js Tutorial](https://untalkedseo.com/programmatic-seo-nextjs/)
- [SEOmatic - pSEO Internal Linking](https://seomatic.ai/blog/programmatic-seo-internal-linking)
- [Ahrefs Japan - プログラマティックSEO](https://ahrefs.jp/blog/content-marketing/programmatic-seo/)
- [Get Passionfruit - pSEO Without Traffic Loss](https://www.getpassionfruit.com/blog/programmatic-seo-traffic-cliff-guide)
- [AirOps - Hidden Dangers of Programmatic SEO](https://www.airops.com/blog/hidden-dangers-of-programmatic-seo)
