# Mac 桌面应用直销（自有官网）调研报告

> 调研日期：2026-05-03
> **可行性评分：6/10**

---

## 真实赚钱案例

| 名字 / 产品 | 类型 | 收入数据 | 渠道 |
|---|---|---|---|
| **MacWhisper**（Jordi Bruin） | AI 转录 | $100K 累计 + 57,574 次下载，Pro 版 $69 终身 | Gumroad + 自有官网 + MAS 双发 |
| **匿名 Solo Mac dev** | Mac 工具 | $300,000 累计收入 | 自有官网 + Paddle |
| **Xnapper** | C2C 截图工具 | $6,000 MRR | 自有官网 + Setapp |
| **BoltAI** | C2C AI 工具 | $3,839 MRR | 自有官网 |
| **PDF Pals** | C2C AI PDF | $2,264 MRR | 自有官网 |
| **30-app portfolio dev** | Mac/iOS 组合 | $22K/月 | 自有官网 + 长尾 SEO |
| **Window-management Mac app** | C2C 工具 | $1,500/月 | 自有官网 |
| **CleanShot X** | C2C 截图（旗舰） | 估算 8 位数 ARR | 自有官网 + Setapp |
| **Rogue Amoeba** | C2C 音频 | 三人小团队，百万营收级 | 100% 自有官网 |
| **AMA macOS app** | 未公开 | $10K 两个月 | 自有官网 |

**残酷诚实**：MacWhisper $100K 是 **17 个月累计**，不是 MRR。"$5K-$50K MRR" 真实案例集中在 **AI 工具类**（2023-2025 风口），其他品类要做到 $5K MRR 通常需 2-3 年沉淀。

---

## 致命瓶颈：流量

成功 solo Mac dev **几乎全部强依赖英文 Twitter/IP**：
- Jordi Bruin、Matthias Gansrigler、Screen Studio (Adam Lyttle)、CleanShot 团队都是

**用户的硬伤**：
- 不愿出镜
- 不善英文营销

→ **走"少数派路径"**：Setapp 被动 + SEO 长尾 + MAS 漏斗
→ **天花板**：$2K-$8K MRR，$30K+ 极难

---

## 流量来源（按效果排序）

1. **Setapp 上架**：70/30 分成 + 推荐再奖 20%（最高 90%）—— **不需要英文营销**
2. **SEO + 长尾词**（中文/日文 你的母语优势）
3. **MAS 引流**：用 MAS 免费版 → 引流到自有官网 Pro 版
4. **Hacker News**：次级渠道，爆款带 5K-50K 流量但 churn 极快
5. **Product Hunt**：2024 年算法改版后大幅衰落（转化率 3.1%）
6. **Indie Hackers**：转化率 23.1%（高于 PH 8 倍）

---

## 支付/技术栈

| 平台 | 费率 | License 支持 | 推荐 |
|---|---|---|---|
| **Paddle Billing** | ~5%+0.5 | 订阅强 | 月入 $2K+ 后切换 |
| **Stripe** | 2.9%+0.30 | 需自建 license 系统 | 灵活但工作量大 |
| **Lemon Squeezy** | 5%+0.50 | 内置 license key | 中端选择 |
| **Gumroad** | 10%（2025 起 MoR） | 简单 license | **起步首选**（30 分钟上线） |

**License key 系统**：自建（Sparkle EdDSA + 简单 server）即可
**Notarization**：必须做，notarytool（altool 已死）
**模式**：一次性买断 + 主版本升级折扣（C2C 友好，2025 反订阅疲劳趋势）

---

## C2C Mac 工具赚钱品类

1. **AI 包装类**：MacWhisper / BoltAI / PDF Pals / MacGPT
2. **截图/录屏**：CleanShot X / Xnapper / Kap / Screen Studio
3. **窗口/键盘/启动器**：Rectangle Pro / Raycast / BetterTouchTool
4. **笔记/写作**：Bear Pro / Drafts / iA Writer
5. **AI + 笔记**：Reflect / Heptabase
6. **音频**：Rogue Amoeba 系
7. **菜单栏小工具**：iStat Menus / One Switch / Bartender
8. **图片/设计辅助**：Acorn / Pixelmator Pro / Permute
9. **翻译/输入法**：日本市场天然机会
10. **生产力 + 隐私**：1Blocker / Little Snitch

**避坑**：游戏、健康冥想、纯 Web 可替代的工具

---

## 闭环三问打分

- **流量 A：5/10** —— 你不做英文营销，主要靠 SEO + Setapp 兜底
- **交易 B：9/10** —— Paddle/Gumroad 通道费 5-10%，95% 净利润可行
- **积累 C：7/10** —— 邮件 list + 代码复用强（Swift/SwiftUI）

---

## 12 个月行动清单

- M1-M2：选品 + 注册 Apple Developer + landing page + 邮件订阅 50 waitlist
- M3-M4：Swift + Sparkle + license 系统 + Paddle/Gumroad
- M5：Soft Launch 给 waitlist + 提交 Setapp + 中文 SEO
- M6：HN Show HN + Indie Hackers 长贴 + Note.com 日文长贴
- M7-M9：MAS 双发 + Setapp 通过 + 邮件 newsletter
- M10-M12：第二款 app（复用代码） + Google Ads 长尾词测试

**12 个月预期**：保守 $2K MRR，乐观 $5K MRR

---

## 用户可行性总评：6/10

**残酷一句话**：Mac 桌面应用直销是手艺人的活，**手艺好且会自我营销**才能成。你手艺一流但拒绝营销，路径不是不能走，只是天花板写在脸上。比起 Mac 桌面 C2C，你画像更适合 **iOS 消费者订阅 app + Web 配套**（CardLink 方向）。

**结论**：作为副线（Mac 端配套），不作为主路径

---

## 数据来源

- [Indie Hackers: $300K Solo Mac Dev AMA](https://www.indiehackers.com/post/i-grew-my-revenue-to-300-000-as-a-solo-indie-mac-developer-ama-c200c97cfc)
- [Indie Hackers: $100K MacWhisper](https://www.indiehackers.com/post/100-000-revenue-with-a-simple-mac-app-9e4976599c)
- [Indie Hackers: 30-app $22K/mo](https://www.indiehackers.com/post/tech/from-failed-app-to-30-app-portfolio-making-22k-mo-in-less-than-a-year-myy3U7K9evxGOVOHti8s)
- [Eternal Storms: Selling Outside MAS Part II](https://blog.eternalstorms.at/2024/12/18/selling-outside-of-the-mac-app-store-part-ii-lets-meddle-with-paddle/)
- [Setapp Revenue Distribution](https://docs.setapp.com/docs/distributing-revenue)
- [Apple Notarization Docs](https://developer.apple.com/documentation/security/notarizing-macos-software-before-distribution)
- [Indie Maker Analytics 2024-2025](https://indielaunches.com/indie-maker-analytics-2024-2025-projects/)
- [DEV: Why PH No Longer Works](https://dev.to/indiehackerksa/why-product-hunt-no-longer-works-for-indie-founders-aom)
- [CleanShot X Pricing](https://cleanshot.com/pricing)
- [Rogue Amoeba](https://rogueamoeba.com/)
