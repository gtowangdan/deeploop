# Week 1: Build & Ship（Day 1-7）

> **本周目标**：Mercari Sold Comps Actor 在 Apify Store 上架 + 自己跑通 50 次 demo
> **总投入**：8-10 小时
> **预算**：$49 Apify Pro plan

---

## Day 1（周六，2 小时）：注册 + 摸底

### Step 1.1：注册 Apify Pro plan（30 分钟）

1. 打开 https://console.apify.com/sign-up
2. 用邮箱注册（如已有账号直接登录）
3. 进入后右上角「Settings → Subscription」
4. 选 **Personal Plan $49/月**（**不要选 Free**，Free 配额跑不动）
5. 填信用卡（可用日元）
6. ✅ Dashboard 显示 "Personal" plan = 通过

### Step 1.2：装 Apify CLI（15 分钟）

打开终端：

```bash
# 1. 装 Node.js 20+（如未装）
node --version  # 应 ≥ 20

# 2. 装 Apify CLI
npm install -g apify-cli

# 3. 登录
apify login
# → 浏览器弹出授权 → 同意

# 4. 验证
apify info
# 应该显示你的 username + email
```

✅ **看到自己 username = 通过**

### Step 1.3：跑通 fatihtahta 现有 Actor 摸底（45 分钟）

**关键步骤**：在动手开发前，先看头部竞品的输出格式 + 缺什么。

1. 打开 https://apify.com/fatihtahta/mercari-japan-scraper
2. 点「Try for free」（用你的免费 credit）
3. 输入测试参数：
   - Search keyword: `vintage levi's`
   - Max items: 20
4. 点「Run」
5. 等 1-2 分钟跑完
6. 看「Output」tab 下载 dataset（JSON 或 CSV）

**逆向看输出字段**：
- 他抓了什么字段？
- 是否区分 active vs sold？（**大概率没区分**——这是你的差异化点）
- 是否有价格历史？
- 是否有卖家信息？

**保存到本地**：
```bash
mkdir ~/projects/mercari-sold-comps
cd ~/projects/mercari-sold-comps
mkdir analysis
# 把 fatihtahta 的输出 JSON 保存到 analysis/fatihtahta-output.json
```

### Step 1.4：同样跑 cloud9_ai 的 Mercari sold（30 分钟）

1. 打开 https://apify.com/cloud9_ai/mercari-scraper
2. 同样操作，跑 20 个结果
3. 对比 fatihtahta 和 cloud9_ai 输出字段差异

记录：
```markdown
# Analysis Notes

## fatihtahta（11 MAU, 5★）
- 字段：title, price, image, url, seller_username, condition
- 缺：sold vs active 区分、价格历史、跨平台 comp

## cloud9_ai（4 MAU, 5★）
- 字段：（你看到的）
- 优势：（如果有）

## 我的差异化点
1. SOLD-only mode + 90 天历史
2. 跨平台 comp（+Yahoo Auctions Closed + Buyee）
3. 日语 keyword 自动扩展
```

### Step 1.5：保存当天进度

```bash
cd ~/projects/mercari-sold-comps
git init
echo "node_modules/\n.env\nstorage/\nanalysis/output*" > .gitignore

cat > PROGRESS.md << 'EOF'
# Mercari Sold Comps - 进度日志

## Day 1 ✅
- Apify Pro plan registered
- Apify CLI installed
- fatihtahta + cloud9_ai analyzed
- 差异化方向确认：SOLD + cross-platform + JP keyword expansion

## Day 2 计划
- Apify Crawlee 项目初始化
- Mercari JP sold 页面结构分析
EOF

git add . && git commit -m "Day 1: setup + competitor analysis"
```

---

## Day 2（周日，3 小时）：Crawlee 项目 + Mercari 页面结构

### Step 2.1：创建 Apify Actor 项目（20 分钟）

```bash
cd ~/projects/mercari-sold-comps

# 创建新 Actor 项目
apify create mercari-sold-comps
# 选 Crawlee + TypeScript

cd mercari-sold-comps

# 检查目录
ls -la
# 应该看到：
# - src/main.ts
# - .actor/actor.json
# - .actor/INPUT_SCHEMA.json
# - package.json
# - Dockerfile
```

### Step 2.2：本地跑通模板（20 分钟）

```bash
# 装依赖
npm install

# 本地跑（默认抓 example.com）
apify run

# ✅ 看到 console 输出 = 通过
```

### Step 2.3：分析 Mercari JP Sold 页面 URL 结构（30 分钟）

打开浏览器（不要登录）：

