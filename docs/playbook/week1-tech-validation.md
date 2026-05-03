# Week 1: 技术验证（Day 1-7）

> **本周目标**：验证 AniList API 能拉到章节信息 + 章节通知能跑通
> **不写产品代码**。如果 API 不可用，整个项目转 Backup
> **总投入**：8-12 小时

---

## Day 1（周六）：注册账号 + 准备工具（2 小时）

### Step 1.1：注册 Apple Developer（30 分钟）

1. 打开 https://developer.apple.com/programs/
2. 点击右上角「**Enroll**」
3. 用你的 Apple ID 登录（如果没有，先去 https://appleid.apple.com 注册）
4. 选择「**Individual / Sole Proprietor**」（不要选 Organization，要法人证明）
5. 填写姓名（必须和身份证/护照一致）
6. 填写信用卡：**$99/年**（可用日元 ¥14,800/年）
7. 提交后等待 Apple 审核（**24-48 小时**）
8. ✅ 收到 Apple 邮件「Welcome to the Apple Developer Program」= 通过

**失败应对**：
- 信用卡拒收 → 换张卡，或用日本本地卡
- 审核被拒 → 检查姓名是否和身份证一致
- 等了 5 天没回 → 联系 Apple Developer Support

---

### Step 1.2：注册 AniList API（5 分钟）

1. 打开 https://anilist.co/signup
2. 用邮箱注册账号
3. 注册完成后，**直接打开** https://anilist.co/graphiql
4. **不需要 API key**（公开 API）
5. ✅ 看到 GraphQL playground = 通过

---

### Step 1.3：注册楽天ブックス API（10 分钟）

1. 打开 https://webservice.rakuten.co.jp/
2. 点击「**新規アプリ登録**」
3. 用日本邮箱注册（如果没有，用 Gmail 也行）
4. 创建新 App：
   - アプリ名：`ChapterPing`（项目代号）
   - URL：`http://localhost:3000`（暂用）
   - 検索キーワード：選任意
5. 拿到 `Application ID`（长得像 `1058989765012345678`）
6. ✅ 把这个 ID 存到本地的 `.env` 文件

---

### Step 1.4：注册 Cloudflare 账号（5 分钟）

1. 打开 https://dash.cloudflare.com/sign-up
2. 用邮箱注册
3. 验证邮箱
4. ✅ 进入 Dashboard = 通过
5. 暂不开 Workers（Day 4 才用）

---

### Step 1.5：本地环境准备（30 分钟）

打开终端：

```bash
# 1. 创建项目文件夹
mkdir ~/projects/chapterping
cd ~/projects/chapterping

# 2. 初始化 Git
git init
echo "node_modules/\n.env\n*.pyc\n__pycache__/" > .gitignore

# 3. 创建 Python 测试目录
mkdir test-anilist
cd test-anilist

# 4. Python 环境（如果没有 Python 3.11+）
# Mac: brew install python@3.11
# Windows/Linux: 自查
python3 --version  # 应该 ≥ 3.11

# 5. 安装依赖
pip3 install requests python-dotenv
```

✅ 没报错 = 通过。

---

### Step 1.6：保存这一天的状态（10 分钟）

创建 `~/projects/chapterping/PROGRESS.md`：

```markdown
# ChapterPing 进度日志

## Day 1（YYYY-MM-DD）✅
- Apple Developer 注册中（等审核）
- AniList 账号 OK
- 楽天 API ID: [你的 ID]
- Cloudflare 账号 OK
- 本地环境 OK

## Day 2 计划
- 测试 AniList GraphQL 拉《呪術廻戦》章节信息
```

提交到 Git：
```bash
git add . && git commit -m "Day 1: accounts ready"
```

---

## Day 2（周日）：测试 AniList GraphQL（2-3 小时）

### Step 2.1：用 Cursor 写测试脚本（30 分钟）

打开 Cursor，新建文件 `test_anilist.py`，把下面这段提示词喂给 Cursor 的 chat：

```
我要写一个 Python 脚本，做这件事：

1. 调用 AniList 的 GraphQL API（https://graphql.anilist.co）
2. 输入漫画名「呪術廻戦」（Jujutsu Kaisen）
3. 拉取该漫画的：
   - 漫画 ID
   - 中文标题、英文标题、日文标题（romaji + native）
   - 总章节数（chapters）
   - 状态（连载中 / 完结）
   - 封面图 URL
   - 描述（description）

不需要 API key，AniList 公开 API。
用 requests 库。
```

