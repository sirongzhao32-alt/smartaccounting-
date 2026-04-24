# 04_User_Journey_and_Task_Flow：用户旅程与任务流

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. Persona

| Persona | 目标 | 痛点 |
|---|---|---|
| Junior Accountant / Staff | 快速处理客户凭证，减少重复下载上传 | 规则记不住、文件混乱、低级错误被打回 |
| Senior Accountant / Manager | 看到风险、异常、低置信项和月结阻塞 | 逐张 review、翻邮件找证据、客户响应慢 |
| CST / SDT Coordinator | 了解客户是否提交材料，是否需要 follow-up | 状态分散在邮件、Excel、PORTAL、XPM |

## 2. Journey A：M8 邮件凭证自动处理

### As-Is

| 步骤 | 用户动作 | 痛点 |
|---|---|---|
| 1 | 打开邮箱查客户邮件 | 邮件太多 |
| 2 | 判断邮件是否包含凭证 | subject / filename 不规范 |
| 3 | 下载附件 | 多附件、ZIP、重复文件容易漏 |
| 4 | 手动分类 | invoice / statement 混在一起 |
| 5 | 上传 Blue Sheets | Drag & Drop，等待处理 |
| 6 | 核对 OCR | 字段缺失、金额错、GST 不确定 |
| 7 | 进入 Xero | 手动或半自动完成 |
| 8 | 后续月结才发现缺资料 | 缺失发现晚 |

### To-Be

| 步骤 | 用户动作 | AI / 系统动作 | 设计机会 |
|---|---|---|---|
| 1 | Staff 打开 Intake Queue | AI 已读取客户邮件和附件 | 默认按风险和 deadline 排序 |
| 2 | 查看自动分类结果 | AI 标记 invoice / bank statement / other | 支持一键修正分类 |
| 3 | 进入 Document Review | AI 已上传 Blue Sheets 并回收 OCR | 原件 + 字段左右对照 |
| 4 | 修改低置信字段 | AI 高亮可疑字段 | 只让人看异常 |
| 5 | 提交 Xero Draft | 系统写入 Draft 并保留日志 | 不直接 approve |
| 6 | Dashboard 更新 | 凭证状态变为 Confirmed / Drafted | 月结覆盖率实时变化 |

### Detailed Task Flow

```text
New customer email arrives
  → EmailAgent monitors inbox
  → Capture message_id, thread_id, sender, subject, timestamp
  → Extract attachments
  → Match client
  → Classify attachments
  → Upload to file.ai / Blue Sheets
  → Receive OCR result
  → Human review based on confidence
  → Create Xero Draft
  → Update document status
```

## 3. Journey B：M9 缺票检测与历史邮件检索

### As-Is

| 步骤 | 用户动作 | 痛点 |
|---|---|---|
| 1 | 月结时检查客户资料 | 才发现凭证不齐 |
| 2 | 翻找历史邮件 | 搜索关键词不统一 |
| 3 | 判断附件是否可用 | 需要打开多个邮件和附件 |
| 4 | 没找到就写催票邮件 | 手动列出缺失项目 |
| 5 | 客户回复慢或发错邮箱 | 状态无法自动回流 |

### To-Be

```text
Month-end checklist detects missing document
  → SearchAgent builds query by client / period / vendor / doc type
  → Historical email search
  → Found: send attachment to M8 OCR
  → Possible: Staff review
  → Not found: ChaseAgent creates email draft
  → Follow-up tracking
  → Client replies with attachment
  → Missing document status resolved
```

## 4. Screen Flow

```text
Dashboard
  ├─ Client Workspace
  │   ├─ Email Intake Queue
  │   │   └─ Document Classification
  │   │       └─ Document Review
  │   │           └─ Xero Draft Result
  │   ├─ Missing Document Tracker
  │   │   ├─ Historical Email Search Results
  │   │   │   ├─ Send found attachment to OCR
  │   │   │   └─ Chase Email Composer
  │   └─ Audit Trail
  └─ Exception Queue
```

## 5. 关键决策点

| 决策点 | 触发条件 | 用户需要看到的信息 | 可执行动作 |
|---|---|---|---|
| 客户匹配不确定 | AI client confidence 低 | 候选客户、匹配理由、邮箱来源 | 选择客户 / 新建 mapping |
| 附件类型不确定 | 文件名模糊或 OCR 类型不明 | 文件预览、AI 猜测、confidence | 改类型 / 送 OCR / 标记 other |
| OCR 字段低置信 | amount/date/vendor/GST 低置信 | 原文位置、字段值、置信度 | 修改 / 确认 / 升级 |
| Xero 写入前 | 凭证 ready to submit | payload、source、risk warning | Create Draft / Save |
| 缺票是否催 | SearchAgent 未找到历史附件 | 缺失清单、搜索证据、联系人 | 生成草稿 / 标记不适用 |
