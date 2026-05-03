# 5 条候选路径调研最终结论

> 调研日期：2026-05-03
> 调研方式：5 个并行 agent，全部带 WebSearch/WebFetch 拿真实数据
> 核心判断标准：闭环三问（流量+交易+积累自控）+ 用户画像匹配

---

## 调研路径与最终打分

| 排名 | 路径 | 分数 | 关键判断 |
|-----|-----|-----|---------|
| 🥇 | **AI Agent 垂直 C2C SaaS**（日本本地化） | **8.5/10** | 蓝海+技术满分+市场满分+不需英文营销 |
| 🥇 | **Telegram Bot + Stars**（日华双语 AI niche） | **8.5/10** | Stars 0 抽成+冷启动快+大盘子 |
| 🥉 | **iOS C2C App + Web 配套** | 7/10 | HabitKit 类有真实路径，但 18-24 月才出收入 |
| 4 | **Mac 桌面应用直销** | 6/10 | 流量命门：成功者全靠英文 IP |
| 5 | **自有域名工具站矩阵** | 4/10 | HCU + AI Overview 双杀，结构性死路 |

---

## 核心洞察：Top 2 是同一条路的两种形态

**AI Agent 垂直 C2C SaaS** 和 **Telegram Bot AI niche** 不是二选一，而是**可以叠加**的统一战略：

```
核心产品：日本本地化 AI Agent
（如「確定申告 AI 助手」「就活 AI 助手」「介護申請 AI 助手」）
              ↓
         分发渠道矩阵
              ↓
   ┌──────────┬──────────┬──────────┐
   │  自有 Web   │  Telegram   │ iOS App  │
   │  Stripe    │   Stars     │  IAP/Web │
   │  日文 SEO  │  俄语东南亚 │  日本 ASO│
   │ (主品牌)   │ (快速冷启动) │ (移动端) │
   └──────────┴──────────┴──────────┘
              ↓
        统一用户库 + 邮件 list + Prompt 库
```

### 为什么这是最优解

✅ **流量自控**：日文 SEO + Telegram 内嵌 + 小红书三路冷启动
✅ **交易自控**：Stripe 主路径（5%）+ Telegram Stars 0 抽成 + Apple 15%（Small Business Program）
✅ **积累自控**：跨平台用户库、品牌、prompt 库、SEO 资产
✅ **AI 杠杆最大化**：Cursor 写 Web + Bot + iOS 三端，统一后端 API
✅ **完全不需英文营销/出镜**：日文 SEO + 中文小红书 + Telegram 病毒分享

---

## 各路径关键数据汇总

### 🥇 AI Agent 垂直 C2C SaaS（8.5/10）

**真实案例**：
- Photo AI（Pieter Levels）：$138K MRR（1 人）
- Inkitt（AI 罗曼史）：$10M/月
- BoredHumans：$733K/月（1 人）
- AI 物理治疗 agent：$41K MRR（solo）

**最适合方向（日本本土化垂直）**：
- 確定申告 AI 助手（报税）
- 就活 AI 助手（求职 + 履歴書 + 面接对策）
- 留学申請 AI 助手（中国学生赴日）
- 介護保険申請 AI 助手
- 漫画/小说创作 AI（なろう系自动续写）

**核心优势**：日本 AI 渗透率仅 26.7%（蓝海）+ 法规复杂 + 数据本地化 = 用户画像（日华+N2+20年技术）的天然护城河

[详细报告 →](./04-ai-agent-vertical-saas.md)

---

### 🥇 Telegram Bot + Stars（8.5/10）

**真实案例**：
- Mini App P2E：$35K/月（1 人）
- 付费 Channel Varlamov：€19K MRR
- 信号服务器 Discord：$14K MRR
- BoredHumans 类工具集：$733K/月

**核心优势**：
- **Telegram Stars 0 抽成**（vs Apple 30%）—— 教科书级的杠杆
- 无需英文营销/出镜
- AI Bot 4 小时即可上线 MVP
- 俄语+东南亚+印度大盘子（10 亿 MAU）

**最适合方向**：
- 日语商务邮件润色 Bot
- N2-N1 学习 Bot
- 日本签证&税务 AI 答疑
- 中日翻译同传 Bot

**风险**：
- Fragment KYC + TON→日元（日本杂所得最高 55%）
- Telegram 算法 0 推荐，靠分享冷启动

[详细报告 →](./05-telegram-discord.md)

---

### 🥉 iOS C2C App + Web 配套（7/10）

**真实案例**：
- HabitKit（Sebastian Röhl）：$40K/月，2025 全年 $600K
- 30-App Portfolio：$25K MRR
- Daylio（情绪日记）：$100K/月
- 日本 IsTalk：月入 ¥250 万（$17K）

**关键政策利好（2025）**：
- 美国区 Web 跳转链接合法（27% 抽成消失，仅美国区）
- Small Business Program：年收入 < $100 万自动 15% 抽成
- Reader App 例外类别：0 抽成（适合阅读/视频/音频/漫画 App）
- CPP（Custom Product Pages）从 35 → 70 个关键词

**残酷数据**：
- 17.3% 新 App 2 年达到 $1K MRR
- 仅 4.6% 达到 $10K MRR
- 每月新增 14,700 个订阅 App
- 大概率前 18 个月 < $1K MRR