Cursor 会生成代码。**直接保存运行**：

```bash
python test_anilist.py
```

### Step 2.2：检查结果（10 分钟）

✅ **预期结果**：

```json
{
  "id": 113415,
  "title": {
    "romaji": "Jujutsu Kaisen",
    "english": "Jujutsu Kaisen",
    "native": "呪術廻戦"
  },
  "chapters": null,  // AniList 漫画 chapters 字段经常 null
  "status": "RELEASING",
  "coverImage": {
    "large": "https://..."
  },
  "description": "..."
}
```

❌ **如果失败**：
- HTTP 429（rate limit）→ 加 sleep(1)
- HTTP 403/404 → 漫画名拼错，换 "Jujutsu Kaisen"（英文）
- 连接失败 → 检查网络

---

### Step 2.3：测试 5 部漫画（30 分钟）

修改 `test_anilist.py`，让它测试这 5 部：

1. 呪術廻戦（Jujutsu Kaisen）
2. 進撃の巨人（Attack on Titan）
3. 葬送のフリーレン（Frieren）
4. SPY×FAMILY
5. 推しの子（Oshi no Ko）

让 Cursor 改代码，让它**循环跑这 5 个**，每个打印 ID + 标题 + 状态。

✅ **5 个全部拿到信息 = 通过**

---

### Step 2.4：补充楽天 API 测试（30 分钟）

新建 `test_rakuten.py`，提示词给 Cursor：

```
写一个 Python 脚本，调用楽天ブックス API：
- Endpoint: https://app.rakuten.co.jp/services/api/BooksTotal/Search/20170404
- 参数：applicationId（从 .env 读）、keyword=「呪術廻戦」、format=json
- 输出：搜到的前 5 本书（标题、作者、出版日、ISBN）

需要从 .env 读 RAKUTEN_APP_ID
```

`.env` 文件内容：
```
RAKUTEN_APP_ID=你的 ID
```

✅ **能拿到 5 本相关书 = 楽天 API 通过**

---

### Step 2.5：当天结束（10 分钟）

更新 `PROGRESS.md`：

```markdown
## Day 2 ✅
- AniList 5/5 漫画拿到信息
- 楽天 API 5/5 拿到书信息
- 决策：双 API 都可用，继续

## Day 3 计划
- 写章节更新检测逻辑
```

```bash
git add . && git commit -m "Day 2: API validated"
```

---

## Day 3-4（工作日晚上各 1.5 小时）：章节更新检测

### Step 3.1：理解 AniList 章节数据问题（10 分钟）

**重要发现**：AniList 的漫画 `chapters` 字段经常返回 `null`（漫画连载中很难知道总章节数）。

→ 我们需要换一个思路：**用 `updatedAt` 字段 + 抓 chapters 的另一个数据源**