1. 访问 https://jp.mercari.com/
2. 搜 "vintage levi's"
3. 在过滤器里选「**売り切れ**」（已售完）
4. 看 URL 变化

预期 URL 格式：
```
https://jp.mercari.com/search?keyword=vintage%20levi%27s&status=sold_out
```

记录关键参数：
- `keyword`：关键词
- `status=sold_out`：只看已售
- `sort_by=newest_first`：排序
- `page`：分页

### Step 2.4：用 Cursor 写 Mercari sold scraper 主逻辑（90 分钟）

打开 Cursor，编辑 `src/main.ts`，把以下提示词喂给 Cursor chat：

```
我要写一个 Apify Crawlee TypeScript scraper 抓 Mercari Japan 已售商品。

输入参数：
- keyword: string (e.g. "vintage levi's")
- maxItems: number (default 100)
- includeJapaneseExpansion: boolean (default true)

逻辑：
1. 如果 includeJapaneseExpansion=true，用一个 keyword 映射表把英文关键词扩展到日语别称：
   {
     "vintage levi's": ["リーバイス ヴィンテージ", "Levi's BIG E", "66前期"],
     "supreme": ["シュプリーム"],
     "bape": ["ベイプ", "ア・ベイシング・エイプ"],
     ...
   }
   （先写 10 个常见 reseller 关键词，后续用户可加）

2. 对每个扩展后的 keyword：
   - 访问 https://jp.mercari.com/search?keyword={kw}&status=sold_out&sort_by=newest_first
   - 用 Crawlee 的 PlaywrightCrawler（Mercari 是 SPA）
   - 解析每个商品卡片：
     - title (商品名)
     - sold_price (售价)
     - currency: "JPY"
     - sold_date (售出日期)
     - image_url
     - product_url
     - condition (商品状态：新品 / 未使用 / 目立った傷なし / etc.)
     - shipping_method
     - seller_username (公开 username 不存 PII)

3. 输出到 dataset：
   每条记录加 `source: "mercari_jp_sold"`

4. 反爬：
   - User-Agent: "Apify Mercari Sold Scraper Bot v1.0"
   - 每次请求间隔 2 秒
   - 用 Apify Residential Proxy

要求：
- TypeScript 严格类型
- 用 Apify Actor.init() / Actor.exit() 框架
- 错误处理（页面 404 / 反爬 429）
- 输出 console 进度条

参考 Apify Crawlee 文档：https://crawlee.dev/api/playwright-crawler
```

Cursor 会写代码。**保存运行**：

```bash
apify run --input='{"keyword":"vintage levi's","maxItems":10,"includeJapaneseExpansion":true}'
```

### Step 2.5：debug 反爬（30 分钟）

第一次跑大概率会遇到：
- Mercari 显示「ロボットでないことを確認」CAPTCHA
- 或返回空数据

应对：
1. 改用 Crawlee 的 stealth mode：
   ```typescript
   const crawler = new PlaywrightCrawler({
     useSessionPool: true,
     persistCookiesPerSession: true,
     launchContext: {
       useChrome: true,
       launchOptions: { headless: true },
     },
   });
   ```

2. 加 Residential Proxy（Apify 后台 → Settings → Integrations → Proxy）：
   ```typescript
   const proxyConfiguration = await Actor.createProxyConfiguration({
       groups: ['RESIDENTIAL'],
       countryCode: 'JP',
   });
   ```

3. 让 Cursor 帮你加完整反爬配置

### Step 2.6：当天结束

```bash
git add . && git commit -m "Day 2: Mercari sold scraper MVP"
```

更新 PROGRESS.md。

---

## Day 3（工作日晚 2 小时）：Yahoo Auctions Closed 模块

### Step 3.1：分析 Yahoo Auctions Closed URL（20 分钟）

1. 访问 https://auctions.yahoo.co.jp/closedsearch/closedsearch
2. 搜 "vintage levi's"
3. URL 格式：
   ```
   https://auctions.yahoo.co.jp/closedsearch/closedsearch?p=vintage+levi%27s&va=vintage+levi%27s&aq=-1&oq=&exflg=1&b=1&n=20
   ```

### Step 3.2：用 Cursor 写 Yahoo Auctions 模块（90 分钟）