**最适合方向**：
- 日中双语家計簿（MoneyCoach 升级版）
- 日中双语 JLPT 学习
- 日中双语番剧追踪 + 习惯结合

[详细报告 →](./02-ios-c2c-app.md)

---

### Mac 桌面应用直销（6/10）

**真实案例**：
- MacWhisper：$100K 累计（17 个月）
- Solo Mac dev：$300K 累计
- Xnapper：$6K MRR
- BoltAI：$3.8K MRR

**致命问题**：
- 成功 solo Mac dev **几乎全部依赖英文 Twitter/IP**（Jordi Bruin、Matthias、CleanShot、Screen Studio）
- 你不愿出镜+不善英文营销 = 走"少数派路径"：Setapp + SEO 长尾 + MAS 漏斗
- 现实天花板 $2K-$8K MRR，$30K+ 极难

**结论**：作为副线（Mac 端配套），不作为主路径

[详细报告 →](./01-mac-desktop.md)

---

### 自有域名工具站矩阵（4/10）

**致命问题**：
- AIO（AI Overview）蚕食 -61% CTR
- HCU 域名级惩罚（一次踩坑全废）
- OmniCalculator $500K/月 = 10+ 年 + 团队 + 3700 工具
- 12 个月做到 $5K+ 不成立

**结论**：**已淘汰**。最多作为 SaaS 的引流入口

[详细报告 →](./03-tool-site-matrix.md)

---

## 最终建议：统一战略

### 主产品：日本本土化 AI Agent

**选品建议（按优先级）**：
1. **就活 AI 助手**（履歴書/職務経歴書/ES/面接対策）—— 日本求职刚需，每年百万学生 + 转职者
2. **確定申告 AI 助手** —— 1-3 月强季节性，但每年都有
3. **留学申請 AI 助手** —— 中国学生赴日 niche，你的双语优势完美匹配

### 分发渠道（三路并行）

1. **自有 Web 站点**（主品牌，Stripe 直收）
   - 日文 SEO 长尾词矩阵
   - Programmatic SEO（Pieter Levels 模式）
   - Note.com / Qiita / Zenn 内容输出

2. **Telegram Bot**（快速冷启动，Stars 0 抽成）
   - 同一后端 API，前端 Bot UI
   - tgstat 目录 + 中文 Telegram 群（在日华人）
   - 病毒邀请奖励

3. **iOS App**（移动端入口，Apple 15% Small Business Program）
   - 同一后端 API + RevenueCat
   - 日本 ASO 长尾词
   - CPP 70 个关键词

### 预算分配（$150-$350/月）

- Apple Developer：$99/年（≈$8/月）
- 域名 + Cloudflare：$2/月
- Claude API（用户付费 cover）：$50-100/月（前期）
- Vercel + Supabase：免费 tier 起步
- Mangools / Ahrefs Lite：$30/月（SEO 工具）
- 余额：留给 Telegram RichAds 测试 / 小红书推广

### 12 个月目标

- **月 1-2**：选定垂直 + Note/小红书发问题验证 + 收 50 个 waitlist
- **月 3-4**：MVP 上线（Web + Telegram Bot 双发，4 周内）
- **月 5-6**：日文 SEO 内容（20 篇长尾） + Programmatic SEO 100 页
- **月 7-9**：iOS App 配套上架，目标 ¥500K MRR（$3.3K）
- **月 10-12**：第二个垂直 agent（共享代码） + 目标 $10K MRR

### 现实预期

- 保守：月入 $1K-$3K（足够 Niche 方向都可达）
- 中位：月入 $3K-$8K（完成第一年闭环）
- 乐观：月入 $10K+（叠加多产品+渠道）

---

## 风险与对冲

| 风险 | 概率 | 对冲 |
|------|-----|------|
| 日本市场 niche 选错 | 中 | M1-M2 用 Note/小红书发问题验证再做 |
| Telegram 平台政策变化 | 低 | 自有 Web 站点是基底，Telegram 只是渠道 |
| Apple 政策反复 | 低 | iOS 仅作配套，主战场在 Web |
| 大厂吃掉（ChatGPT 加新功能） | 高 | 选**日本法规壁垒重**的垂直，AI 替代不了 |
| API 涨价 | 低 | Claude/GPT 价格在持续**降**而非涨 |
| 18 个月没收入心理崩溃 | 中 | 第一天就收钱（哪怕 5 个用户） |

---

## 立即可做的 5 件事

1. **本周末**：选 1 个垂直方向（强烈建议从「就活 AI 助手」起步）
2. **本周**：在 Note.com + 小红书发"我打算做 X，需要 5 个真实用户聊聊痛点"
3. **下周**：跑 Ahrefs 日文长尾词，找 KD<10 的目标关键词 20 个
4. **下下周**：Cursor 写 MVP（Next.js + Supabase + Stripe + Anthropic SDK）
5. **第 4 周**：上线 Web 版 + Telegram Bot 版，收第一个付费

---

## 数据来源

详见各路径独立报告：
- [01-mac-desktop.md](./01-mac-desktop.md)
- [02-ios-c2c-app.md](./02-ios-c2c-app.md)
- [03-tool-site-matrix.md](./03-tool-site-matrix.md)
- [04-ai-agent-vertical-saas.md](./04-ai-agent-vertical-saas.md)
- [05-telegram-discord.md](./05-telegram-discord.md)

每份报告都带具体 URL 来源，可独立验证。
