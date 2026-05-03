# iOS C2C App + Web 配套 调研报告

> 调研日期：2026-05-03
> **可行性评分：7/10**

---

## 市场残酷真相（2026 数据）

来自 RevenueCat《State of Subscription Apps 2026》（11.5 万+ App、$160 亿+ 收入）：

- **每月新增 14,700 个订阅 App**（4 年涨 7 倍）
- **2020 年前发布的老 App 仍占 69% 总收入**
- **新 App 2 年内达到 $1K MRR 的仅 17.3%**，达到 $10K MRR 的仅 **4.6%**
- **First Month 流失 = 35% 全年取消**
- 头部 10% 增长 306%+，底部严重萎缩 = 马太效应加剧

---

## 真实赚钱案例

| 名字 / 产品 | 类型 | 收入数据 |
|---|---|---|
| **HabitKit**（Sebastian Röhl） | 习惯追踪，纯 ASO | **$40K/月稳定**，2025 全年 $600K+ |
| **30-App Portfolio**（Max Artemov） | ASO 组合 | **$22K/月**（1 年），2025 扩到 $25K+ MRR |
| **App Portfolio（匿名）** | 移动 App 组合 | **$185K/月** |
| **重建账号案例（匿名）** | Apple 冻结后重建 | **$60K/月** |
| **Habit Pixel**（solo） | 习惯追踪 | $1K MRR / 8 个月 |
| **Daylio** | 情绪/日记 | **~$100K/月**（Sensor Tower 估算） |
| **MoneyCoach**（多设备同步） | 个人财务 iPhone+iPad+Mac+Watch+Vision Pro | 多次 Apple 推荐 |
| **Bandle**（Web→iOS） | 音乐猜谜 | Web 端转化率 60%，整体用户 +30% |
| **NotePlan** | 任务+笔记+日历 Mac+iOS | Setapp + 自有订阅 |
| **IsTalk**（日本 LINE 分析） | C2C 工具 | **¥250 万/月（$17K）**，订阅用户 4500+ |
| **TypingMind** | ChatGPT 替代 UI | **$50K MRR**（2024 年初） |

**真实分布**：
- 大多数 first app 首年 < $100
- 一开发者 2025 年 8 个产品共赚 $1,464（典型底部）
- 2-5 年才能"养活自己"是基线

---

## 30% 抽成怎么破（2025-2026 政策）

### 关键转折：2025 年 4 月 30 日 Epic v. Apple 美国判决

- **美国区**：iOS App 内可放外部支付链接，Apple **不能再收 27% 抽成**
- 开发者拿 100%（扣 Stripe 通道费）
- 但 Web 转化率比 IAP 低 30%+（A/B 测试数据）

### Small Business Program（关键）

**年收入 < $100 万自动 15% 抽成**（不是 30%），起步阶段默认适用

### Reader App 例外

阅读/视频/音频/书 App 可以申请，0 抽成（外链账户）

### 三种模式对比

| 模式 | 抽成 | 适合 |
|---|---|---|
| **纯 IAP** | 30%（Small Business 15%） | 纯 iOS |
| **Reader App** | 0% | 阅读/视频/漫画 |
| **混合（IAP + Web 链接）** | 看引导 | 大多数订阅 |
| **Web-first** | 0% | 已有 Web 流量 |

### 跨平台订阅（Web 注册 → iOS 登录）

- **完全合法**，Spotify/Netflix 模式
- 工具：**RevenueCat Web Billing**（Stripe）

---

## C2C 兴趣社区方向（按用户匹配度）

| 方向 | 市场数据 | 用户优势匹配 | 推荐 |
|---|---|---|---|
| **习惯/情绪/日记** | $1.7B → $5.5B（2033） | Mac+iOS 协同 | ★★★★ |
| **个人财务（家計簿）** | 日本 + 中国双层 | 极高（双语） | ★★★★ |
| **冥想/睡眠** | 数十亿美元 | 中（音频内容） | ★★ |
| **追番/动漫工具** | 日华独有视角 | 极高 | ★★★ |
| **TCG/游戏辅助** | Pokemon TCG 爆 | 中（变现弱） | ★★ |
| **日中语言学习** | 日华最强 niche | 极高 | ★★★ |
| **漫画/轻小说阅读器** | Reader App 0 抽成 | 高 | ★★★ |
| **Vtuber/二次元** | 日本特有 | 极高 | ★★★ |

### 最佳推荐组合

1. **日中双语家計簿 + Mac 端**（MoneyCoach 升级版）
2. **日中双语 JLPT 学习 + Web 题库**
3. **追番 + 日语学习 hybrid**

---

## ASO 真实玩法

### 关键政策（2025）
- **CPP（Custom Product Pages）从 35 → 70 个关键词**
- 每个 CPP 可对应一个长尾意图

### 多语言市场对比

