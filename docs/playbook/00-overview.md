# Manga Tracker 完整执行手册（30 天到第一笔收入）

> 每天打开这份文档就能照做的级别
> 不会让你思考"接下来该做什么"
> 失败应对都已写明

---

## 项目代号

**ChapterPing**（暂定，可改）

---

## 30 天总览

| 周 | 目标 | 关键 deliverable | 失败应对 |
|---|------|----------------|---------|
| Week 1 | 技术验证（不写产品代码） | AniList API 能拉到章节信息 + 通知能跑通 | API 不可用 → 转 Backup |
| Week 2 | iOS MVP | App 能跑：3 tab + 搜索 + 添加 + 通知 | 进度慢 → Week 3 顺延 |
| Week 3 | 付费 + 上架 | RevenueCat 集成 + 5 套 CPP 截图 + 苹果审核通过 | 拒审 → 修改重提 |
| Week 4 | 冷启动 + 第一笔收入 | 100 装机 + 6 付费用户 | < 50 装机 → 重发渠道 |

**总投入**：每周 12-16 小时 × 4 周 = **50-65 小时**
**总现金支出**：$99（Apple Developer）+ $20（域名）+ $30（首月 API/工具）= **$149**

---

## 周计划详细文档

- [Week 1: 技术验证](./week1-tech-validation.md) — 不写产品代码，先验证 API 假设
- [Week 2: iOS MVP](./week2-ios-mvp.md) — 用 Cursor 写 SwiftUI
- [Week 3: 付费 + 上架](./week3-paywall-launch.md) — RevenueCat + ASO + 提审
- [Week 4: 冷启动](./week4-cold-start.md) — Reddit/HN/5ch/小红书 4 渠道发帖

---

## 第 1 优先级（这个周末就做）

**只做一件事**：完成 Week 1 的 Day 1。

打开 [week1-tech-validation.md](./week1-tech-validation.md)，按上面的 Day 1 步骤照做。**2 小时内能完成**。

---

## 失败迹象 + 立即行动

| 时点 | 信号 | 立即做 |
|------|-----|------|
| Week 1 Day 7 | AniList + 楽天 + MAL 都拉不到数据 | 启动 Backup（AI Pixel Art） |
| Week 2 Day 14 | iOS MVP 跑不起来 | 简化到 1 个 tab + 1 个 API |
| Week 3 Day 21 | 苹果连续 3 次拒审 | 修改产品定位（去掉漫画封面 → 纯文字追踪）|
| Week 4 Day 30 | < 50 装机 | 第 5 周重发渠道 + 加 ASO |
| Month 3 | < 20 付费 | wedge 不对，调整 |
| Month 6 | < $1K MRR | 启动 Backup |

---

## 工具清单（开工前先准备好）

| 工具 | 用途 | 费用 |
|------|-----|------|
| Apple Developer Program | iOS 上架 | $99/年 |
| Cursor Max | 写代码 | 已订阅 |
| Claude Max | AI 推荐 + 写文案 | 已订阅 |
| Cloudflare（账号） | 后端 Workers + 域名 | 免费 |
| AniList API | 漫画/轻小说数据 | 免费 |
| 楽天ブックス API | 日本书数据 | 免费（需注册） |
| RevenueCat | 订阅管理 | 免费 < $10K MRR |
| ASOTools 免费版 | 关键词调研 | 免费 |
| GitHub | 代码仓库 | 免费 |

---

## 关键判断（不要改）

- **iOS 主体，Web 配套**（不要先做 Web，iOS 才是漫画用户入口）
- **三语 metadata 是核心 wedge**（不要妥协做单语版本）
- **章节通知准 = 卖点**（这一项做不到 = 项目失败）
- **绝不内嵌阅读器**（Apple 拒审风险高）
- **主战场日本 + 全球三语**（不只做日本，市场太小）

---

## 接下来打开 [week1-tech-validation.md](./week1-tech-validation.md) 开始 Day 1。
