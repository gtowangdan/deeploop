# Week 3: 付费 + 上架（Day 15-21）

> **本周目标**：RevenueCat 集成 + ASO 资产 + 苹果审核通过
> **总投入**：12-14 小时

---

## Day 15-16（周一周二晚各 2 小时）：RevenueCat 付费

### Step 15.1：注册 RevenueCat（15 分钟）

1. 打开 https://app.revenuecat.com/signup
2. 用邮箱注册
3. 创建 Project：`ChapterPing`
4. 选 iOS 平台

### Step 15.2：在 App Store Connect 创建订阅产品（45 分钟）

1. 打开 https://appstoreconnect.apple.com
2. My Apps → + → New App
3. 填写基本信息：
   - Platform: iOS
   - Name: `ChapterPing`
   - Primary Language: Japanese（日本市场首发）
   - Bundle ID: `com.yourname.chapterping`
   - SKU: `chapterping001`
4. 创建好后，左侧 Subscriptions
5. 点 + 创建：
   - Reference Name: `ChapterPing Pro Monthly`
   - Product ID: `com.yourname.chapterping.pro.monthly`
   - Subscription Group: 新建 `Pro`
6. 设置价格：**¥600/月**（约 $4.99）
   - 同时创建年订阅 `pro.yearly` ¥3,800/年（约 $29.99）
7. 加多语言描述（先填日文，后面 Cursor 翻其他）：
   - Display Name: `ChapterPing Pro`
   - Description: `無制限の作品追跡、章節通知、Widget、Live Activity`

### Step 15.3：在 RevenueCat 配置（30 分钟）

1. RevenueCat → Project → App → Apps → + iOS
2. 上传 App Store Connect 的共享密钥（App Store Connect → Users and Access → Keys → App Store Connect API → 创建）
3. 同步产品（自动从 App Store Connect 拉）
4. 创建 Entitlement：`pro`
5. 把 `pro.monthly` 和 `pro.yearly` 都关联到 `pro` entitlement

### Step 15.4：iOS 集成 RevenueCat（30 分钟）

`ChapterPingApp.swift` 启动时配置：

```swift
import RevenueCat

@main
struct ChapterPingApp: App {
    init() {
        Purchases.logLevel = .debug
        Purchases.configure(withAPIKey: "你的 RevenueCat API Key")
    }
    ...
}
```

提示词给 Cursor：
```
写一个 SwiftUI PaywallView：
- 顶部图标 + 标语「すべての作品を追跡しよう」
- 4 个 benefit 列表（用 SF Symbols）：
  - 無制限の作品追跡（5 部以上）
  - 章節更新の即時通知
  - iOS Widget + Live Activity
  - 中日英三言語検索
- 2 个购买选项：月 ¥600 / 年 ¥3,800（年付省 47%）
- 「購入を復元する」按钮
- 用 RevenueCat Purchases.shared.purchase()

参考：https://www.revenuecat.com/docs/integrations/swiftui-paywall
```

### Step 15.5：付费墙触发逻辑（30 分钟）

提示词：
```
当用户在「閲読中」加第 6 部作品时，弹 PaywallView。

判断逻辑：
- 检查 Purchases.shared.customerInfo.entitlements["pro"]?.isActive
- isActive == false → 弹 PaywallView
```

### Step 15.6：测试沙盒购买（30 分钟）

1. App Store Connect → Users and Access → Sandbox Testers → + 创建测试账号
2. iPhone 设置 → App Store → 沙盒账号登录
3. 跑 App，弹付费墙，点购买
4. ✅ 走完支付流程 + RevenueCat 显示订阅成功 = 通过

---

## Day 17-18（周三周四晚各 2 小时）：ASO 准备

### Step 17.1：关键词调研（60 分钟）

打开 https://www.asotools.io（免费版）

跑这 3 个市场：

**日本区**搜：
- 漫画 記録
- 漫画 追跡
- 読書 記録
- ライトノベル
- ブクログ（看竞品的关键词）

记下：KD（难度）< 30 + Volume > 500 的词。预期能找到：

| 关键词 | KD | Volume | 备注 |
|-------|-----|--------|------|
| 漫画 記録 | 22 | 1200 | 主词 |
| 漫画 追跡 | 18 | 800 | 副词 |
| ライトノベル 記録 | 12 | 400 | 长尾，蓝海 |
| 読書記録 アプリ | 28 | 2500 | 高竞争但量大 |

**美国区**搜：
- manga tracker
- light novel tracker
- book tracker
- manga reading list

预期：
| 关键词 | KD | Volume |
|-------|-----|--------|
| manga tracker | 35 | 3000 |
| light novel tracker | 8 | 600 |
| anime manga tracker | 22 | 1500 |

**港台区**搜：
- 漫畫 追蹤
- 追番 漫畫
- 讀書記錄

### Step 17.2：写 App 描述（60 分钟）

让 Claude 帮你写。提示词：

```
我做了一个 iOS App「ChapterPing」，功能：
- 追踪 manga + light novel + book 三合一
- 章节级别精确通知
- 中日英三语搜索
- iOS Widget + Live Activity

请写 4 个版本的 App Store 描述：
1. 日文版（主语：日本读者）
2. 英文版（主语：英语 manga 读者）
3. 简体中文（主语：在追日漫的中国读者）
4. 繁体中文（港台读者）

每版要有：
- 30 字一句话标语（subtitle）
- 100 字短描述
- 800 字长描述（含 5 个 benefit + 3 个 use case）
- 5 个推荐关键词（用「,」分隔）

避开关键词：违反 Apple 政策的词（free, best 等夸张词）
日文版要用敬体（です/ます调）
```

