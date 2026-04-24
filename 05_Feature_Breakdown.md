# 05_Feature_Breakdown：功能拆解

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 功能模块总览

| 模块 | 功能 | 优先级 |
|---|---|---|
| F1 Dashboard | 月结总览、风险状态、KPI 摘要 | P0 |
| F2 Email Intake | 邮件读取、附件捕获、客户匹配 | P0 |
| F3 Document Classification | 附件类型识别、异常文件识别 | P0 |
| F4 OCR Review | file.ai / Blue Sheets 调用、OCR 字段确认 | P0 |
| F5 Xero Draft | Xero Draft 写入、写入日志、失败重试 | P0 |
| F6 Missing Tracker | 缺票清单、凭证覆盖率、阻塞原因 | P0 |
| F7 Historical Search | 历史邮件检索、候选附件、匹配理由 | P0 |
| F8 Chase Email | 催票草稿、模板、发送、响应追踪 | P0 |
| F9 Exception Queue | 低置信、API 失败、密码文件、客户不确定 | P0 |
| F10 Audit Trail | 来源证据、人工修改、系统写入、发送记录 | P0 |
| F11 Rule & Config | 阈值、自动发送开关、客户白名单、模板配置 | P1 |
| F12 Vendor Rule Assistant | Vendor Master List、科目/GST 推荐 | P2 |

## 2. F1 Dashboard

| 功能 | 说明 |
|---|---|
| Customer status table | 客户、period、deadline、coverage、risk status |
| KPI cards | 月结周期、凭证覆盖率、催票响应、待审核数 |
| Risk filter | Missing Docs / Pending Review / API Failed / Overdue |
| Drill-down | 点击客户进入 Client Workspace |
| Workload view | 按 Staff 显示待处理任务量 |

## 3. F2 Email Intake

| 功能 | 说明 |
|---|---|
| Email sync | 读取指定邮箱、日期范围、试点客户邮件 |
| Attachment capture | 捕获附件、大小、文件类型、hash |
| Thread tracking | 记录 message_id / thread_id，追踪回复 |
| Client match | 根据邮箱域名、客户别名、UEN、Xero contact 匹配客户 |
| Manual override | 客户匹配错误时支持人工修正 |
| Duplicate detection | hash + invoice no + amount 防重复处理 |

## 4. F3 Document Classification

| 文档类型 | 识别依据 | 后续动作 |
|---|---|---|
| Supplier Invoice | invoice no、vendor、amount、GST、supplier keywords | 送 OCR + Xero bill draft |
| Sales Invoice | customer invoice、sales amount、invoice date | 送 OCR + Xero invoice draft |
| Bank Statement | bank name、account no、statement period、transaction rows | Bank Statement pipeline / completeness check |
| Expense Claim | employee name、claim items、receipt | OCR / expense review |
| Contract / Other | tenancy agreement、supporting document | P2，先标记 supporting doc |
| Unknown | 无法判断 | Exception Queue |
| Password Protected | 加密 PDF | Exception Queue + request password |

## 5. F4 OCR Review

| 区域 | 内容 |
|---|---|
| 文件预览区 | PDF / image preview，支持 zoom、page navigation |
| 字段区 | vendor、invoice no、date、due date、amount、currency、GST、line items |
| 置信度区 | overall confidence + field confidence |
| 警告区 | missing amount、date mismatch、duplicate invoice、GST uncertain |
| 操作区 | Confirm、Edit、Send to Senior Review、Mark as Exception |

## 6. F5 Xero Draft

| 功能 | 说明 |
|---|---|
| Payload preview | 写入前展示 Xero payload |
| Create Draft | 默认只创建 Draft，不 approve |
| Attach source | 保存 source email / attachment reference |
| Write log | 保存 API response、error、timestamp |
| Retry | 网络 / 临时失败可重试 |
| Mapping review | 科目或 contact 不匹配时进入人工 mapping |

## 7. F6 Missing Document Tracker

| 字段 | 描述 |
|---|---|
| client_id | 客户唯一标识，PoC 可用临时 mapping |
| period | 月份 / 季度 / 年度 |
| required_doc_type | 应收文档类型 |
| received_count | 已收到数量 |
| confirmed_count | 已确认数量 |
| missing_count | 缺失数量 |
| missing_reason | not received / OCR failed / pending review / not applicable |
| blocker_level | high / medium / low |
| next_action | search history / chase client / manual review |

## 8. F7 Historical Search

| 搜索维度 | 示例 |
|---|---|
| Client | legal name, trading name, alias, UEN |
| Email | sender, recipient, domain, thread |
| Period | Jun 2026, 2026-06, Q2 |
| Vendor | Singtel, DBS, OCBC |
| Doc type | invoice, statement, receipt, bank |
| Amount / invoice no | exact / fuzzy search |

## 9. F8 Chase Email

| 功能 | 说明 |
|---|---|
| Template selection | L1 friendly reminder / L2 follow-up / L3 escalation |
| Missing list insertion | 自动插入缺失凭证列表 |
| Context summary | 加入“we could not locate the following documents...” |
| Tone control | 礼貌、明确、非法律威胁 |
| Human review | PoC 默认人工审核后发送 |
| Reply tracking | 识别客户回复、附件补交、bounce |

## 10. 路线图

| 版本 | 功能 |
|---|---|
| V0 / Clickable Prototype | Dashboard、Intake Queue、Review Page、Missing Tracker、Search Results、Chase Composer |
| V1 / PoC | 邮件读取、附件分类、OCR 回收、人工确认、Xero Draft/mock、缺票检索、催票草稿 |
| V2 / Pilot | 自动回复追踪、异常队列、KPI dashboard、配置中心、部分自动发送 |
| V3 / Scale | Vendor Rule Assistant、跨客户知识库、Bank Reco 预警、AR Collection 扩展 |
