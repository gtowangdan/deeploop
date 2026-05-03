# Week 2: iOS MVP（Day 8-14）

> **本周目标**：iOS App 能跑通 3 tab + 搜索 + 添加 + 章节通知
> **总投入**：14-16 小时
> **前置条件**：Week 1 全部通过

---

## Day 8（周一晚 2 小时）：Xcode 项目初始化

### Step 8.1：开 Xcode 新项目（20 分钟）

1. 打开 Xcode（如果没装：App Store 搜「Xcode」，**6GB 大，提前装好**）
2. File → New → Project
3. **iOS → App**
4. Product Name: `ChapterPing`
5. Team: 选你的 Apple Developer 账号
6. Organization Identifier: `com.yourname.chapterping`
7. Interface: **SwiftUI**
8. Language: **Swift**
9. 不勾 Core Data / Tests（暂不需要）
10. 保存到 `~/projects/chapterping/ios/`

### Step 8.2：跑通 Hello World（15 分钟）

1. 选 iPhone 15 模拟器
2. 按 ▶️ Run
3. ✅ 看到「Hello, world!」= 通过

### Step 8.3：装依赖（25 分钟）

File → Add Package Dependencies → 搜以下加上：

| Package | URL |
|---------|-----|
| **Apollo iOS**（GraphQL 客户端，调 AniList） | `https://github.com/apollographql/apollo-ios` |
| **RevenueCat** | `https://github.com/RevenueCat/purchases-ios` |
| **Kingfisher**（图片缓存） | `https://github.com/onevcat/Kingfisher` |
| **OSLog**（系统自带不用装） | - |

✅ **Build 成功无报错 = 通过**

### Step 8.4：建项目结构（30 分钟）

让 Cursor / Claude Max 干：

提示词：
```
帮我设计一个 SwiftUI 项目结构，App 名 ChapterPing，功能：
- 3 个 tab：閲読中 / TBR（想看）/ 完読
- 每个 tab 显示作品列表（卡片样式）
- 卡片有：封面、标题（中日英）、最新章节、距上次更新天数

请给出文件结构（建议哪些 Group / 文件夹）和每个文件的职责。
不要写代码，先给结构。
```

Cursor 会给类似：
```
ChapterPing/
├── App/
│   └── ChapterPingApp.swift
├── Features/
│   ├── Reading/
│   │   ├── ReadingView.swift
│   │   └── ReadingViewModel.swift
│   ├── TBR/
│   ├── Completed/
│   └── AddSeries/
├── Models/
│   ├── Series.swift
│   └── Chapter.swift
├── Services/
│   ├── AniListService.swift
│   ├── MangadexService.swift
│   └── RakutenService.swift
├── Components/
│   └── SeriesCard.swift
└── Utils/
```

按这个结构在 Xcode 创建对应 Group 和空 Swift 文件。

### Step 8.5：保存进度

```bash
cd ~/projects/chapterping/ios
git add . && git commit -m "Day 8: Xcode project init"
```

更新 PROGRESS.md。

---

## Day 9-10（每天 2 小时）：核心 UI（3 tab + 卡片）

### Step 9.1：写 TabView 主入口（30 分钟）

打开 `ChapterPingApp.swift`，让 Cursor 帮你写：

提示词（在 Cursor 里 Cmd+L 打开 chat）：
```
写一个 SwiftUI TabView，3 个 tab：
- 閲読中（icon: book.fill）
- TBR（icon: bookmark.fill）
- 完読（icon: checkmark.circle.fill）

每个 tab 暂时用占位 View（如 Text("Reading list")）。
适配 iOS 17+。
```

按 Cursor 给的代码替换 `ContentView.swift`，跑模拟器。

✅ **看到 3 个 tab 能切换 = 通过**

### Step 9.2：写 Series Model（30 分钟）

`Models/Series.swift`：

提示词：
```
写一个 Swift struct Series:
- id: Int
- titleRomaji: String
- titleEnglish: String?
- titleNative: String  // 日文原版
- titleChinese: String?  // 我们自己加的
- coverImageURL: URL?
- latestChapter: Int?
- latestChapterDate: Date?
- status: SeriesStatus（enum: reading/tbr/completed）
- source: DataSource（enum: anilist/mangadex/rakuten）

加 Identifiable + Codable + Hashable
```

### Step 9.3：写 SeriesCard 组件（45 分钟）

`Components/SeriesCard.swift`：

