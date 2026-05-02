# Chrome 扩展完整赚钱手册

> 副推荐路径：浏览器商店分发，AI 类扩展是当前最强风口

---

## 真实赚钱数据

| 案例 | 收入 | 模式 | 来源 |
|------|------|------|------|
| **GMass**（Gmail 群发） | $130K-$200K MRR | 订阅 SaaS | [extensionpay.com](https://extensionpay.com/articles/browser-extensions-make-money) |
| **Eightify**（YouTube AI 摘要） | ~$540K/年（$45K/月）、50% 毛利 | AI 订阅 | 同上 |
| **Easy Folders**（ChatGPT/Claude 文件夹） | $3.7K MRR、累计 $42K（上线 6 个月） | freemium 订阅 | [Indie Hackers](https://www.indiehackers.com/product/easy-folders/6-months-post-launch-my-chrome-extension-has-hit-3-700-in-mrr-and-42-000-in-total-revenue--O3qs28VAnAkcJw0j--M) |
| **Tailscan**（前端审查工具） | ~$30K ARR、95% 毛利 | 买断/订阅 | [extensionpay.com](https://extensionpay.com/articles/browser-extensions-make-money) |
| solo 开发者两扩展合计 | ~$10K MRR | 订阅 | [Starter Story](https://www.starterstory.com/ideas/chrome-extension/profitability) |

---

## 当前窗口（2025-2026）

### MV3 迁移留下的机会

- MV3 已强制（2024 全面、2025/06 移除所有 MV2 残留）
- **大量旧扩展开发者懒得迁移，留下空位**
- AI 类扩展是当前最强风口
- 来源：[Indie Hackers 机会帖](https://www.indiehackers.com/post/software-opportunity-thousands-of-chrome-extensions-are-about-to-disappear-85DQAl9yaLglihq0kkkP)

### 流量逻辑

Chrome Web Store 排名因素：
1. 安装量
2. 活跃用户数（DAU/WAU）
3. 评分（4.5+ 是关键阈值）
4. 关键词匹配
5. 更新频率

**不需要个人品牌**：上述案例几乎全部不出镜，靠商店搜索 + 早期 Product Hunt + Reddit 软发布即可冷启动。

---

## 三个最适合你的方向

### 方向 1：AI 平台增强（Easy Folders 模式）

寄生在 Claude / ChatGPT / Gemini 之上，做生产力工具。

**具体产品创意**：
- Claude 提示词管理器（按文件夹分类、批量执行、模板库）
- Claude 对话搜索 / 历史归档
- 多平台 AI 对比工具（同一个问题同时问 Claude + GPT + Gemini）
- AI 输出导出 PDF/Markdown/Notion
- AI 对话云同步（跨设备）

**为什么这条最快验证**：
- 你每天用 Claude，痛点你最清楚
- Easy Folders 6 个月做到 $3.7K MRR 已证明可行
- 不需要市场调研，自己就是用户

### 方向 2：日本本地服务增强（你的护城河）

英语圈对手做不动的方向。

**具体产品创意**：
- 楽天 / Amazon JP / メルカリ 比价
- 価格.com 自动跟踪 + 降价通知
- freee / MoneyForward 自动整理收据
- 日本招聘网站（リクナビ/マイナビ/Wantedly）自动填充简历
- 日本不动产网站（SUUMO/HOME'S）多站对比
- 日本电商一键复制商品到中国跨境平台

**为什么这条最有差异化**：
- **几乎没有竞争**
- 日本用户付费意愿强
- 你懂日本本地痛点

### 方向 3：开发者工具（Tailscan 模式）

技术含量高，开发者付费意愿强。

**具体产品创意**：
- JSON/YAML/XML 美化 + diff
- API 调试增强（替代 Postman 一部分功能）
- Tailwind/CSS 检查器
- Git 工具增强（GitHub PR diff 优化）
- API key 加密管理
- localStorage / cookie 管理增强

---

## 12 个月行动清单

### 第 0 月：环境

- [ ] 注册 [Chrome Web Store 开发者账号](https://chrome.google.com/webstore/devconsole)（$5 一次性）
- [ ] 学 MV3 基础（[官方文档](https://developer.chrome.com/docs/extensions/develop/migrate/what-is-mv3)）
- [ ] 选 ExtensionPay 作为支付（[extensionpay.com](https://extensionpay.com)，10% 抽成，省去自建支付系统）
- [ ] 写 Hello World 扩展并发布到测试 channel

### 第 1 月：第一个扩展

#### 推荐起步项目：Claude 提示词管理器

**理由**：
- 你每天用 Claude，痛点最清楚
- 受众明确（用 Claude 的人）
- Easy Folders（ChatGPT 版）已证明这条路通

**功能 v1**：
- 提示词文件夹分类
- 一键插入到 Claude 输入框
- 模板变量替换（如 `{{topic}}`）
- 导入/导出 JSON

**技术栈**：
- Manifest V3 + TypeScript
- React（弹窗界面）
- Cursor Max 写代码

**预期时间**：1-2 周完成 v1

#### 上线流程

- [ ] 准备 Chrome Store 资源：
  - 图标（128x128）
  - 截图（1280x800，至少 3 张）
  - 宣传图（440x280）
  - 简介（130 字）+ 详细描述（多段）
- [ ] 提交审核（通常 1-3 天）
- [ ] 发布后立刻在 Reddit r/ClaudeAI / r/chrome_extensions 发帖
- [ ] 上 Product Hunt（选周二/三发布，避开周末）
- [ ] 加 Twitter 标签（即使你不发推，也能被搜到）

### 第 2-3 月：验证 + 迭代

- [ ] 目标：**100 装机量 + 5-10 个付费**
- [ ] freemium 设计：
  - 免费：3 个文件夹、20 个提示词
  - Pro $5/月：无限文件夹、云同步、共享
- [ ] 看 Chrome Store 后台数据：
  - 装机量、卸载率
  - 哪个国家用户多
  - 关键词搜索量

### 第 4-6 月：增长

- [ ] **优化转化率**：免费 → Pro
- [ ] **加新功能**：基于用户反馈
- [ ] **扩到 Edge / Firefox 商店**（同一份代码改 manifest 即可）
- [ ] **目标**：MRR $500-$1K

### 第 7-9 月：第二个扩展

- [ ] 选第二个方向（建议日本本地服务，与第一个互补）
- [ ] 复用支付/auth/UI 组件
- [ ] 第一个扩展给第二个引流（footer 链接）
- [ ] **目标**：MRR $1K-$3K

### 第 10-12 月：矩阵

- [ ] 3-5 个扩展组合
- [ ] 共享 ExtensionPay 账号系统
- [ ] **目标**：MRR $3K-$5K

---

## 关键技术细节

### MV3 vs MV2

- MV3 是当前唯一支持的版本
- 主要变化：service worker 替代 background page、限制远程代码执行
- 老扩展迁移成本不低，**很多放弃 = 你的机会**

### 支付方案对比

| 方案 | 抽成 | 难度 | 推荐度 |
|------|-----|------|------|
| **ExtensionPay** | 10% | 低（30 分钟集成） | ⭐⭐⭐ 起步首选 |
| Stripe 自建 | 2.9% + $0.30 | 中（2-3 天） | 营收 $5K+ 后切换 |
| Paddle | 5% + $0.50 | 中 | 国际市场友好（含 VAT） |

### Chrome Store 审核避坑

- **权限最小化**：只申请必要的 permissions
- **隐私政策必须**：写一份 Privacy Policy 链接
- **描述明确**：避免"AI"等触发审核的词（除非真的用了）
- **首次提交可能被拒 1-2 次**：耐心修改

---

## 成功扩展的 5 个共同特征

1. **寄生在大平台**：ChatGPT、LinkedIn、Gmail、YouTube、Twitter
2. **解决具体高频痛点**：每天用，每天痛
3. **免费版让人离不开**：核心功能免费
4. **付费版解锁组织/批量/同步**：进阶用户的痒点
5. **5 星好评**：4.5+ 评分是关键阈值

---

## 真实数据基准

### 装机量 → MRR 的转化率

- **保守**：1000 装机 = $50-$100 MRR（低 niche）
- **典型**：1000 装机 = $200-$500 MRR（AI 工具类）
- **高质量**：1000 装机 = $1000+ MRR（开发者工具、企业用）

### 留存

- 24 小时留存：< 50%（很多用户装了不用）
- 7 天留存：20-30%（这部分是你的目标用户）
- 30 天留存：10-15%

### 付费转化率

- freemium → 付费：1-5%（典型）、8-15%（优秀）
- 免费试用 → 付费：30-50%（如果产品强）

---

## AI 加速的具体场景

### 场景 1：写 Manifest + 基础结构（半天 → 1 小时）

Cursor Max 直接生成 Manifest V3 + content script + background worker 骨架

### 场景 2：写 UI（2-3 天 → 1 天）

Claude 设计 React 组件 + Tailwind 样式

### 场景 3：写商店描述（半天 → 30 分钟）

Claude 写英文 + 日文 + 中文三个版本，你校对

### 场景 4：客服回复（每天 30 分钟 → 5 分钟）

用户问题用 Claude 起草回复，你审核

---

## 立即可做的 3 件事

1. **本周末**：
   - 注册 Chrome Store 开发者账号（$5）
   - 装 ExtensionPay
   - 写 Hello World 扩展

2. **下周**：
   - 用 Cursor Max 写"Claude 提示词管理器" v1
   - 准备商店资源（图标、截图、文案）

3. **下下周**：
   - 提交审核
   - 上 Reddit r/ClaudeAI + Product Hunt

---

## 核心数据来源

- [extensionpay.com - Browser Extensions Revenue](https://extensionpay.com/articles/browser-extensions-make-money)
- [Easy Folders MRR Update](https://www.indiehackers.com/product/easy-folders/6-months-post-launch-my-chrome-extension-has-hit-3-700-in-mrr-and-42-000-in-total-revenue--O3qs28VAnAkcJw0j--M)
- [Starter Story - Chrome Extension Profitability](https://www.starterstory.com/ideas/chrome-extension/profitability)
- [Indie Hackers - MV3 Migration Opportunity](https://www.indiehackers.com/post/software-opportunity-thousands-of-chrome-extensions-are-about-to-disappear-85DQAl9yaLglihq0kkkP)
- [Chrome MV3 Migration](https://developer.chrome.com/docs/extensions/develop/migrate/what-is-mv3)
- [ExtensionPay](https://extensionpay.com)