| 市场 | 竞争 | 付费意愿 | 你的优势 |
|---|---|---|---|
| 🇯🇵 日本 | 中 | **高** | ⭐⭐⭐⭐⭐ N2 + 在地 |
| 🇨🇳 中国 | 极高 | 中 | ⭐⭐⭐⭐ 母语 |
| 🇺🇸🇬🇧 欧美 | 极高 | 极高 | ⭐⭐ 不善英文 |
| 🇰🇷🇹🇼🇸🇬 | 中 | 中高 | ⭐⭐⭐ 文化相近 |

### 中国区残酷真相

- **个人开发者必须 ICP 备案**
- **游戏必须版号 + 营业执照 + 批复函**
- 个人开发者基本做不了游戏
- **结论**：初期不做中国区，做日本 + 港台 + 北美 + 欧洲

---

## 闭环三问打分

- **流量 A：6/10** —— App Store 算法占 90%，但 CPP + 日文/中文 niche 可拿 30-40% 自有杠杆
- **交易 B：8/10** —— Small Business 15% + 美国区 Web 0 抽成 + RevenueCat 跨平台
- **积累 C：8/10** —— ASO 关键词 + iOS+Mac+Watch+VisionPro 代码复用 + 用户邮件

---

## AI 杠杆

- Cursor + Claude 写 SwiftUI：3-5x 速度提升
- AI 关键词调研 + 多语言文案
- Midjourney/DALL-E 出图标 + 截图变体
- [Eronred/aso-skills](https://github.com/Eronred/aso-skills) ASO 技能包

---

## 12 个月行动清单

### 第 1 个月：选品 + 关键词验证
- 锁定 1 主方向（推荐双语家計簿 或 JLPT 学习）
- ASOTools 跑日/美/港台关键词
- 找 5-10 个 KD<50 + Volume>1000 长尾词
- 注册 Apple Developer（$99，Small Business 自动）

### 第 2-3 个月：MVP
- Cursor + Claude 写 SwiftUI（6 周做 v0.1 iOS+Mac）
- RevenueCat 集成
- 硬付费墙 + 17-32 天试用

### 第 4 个月：上架 + 多区域 ASO
- 70 个 CPP 配 70 个关键词意图
- AI 生成日/中/英三语描述
- 提交日 + 美 + 港台 + 韩 + 欧（**跳过中国大陆**）

### 第 5-6 个月：内容引流（不出镜）
- 日文 X 每天 1 条开发日记（截图）
- Zenn/Qiita 月更技术博客
- 中文小红书/即刻同步（图文，不出镜）

### 第 7-9 个月：迭代 + 第二款
- 看 RevenueCat 数据：Cohort 留存 + 付费墙转化
- < $500 MRR → 大概率方向错，回选品
- $500-$2K → 加相关 niche 小 App
- > $2K → 加深 + Web 端配套

### 第 10-12 个月：Web 端 + 0 抽成
- 美国区接 RevenueCat Web Billing + Stripe
- Web 端 SEO（日/中/英博客）
- Mac 版上 Setapp（被动收入）

### 12 个月目标
- **底线**：$300-$1K/月（验证方向）
- **中等**：$1K-$3K MRR（17.3% 上半区）
- **乐观**：$5K-$10K MRR（HabitKit 第 2 年）
- **不现实**：$20K+

---

## 用户可行性总评：7/10

**$5K-$10K MRR 概率约 25-35%**（vs 整体 4.6%），前提：
1. 选**日中双语 niche**（不做纯英文/纯中国大陆）
2. 选**非游戏方向**
3. 接受 12-18 月可能 < $1K MRR
4. **避开 Portfolio 30-app 模式**（账号被封风险），改走 **HabitKit 单品深挖**
5. **从一开始 iOS+Mac 双端**（绕开纯 iOS 红海）

**最大风险**：18 个月没起色就放弃 → 90% 死在这里

---

## 数据来源

- [State of Subscription Apps 2026 - RevenueCat](https://www.revenuecat.com/state-of-subscription-apps/)
- [HabitKit 2025 Recap](https://sebastianroehl.substack.com/p/2025-the-year-that-changed-everything)
- [Max Artemov 30-App Portfolio](https://www.indiehackers.com/post/tech/from-failed-app-to-30-app-portfolio-making-22k-mo-in-less-than-a-year-myy3U7K9evxGOVOHti8s)
- [Apple Anti-Steering Ruling](https://www.revenuecat.com/blog/growth/apple-anti-steering-ruling-monetization-strategy/)
- [App Store Small Business Program](https://developer.apple.com/app-store/small-business-program/)
- [Reader Apps - Apple](https://developer.apple.com/support/reader-apps/)
- [RevenueCat Web Billing](https://www.revenuecat.com/billing)
- [Apple Notarization](https://developer.apple.com/documentation/security/notarizing-macos-software-before-distribution)
- [日本 IsTalk 月收 250万円](https://note.com/keitaaaan/n/n6b4ff16d9835)
- [aso-skills GitHub](https://github.com/Eronred/aso-skills)
- [App Radar ASO 2025](https://appradar.com/academy/apple-app-store-optimization-aso)