**方案 A**（首选）：用 AniList 的 **schedule 信息**（动画用，漫画无法用）
**方案 B**：抓漫画连载站的章节列表（比如 [MangaUpdates](https://www.mangaupdates.com/) 有公开 RSS）

实际上对漫画追更，**最稳的数据源是 MangaUpdates RSS feed**：
- 例：https://api.mangaupdates.com/v1/series/12345/rss

### Step 3.2：测试 MangaUpdates RSS（30 分钟）

让 Cursor 写：

```
写 Python 脚本：
1. 调用 MangaUpdates 公开 API（https://api.mangaupdates.com/v1/）
2. 搜索「Jujutsu Kaisen」
3. 拿到 series_id
4. 用 series_id 拉最新 10 章信息
5. 输出：章节号、章节标题、发布日期
```

✅ **拿到最近 10 章 = 数据源问题解决**

❌ **如果 MangaUpdates 不行**，备用：
- Comic Vine API
- Mangadex API（https://api.mangadex.org/docs/）— **推荐**，更全
- 抓 Jump+ 公开 sitemap

### Step 3.3：写章节更新检测器（45 分钟）

让 Cursor 写 `chapter_watcher.py`：

```
写 Python 脚本：
1. 维护一个 watch_list.json：
   {
     "Jujutsu Kaisen": { "last_chapter": 245, "data_source": "mangadex" },
     "Frieren": { "last_chapter": 130, "data_source": "mangadex" }
   }
2. 每次跑：
   - 对每个作品调 API 拉最新章节号
   - 如果新章节号 > last_chapter，打印 "NEW CHAPTER: [作品] ch [新号]"
   - 更新 watch_list.json
3. 每 30 分钟跑一次（用 schedule 库）
```

跑这个脚本，**让它在你电脑后台跑 24 小时**：

```bash
python chapter_watcher.py
```

### Step 3.4：等真实新章节（24 小时被动等）

**这是最重要的验证**：你的脚本必须能在真实场景里检测到新章节。

- 大多数日漫周更新（周一/三/五），轻小说月更
- 24 小时内大概率有 1-2 部更新

✅ **看到 "NEW CHAPTER: ..." 打印 = 核心逻辑成立**

❌ **24 小时没动静**：
- 可能你列的作品都没更新（正常）
- 改成跑 48 小时
- 或者手动改 watch_list.json 的 last_chapter 减 1，看脚本能否发现

---

## Day 5-6（周末，3-4 小时）：部署到 Cloudflare Workers

### Step 5.1：把 Python 脚本翻成 TypeScript（90 分钟）

Cloudflare Workers 不跑 Python，要 JavaScript/TypeScript。

让 Cursor 干：
```
把 chapter_watcher.py 翻译成 Cloudflare Workers 的 TypeScript：
1. 用 fetch API 调 Mangadex/AniList
2. 用 Cloudflare KV 存 watch_list（不用 JSON 文件）
3. 用 Cron Triggers 每 30 分钟跑
4. 检测到新章节 → 调用 SendGrid API 发邮件给我
```

### Step 5.2：部署到 Cloudflare（45 分钟）

```bash
# 1. 安装 wrangler
npm install -g wrangler

# 2. 登录
wrangler login

# 3. 创建 Workers 项目
wrangler init chapterping-watcher
cd chapterping-watcher

# 4. 把 Cursor 生成的代码贴到 src/index.ts

# 5. 创建 KV namespace
wrangler kv:namespace create WATCH_LIST

# 6. 在 wrangler.toml 加入 KV 绑定 + Cron Trigger
# [triggers]
# crons = ["*/30 * * * *"]

# 7. 部署
wrangler deploy
```

✅ **部署成功 + Workers Dashboard 看到新 Worker = 通过**

### Step 5.3：监测 24 小时（被动）

- Cloudflare Dashboard → Workers → ChapterPing-Watcher → Logs
- 看每 30 分钟是否触发
- 看真实更新时是否发邮件

✅ **收到至少 1 封 "新章节" 邮件 = 整个 pipeline 通过**

---

## Day 7（周日）：决策点

### Step 7.1：填决策表（30 分钟）

打开 `PROGRESS.md`，填这个表：

| 验证项 | 通过 | 备注 |
|-------|------|-----|
| Apple Developer 通过 | ☐ | |
| AniList API 能拉作品信息 | ☐ | |
| 楽天 API 能拉日本书信息 | ☐ | |
| Mangadex API 能拉章节列表 | ☐ | |
| 章节更新检测器能跑 | ☐ | |
| Cloudflare Workers 部署成功 | ☐ | |
| 收到至少 1 封新章节邮件 | ☐ | |

### Step 7.2：决策

**全部 7 项通过** → ✅ **GO**：下周开始 [Week 2: iOS MVP](./week2-ios-mvp.md)

**1-3 项失败但可修复** → ⚠️ **GO 但延后**：
- API 限流：加 cache 重试
- Workers 不稳定：换 Vercel Cron
- 邮件不发：换 Resend / Mailgun

**关键 API 死路**（AniList + Mangadex 都不可用）→ ❌ **NO-GO**：
- 立即启动 Backup：[Path A AI Pixel Art](../research/path-validation/) 重新启动
- 不要硬撑

---

## Week 1 总结

✅ **本周不写产品代码**，只验证 4 件事：
1. 数据能拉（AniList + 楽天 + Mangadex）
2. 章节更新能检测
3. 部署能跑
4. 通知能发

❌ **本周失败的明确信号**：
- API 全部限流不可用（极小概率）
- Cloudflare Workers 政策不允许此用途

---

## 下一步

打开 [week2-ios-mvp.md](./week2-ios-mvp.md)，开始 Day 8。