提示词：
```
写一个 SwiftUI View，名 SeriesCard，输入 Series：
- 左边：封面图（用 Kingfisher 加载，圆角，60x80）
- 右边：
  - 第一行：日文标题（粗体）
  - 第二行：英文标题（小字灰色）
  - 第三行：「ch.245 · 3 日前」格式

整体 Card 风格：圆角 12，浅色背景，阴影
适配深色模式
```

### Step 9.4：写 ReadingView 列表（45 分钟）

`Features/Reading/ReadingView.swift`：

提示词：
```
写 SwiftUI View ReadingView：
- ScrollView 包 LazyVStack
- 显示一个 [Series] 数组（先用 mock 数据）
- 每项用 SeriesCard
- 顶部 Navigation 标题「閲読中」
- 顶部右上角按钮「+」（点击打开 AddSeriesView，先用 sheet）

mock 数据：5 部漫画（呪術廻戦、進撃の巨人、フリーレン、SPY×FAMILY、推しの子）
```

跑模拟器：

✅ **看到 5 张卡片列表 = 通过**

---

## Day 11（周三晚 2 小时）：搜索 + 添加作品

### Step 11.1：AniList GraphQL 集成（60 分钟）

`Services/AniListService.swift`：

提示词：
```
写 SwiftUI Service AniListService：
- 用 Apollo iOS 客户端
- Endpoint: https://graphql.anilist.co
- 函数 search(query: String) async -> [Series]
- GraphQL query 拉：id, title (romaji/english/native), coverImage, status, chapters

参考 Apollo iOS 文档：https://www.apollographql.com/docs/ios/
```

如果 Apollo iOS 配置复杂，可以先用 URLSession + raw GraphQL：

```swift
let query = """
query ($search: String) {
  Page(page: 1, perPage: 10) {
    media(search: $search, type: MANGA) {
      id
      title { romaji english native }
      coverImage { large }
      status
    }
  }
}
"""
```

### Step 11.2：AddSeriesView（30 分钟）

`Features/AddSeries/AddSeriesView.swift`：

提示词：
```
写 SwiftUI View AddSeriesView：
- TextField 搜索框（占位文字「作品名を検索」）
- 搜索结果列表（用 SeriesCard）
- 用户点某项 → 添加到当前列表（@Binding 或 NotificationCenter）
- 用 .onChange 触发搜索（debounce 300ms）

调用 AniListService.search()
```

### Step 11.3：测试搜索（30 分钟）

模拟器跑：
1. 点「+」
2. 搜「Jujutsu Kaisen」
3. ✅ 看到搜索结果列表

✅ **搜索结果出来 = 通过**

---

## Day 12（周四晚 2 小时）：本地存储 + 章节通知

### Step 12.1：本地存储用 SwiftData 或 CoreData（45 分钟）

iOS 17+ 用 SwiftData 最简单。

提示词：
```
用 SwiftData 把 Series 持久化：
- 给 Series 加 @Model 注解（如果是 class）或 @Observable
- 在 ChapterPingApp 里加 .modelContainer(for: Series.self)
- ReadingView 用 @Query 读取 status == .reading 的 Series

参考：https://developer.apple.com/documentation/swiftdata
```

### Step 12.2：章节通知逻辑（45 分钟）

App 端**不**做后台轮询（耗电）。让 Cloudflare Workers（Week 1 写的）发 push。

App 端只需要：
1. 申请通知权限
2. 注册 device token
3. 把 token 上传到 Cloudflare Workers KV

提示词：
```
写 Swift 代码：
1. App 启动时申请 UNUserNotificationCenter 权限
2. 注册远程通知，拿到 device token
3. POST 到 https://chapterping-watcher.[你的子域].workers.dev/register
   body: { "deviceToken": "...", "userId": "anonymous-uuid" }

App 端不做轮询，通知由 Workers 推送
```

### Step 12.3：APNs 配置（30 分钟）

1. 打开 https://developer.apple.com/account
2. Certificates, IDs & Profiles → Keys → +
3. 选 「Apple Push Notifications service (APNs)」
4. 下载 .p8 文件，**保管好不能再下载**
5. 记录 Key ID 和 Team ID
6. 把 .p8 + 配置写到 Cloudflare Workers Secrets：

```bash
wrangler secret put APNS_KEY_ID
wrangler secret put APNS_TEAM_ID
wrangler secret put APNS_BUNDLE_ID  # com.yourname.chapterping
# .p8 内容用 wrangler secret put APNS_KEY 多行输入
```