### Step 17.3：截图设计（45 分钟）

需要 5 套截图（不同 CPP）：

每套 5 张，尺寸 1290×2796（iPhone 15 Pro Max）：

**截图 1**：3 tab 主界面 + 标语「30 部の作品を一目で管理」
**截图 2**：章节通知 demo + 标语「新しい章を逃さない」
**截图 3**：搜索界面 + 标语「日本語・英語・中国語で検索」
**截图 4**：Widget + 标语「ホーム画面で最新章を確認」
**截图 5**：Live Activity + 标语「ロック画面でも更新を確認」

工具：
- Figma + 模板（搜「iOS App Store Screenshots Template」）
- 或者 [Screenshots Pro](https://screenshotspro.com)（免费）
- 或 Cursor 生成 SwiftUI 截图自动化脚本

### Step 17.4：CPP 配置（45 分钟）

App Store Connect → Custom Product Pages → +

创建 5 个 CPP：

| CPP 名 | 主关键词 | 用途 |
|--------|---------|------|
| Manga Tracker (EN) | manga tracker | 美国区主推 |
| 漫画記録 (JP) | 漫画 記録 | 日本主推 |
| Light Novel | light novel tracker | 长尾蓝海 |
| 漫畫追蹤 (TW) | 漫畫 追蹤 | 港台 |
| 读书记录 (CN) | 读书记录 | 中国港澳 |

每个 CPP 用对应市场的截图。

---

## Day 19-20（周五周六，5 小时）：提苹果审核

### Step 19.1：提交前 Checklist（30 分钟）

App Store Connect → My Apps → ChapterPing → App Information：

- [ ] App Icon（1024×1024 + 各种尺寸）—— 用 Bakery 或 IconKitchen 生成
- [ ] Bundle ID 已设置
- [ ] Primary Language: Japanese
- [ ] Privacy Policy URL（**必须有**，用 Termly 免费生成）
- [ ] Support URL（用一个简单的 Notion / Vercel landing page）
- [ ] Age Rating: 12+（漫画相关）
- [ ] Category: Books
- [ ] Subcategory: Reference

### Step 19.2：上传构建（30 分钟）

Xcode → Product → Archive → Distribute App → App Store Connect → Upload

等 10 分钟（Apple 处理）后，App Store Connect → TestFlight 看构建出现。

### Step 19.3：填上架信息（60 分钟）

App Store Connect → Pricing and Availability：
- Price: Free（IAP 单独定价）
- Availability: 全部国家（或先选日本+美国+港台+欧盟测试）

App Information：
- 填好 Privacy Policy / Support URL
- Age Rating

App Privacy（必填）：
- Data Types Collected: 选你真实在收集的（用户邮箱用于通知 → User Email）
- 用 Apple 的引导工具

### Step 19.4：填这版本信息（60 分钟）

Version 1.0 → 填：
- What's New: `初回リリース。漫画・ライトノベル・本を一つのアプリで追跡できます。`
- Promotional Text: 副标语
- Description: 用 Day 17 写好的
- Keywords: 用 Day 17 调研好的（日文版用日文，逗号分隔，**100 字符限制**）
- Support URL
- Marketing URL（可空）
- App Review Information: 写测试账号 + 一行说明「This is a manga tracking app. No reading content embedded.」

### Step 19.5：提交审核（30 分钟）

→ Add for Review → Submit for Review

正常 1-3 天回复。

### Step 19.6：等待中干嘛？（被动）

- 同步开发 Web 端（不阻塞上架）：
  - Next.js + Cloudflare Workers
  - 基本搜索 + 列表（同后端）
  - 域名（Cloudflare 注册 .com $10/年）

---

## Day 21（周日）：处理审核结果

### 情况 A：通过 ✅

恭喜！立即进入 [Week 4: 冷启动](./week4-cold-start.md)。

### 情况 B：被拒 ⚠️

常见拒理由 + 应对：

| 拒理由 | 解决 |
|-------|-----|
| Guideline 4.0 - Design - Minimum Functionality | 加更多功能（多语言搜索 / 标签 / 评分） |
| Guideline 5.2.3 - Legal - Intellectual Property | **绝不内嵌阅读器**；漫画封面用 AniList CDN（公开 API） |
| Guideline 2.1 - Performance - App Completeness | 测试账号问题，重新提供 |
| Guideline 3.1.1 - Business - Payments | 付费墙必须用 IAP，不能跳 Web |

修改 → 重新提交 → 等 1-3 天

### 情况 C：审核中（24+ 小时无回复）

**正常**。日本时区周末提交可能 5 天后才回复。耐心等。

---

## Week 3 决策点

✅ **审核通过** → 下周 [Week 4: 冷启动](./week4-cold-start.md)
⚠️ **第 1 次拒** → 修改重提，**继续准备 Week 4 冷启动文案**
❌ **连续 3 次拒** → 产品定位有问题，简化（去掉漫画封面，纯文字追踪）

---

## 失败应对：审核连续被拒

**最大风险**：苹果觉得"漫画追踪"太擦边版权。

**保命方案**：
- 改名「ReadPing」（去 Manga 字眼）
- 描述改成「Reading tracker for any books and series」
- 截图去掉漫画封面，用通用书籍图标
- 重新提交

这是退路，先尝试原方案。

---

## 下一步

打开 [week4-cold-start.md](./week4-cold-start.md)。