提示词：
```
在同一个 Apify Actor 项目里加 Yahoo Auctions Closed scraper 模块。

新文件 src/yahoo-auctions.ts：
- 函数 scrapeYahooAuctionsClosed(keyword: string, maxItems: number)
- URL: https://auctions.yahoo.co.jp/closedsearch/closedsearch?p={kw}
- Yahoo Auctions 用普通 server-side render，可以用 CheerioCrawler（更快）

字段：
- title
- final_price (落槌价)
- currency: "JPY"
- end_date
- bidder_count (出价人数)
- image_url
- product_url
- seller_username
- shipping_method

输出加 `source: "yahoo_auctions_closed"`

整合到 main.ts：
- 输入参数加 `crossPlatform: boolean`
- 如果 true，同时跑 Mercari sold + Yahoo Auctions closed
- 用 keyword 模糊匹配把 Mercari 商品和 Yahoo 商品 link 起来（按品牌+型号文本相似度）
```

### Step 3.3：测试

```bash
apify run --input='{"keyword":"vintage levi's","maxItems":10,"crossPlatform":true}'
```

✅ 输出包含两个 source 的数据 = 通过

```bash
git add . && git commit -m "Day 3: Yahoo Auctions module"
```

---

## Day 4（工作日晚 1.5 小时）：Buyee 模块

### Step 4.1：分析 Buyee URL（15 分钟）

Buyee 是 Mercari 的代购镜像站。

1. 访问 https://buyee.jp/mercari/search?keyword=vintage+levi%27s
2. URL 直接对应 Mercari URL
3. **特点**：Buyee 显示 active 商品（在售），价格略高于 Mercari（含手续费）

### Step 4.2：用 Cursor 写 Buyee 模块（60 分钟）

提示词：
```
新文件 src/buyee.ts：
- 函数 scrapeBuyee(keyword: string, maxItems: number)
- URL: https://buyee.jp/mercari/search?keyword={kw}
- 用 CheerioCrawler

字段：
- title
- buyee_price (含 Buyee 服务费的现售价)
- mercari_original_price (原 Mercari 价格，如可见)
- currency: "JPY"
- image_url
- product_url
- buyee_listing_id

输出加 `source: "buyee"`

整合到 main.ts:
- 同一 keyword 三平台同时跑
- 输出 unified 表格：每条 record 包含 mercari_sold_data + yahoo_auctions_data + buyee_current_data
```

### Step 4.3：测试

```bash
apify run --input='{"keyword":"vintage levi's","maxItems":10,"crossPlatform":true}'
```

```bash
git add . && git commit -m "Day 4: Buyee module + unified output"
```

---

## Day 5（工作日晚 1 小时）：日语 keyword 扩展词典

### Step 5.1：用 Claude 生成 reseller 高频关键词词典（45 分钟）

打开 Claude Max，提示词：

```
我要做一个 reseller 工具，输入英文关键词，自动扩展到日语别称。

帮我生成 30 个全球 reseller 圈最热门的英文关键词 + 对应的日语扩展（每个 3-5 个变体）。

格式：JSON

例：
{
  "vintage levi's": ["リーバイス ヴィンテージ", "Levi's BIG E", "66前期", "501XX"],
  "supreme": ["シュプリーム", "Supreme box logo"],
  "bape": ["ベイプ", "ア・ベイシング・エイプ"],
  ...
}

要覆盖的品类：
1. Vintage denim (Levi's, Wrangler, Lee)
2. Hip-hop streetwear (Supreme, BAPE, Stussy)
3. Anime collectibles (鬼滅の刃, ガンプラ, Pokemon, ジョジョ)
4. Sneakers (Air Jordan, Yeezy, Nike Dunk)
5. Watches (G-Shock, Seiko vintage)
6. Cameras (Leica, Nikon film)
```

把 Claude 输出保存到 `src/keyword-expansion.ts`：

```typescript
export const JP_KEYWORD_EXPANSION: Record<string, string[]> = {
  "vintage levi's": ["リーバイス ヴィンテージ", "Levi's BIG E", "66前期", "501XX"],
  // ... 30 个
};
```

### Step 5.2：集成到 scraper（15 分钟）

让 Cursor 修 main.ts：
- 检查输入 keyword 是否在 JP_KEYWORD_EXPANSION
- 如果在，自动扩展 + 同时跑所有变体
- 去重（按 product_url）

```bash
git add . && git commit -m "Day 5: JP keyword expansion dictionary"
```

---

## Day 6（周六，3 小时）：Apify Store 上架

### Step 6.1：写 INPUT_SCHEMA.json（30 分钟）

让 Cursor 写完整的 INPUT_SCHEMA.json：