### Step 12.4：让 Workers 发 push（30 分钟）

回到 Week 1 的 Workers 项目，修改章节检测逻辑：
- 之前：发邮件
- 现在：拿 KV 里所有 deviceToken，调 APNs API 发 push

让 Cursor 写这部分。

测试：手动改 KV 里某作品的 last_chapter -1，等 30 分钟（或手动触发 Worker）。

✅ **手机收到 push 通知「呪術廻戦 ch.246 配信開始」= 通过**

---

## Day 13（周六 4 小时）：iOS Widget

### Step 13.1：加 Widget Extension（30 分钟）

Xcode → File → New → Target → Widget Extension
- Name: `ChapterPingWidget`
- 不勾 Live Activity（Day 14 加）

### Step 13.2：写 Widget UI（90 分钟）

提示词：
```
写一个 SwiftUI Widget：
- 中号 Widget（systemMedium）
- 显示「今日 3 部更新」
- 列表显示前 3 部最近更新的作品（封面 + 标题 + 章节号）
- 数据从 SwiftData 共享（用 App Group 共享数据库）
- 点击 Widget 打开 App
```

### Step 13.3：App Group 配置（45 分钟）

让 Widget 读 App 的 SwiftData 数据：
1. App 和 Widget 都开启 App Groups capability
2. 创建 group identifier `group.com.yourname.chapterping`
3. SwiftData 容器配置 `groupContainer`

详细文档：https://developer.apple.com/documentation/swiftdata/configuring-the-model-container

### Step 13.4：测试 Widget（45 分钟）

1. 加一个作品到「閲読中」
2. 退出 App
3. 长按主屏 → 添加 Widget → ChapterPing
4. ✅ Widget 显示作品 = 通过

---

## Day 14（周日 4 小时）：Live Activity

### Step 14.1：加 Live Activity（30 分钟）

ChapterPingWidget target 加 Activity：
- Info.plist 加 `NSSupportsLiveActivities = YES`

### Step 14.2：写 Live Activity UI（90 分钟）

提示词：
```
写 ActivityKit Live Activity：
- 当有新章节 push 来时，启动 Live Activity
- 锁屏 / 灵动岛显示「[作品名] ch.246 配信中」
- 5 分钟后自动消失

参考：https://developer.apple.com/documentation/activitykit
```

### Step 14.3：联调 push + Live Activity（60 分钟）

Workers 发 push 时，包含 ActivityKit token，触发 Live Activity 启动。

详细：https://developer.apple.com/documentation/activitykit/updating-and-ending-your-live-activity-with-activitykit-push-notifications

### Step 14.4：当天结束（30 分钟）

更新 PROGRESS.md：

```markdown
## Week 2 完成 ✅
- 3 tab UI 跑通
- AniList 搜索集成
- SwiftData 持久化
- Push 通知端到端跑通
- Widget 显示
- Live Activity 跑通

## Week 3 计划
- RevenueCat 付费
- ASO 准备
- 提苹果审核
```

```bash
git add . && git commit -m "Week 2 done: iOS MVP working"
git tag mvp-v0.1
git push --tags
```

---

## Week 2 决策点

✅ **MVP 全部跑通** → 下周 [Week 3: 付费 + 上架](./week3-paywall-launch.md)

⚠️ **部分卡住**（如 Live Activity 难度高） → **去掉 Live Activity 先上架**，Day 14 只做 Widget 即可

❌ **Push 通知端到端不通** → 这是核心 wedge，**必须解决**：
- 检查 APNs 证书
- 检查 Workers 调 APNs 是否正确
- 用 [Pusher Beams](https://pusher.com/beams/) 替代（免费 tier 1000 通知/月）

---

## 常见 Bug 速查

| 问题 | 原因 | 解决 |
|------|------|------|
| 模拟器收不到 push | 模拟器只支持 iOS 16+ | 用真机 |
| Workers 调 APNs 401 | JWT 签名错 | 用 `node-jose` 重新生成 |
| SwiftData crash | iOS 17 早期版本不稳 | 升级到 iOS 17.4+ |
| Widget 不刷新 | reload policy | 加 `WidgetCenter.shared.reloadAllTimelines()` |

---

## 下一步

打开 [week3-paywall-launch.md](./week3-paywall-launch.md)。
