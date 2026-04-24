# 03_Service_Blueprint：服务蓝图

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 服务蓝图目标

说明智能会计交付助手如何把客户、CST / SDT、会计 Staff、Senior / Manager、AI Agent、Email、file.ai / Blue Sheets、Xero、Excel / 月结清单串成一个可执行服务链路。

## 2. 关键服务场景

| 场景 | 描述 | 业务价值 |
|---|---|---|
| S1 邮件凭证自动处理 | 客户发邮件后，AI 自动捕获附件并送入 OCR | 减少人工下载、分类、上传 |
| S2 OCR 人工确认与 Xero Draft | OCR 返回后，Staff 快速确认并写入 Xero Draft | 保留人工控制，降低录入工作量 |
| S3 缺票识别 | 月结清单与实收凭证对比，发现缺失 | 提前暴露阻塞项 |
| S4 历史邮件检索 | 缺票时 AI 自动翻历史邮件找附件 | 减少人工翻邮件 |
| S5 催票邮件 | 找不到附件时，生成催票草稿并追踪回复 | 提高 follow-up 及时性 |

## 3. 服务蓝图总览

| 阶段 | 客户行为 | 前台员工行为 | 后台 AI 行为 | 系统 / 工具 | 输出证据 |
|---|---|---|---|---|---|
| 1 文件提交 | 客户发送邮件和附件 | 无需手动查找，系统提醒新任务 | EmailAgent 读取邮件、附件、metadata | Email API | email_thread_id、attachment_id |
| 2 文件分类 | 无 | Staff 查看自动分类结果，必要时修正 | 判断 document_type、client、period、vendor | Agent DB | 附件分类状态 |
| 3 OCR 处理 | 无 | Staff 等待任务进入 review queue | 上传 file.ai / Blue Sheets，获取 OCR fields | file.ai / Blue Sheets | OCR JSON、confidence |
| 4 人工确认 | 无 | Staff 对照原件确认字段 | 标记低置信字段、异常字段 | Review UI | confirmation log |
| 5 Xero 写入 | 无 | Staff / Senior 提交 Draft | 调用 Xero API 写入 Draft | Xero | xero_draft_id、write log |
| 6 月结检查 | 客户等待服务进展 | Staff 查看客户月结进度 | 对比 required_docs 和 confirmed_docs | Month-end checklist | missing_doc_flags |
| 7 历史检索 | 无 | Staff 查看候选邮件 | SearchAgent 检索历史邮件和附件 | Email API | candidate emails |
| 8 催票 | 客户收到缺票请求 | Staff 审核草稿并发送 | ChaseAgent 生成邮件，追踪回复 | Email API | chase_email_id、status |
| 9 状态回流 | 客户补发文件 | Staff 查看状态更新 | 新邮件自动进入 intake | Agent DB | coverage update |

## 4. M8 泳道图

```text
Customer sends email
  → Email API exposes message + attachments
  → EmailAgent captures source data
  → Client matching by domain / mapping / name / UEN
  → Intake Queue groups documents by client and period
  → file.ai / Blue Sheets OCR
  → Document Review UI
  → Staff confirms fields
  → XeroAgent creates Draft
  → Dashboard updates document coverage
```

## 5. M9 泳道图

```text
Month-end Checklist detects missing document
  → Missing Document Tracker flags gap
  → SearchAgent searches historical email
  ├─ Found attachment → send to M8 OCR flow
  ├─ Possible match → Staff review
  └─ Not found → ChaseAgent creates email draft
  → Staff reviews and sends
  → Customer replies with attachment
  → EmailAgent captures reply
  → Missing status updates to received / confirmed
```

## 6. 服务恢复机制

| 失败点 | 用户看到什么 | 系统做什么 |
|---|---|---|
| 邮件 API 读取失败 | “邮件同步失败，最近同步时间...” | 自动重试，通知 admin，允许手动上传 |
| 附件密码保护 | “文件受密码保护，需人工处理” | 创建 exception task |
| OCR 失败 | “OCR 未返回可用结果” | 允许重新上传、手动录入或请求客户补件 |
| 客户匹配不确定 | “可能属于以下客户...” | Staff 选择客户后写入 learning log |
| Xero 写入失败 | “Xero Draft 创建失败：字段/权限/网络原因” | 保留 payload，支持重试 |
| 催票邮件退回 | “Email bounced” | Flag 给 Staff，提示更新联系人 |

## 7. 服务指标

| 节点 | 可测指标 |
|---|---|
| Email Intake | 邮件捕获量、附件捕获量、附件分类准确率 |
| OCR Review | 平均 review time、低置信字段比例、人工修改率 |
| Xero Draft | 写入成功率、写入失败原因、重试成功率 |
| Missing Tracker | 缺票发现提前天数、缺票关闭时间 |
| Chase Email | 发送量、回复率、补件率、bounce rate |
| End-to-End | 月结周期、准时率、凭证覆盖率 |