```json
{
  "title": "Mercari Sold Comps Scraper Input",
  "type": "object",
  "schemaVersion": 1,
  "properties": {
    "keyword": {
      "title": "Search keyword",
      "type": "string",
      "description": "English or Japanese. Auto-expanded to JP variants if matched.",
      "editor": "textfield",
      "prefill": "vintage levi's"
    },
    "maxItems": {
      "title": "Max items",
      "type": "integer",
      "default": 100,
      "minimum": 1,
      "maximum": 5000
    },
    "crossPlatform": {
      "title": "Include Yahoo Auctions Closed + Buyee",
      "type": "boolean",
      "default": true
    },
    "includeJapaneseExpansion": {
      "title": "Auto-expand to Japanese keywords",
      "type": "boolean",
      "default": true
    }
  },
  "required": ["keyword"]
}
```

### Step 6.2：写 README.md（90 分钟，**最关键**）

让 Claude 写英文 README，提示词：

```
我做了一个 Apify Actor "Mercari Sold Comps"，写一份英文 README 投到 Apify Store。

核心功能：
1. 抓 Mercari Japan 已售（sold）商品的 90 天价格历史
2. 同时抓 Yahoo Auctions Closed 落槌价
3. 同时抓 Buyee 当前在售价
4. 日语关键词自动扩展（reseller 输入英文，自动搜日语变体）

Buyer persona：
- 美国/欧洲在 Mercari Japan 倒卖 vintage 的 reseller
- 跨境 dropshipper
- 日货代购

价格：$5/1000 results

README 必须有：
1. 一句话定位（10-20 词）
2. 关键功能 bullet（5 个）
3. Sample input + sample output（截图位）
4. 5 个真实 use case（写得详细，每个 100 词）：
   - Vintage denim flipper 决策周扫货预算
   - 鬼滅 figure dropshipper 看 release wave 价格
   - Buyee 类竞品做内部 BI
   - Etsy 店主筛选高利润商品
   - YouTube vintage hauler 做内容
5. 与其他 Apify Mercari actors 的对比表（你的优势）
6. SEO 关键词密集（"Mercari sold price", "Japan reseller", "vintage import", "cross-platform comp"）
7. 安全声明（不存 PII，遵守 ToS，2s rate limit）

风格：简洁，技术友好，不夸张
```

把生成的 README 写到 `README.md`。

### Step 6.3：截图（30 分钟）

跑一次 actor，截图：
1. Input form 填写界面
2. 跑完后的 dataset 表格视图
3. 一个具体 row 展开（显示三平台数据）

保存到 `screenshots/` 目录。在 README 里引用。

### Step 6.4：上架（30 分钟）

```bash
# 1. 部署到 Apify
apify push

# 2. 浏览器打开
# https://console.apify.com/actors

# 3. 找到 mercari-sold-comps，点 Settings
# 4. Make public：
#    - Visibility: Public
#    - Pricing: $5/1000 results
#    - Trial: 100 free items

# 5. Description: 用 README 第一句
# 6. Categories: E-commerce, Data extraction
# 7. Tags: mercari, japan, sold, vintage, reseller

# 8. Publish
```

✅ 浏览器搜 https://apify.com/[你的username]/mercari-sold-comps 能打开 = 上架成功

```bash
git add . && git commit -m "Day 6: Apify Store published"
git tag v0.1
```

---

## Day 7（周日，1 小时）：决策点

### Step 7.1：填决策表

| 验证项 | 通过 | 备注 |
|-------|------|-----|
| Apify Pro 注册 | ☐ | |
| Mercari sold scraper 跑通 | ☐ | |
| Yahoo Auctions 模块跑通 | ☐ | |
| Buyee 模块跑通 | ☐ | |
| JP keyword expansion 生效 | ☐ | |
| README 完整 + 截图 | ☐ | |
| Apify Store 上架 + 公开可见 | ☐ | |

### Step 7.2：决策

**全部 7 项通过** → ✅ **Week 2: Runs & SEO**

**反爬卡死** → 加 Residential Proxy（Apify 后台 add-on）；如仍不通：
- 转 Yahoo Auctions Closed 单独 actor（最简单的）
- 跳过 Mercari，只做 Yahoo + Buyee

**README 难产** → 用 fatihtahta 的 README 做模板，改 30%

---

## Week 1 总结

✅ 本周 deliverable：
- Apify Pro 账号
- Mercari Sold Comps Actor 上架公开
- 完整 README + 截图
- 三平台抓取通

❌ 本周失败信号：
- 反爬完全卡死（用了 proxy 仍 0 数据）
- Apify 平台拒绝上架（极小概率）

---

## 下一步

打开 [week2-runs-seo.md](./week2-runs-seo.md)，开始 Day 8。
