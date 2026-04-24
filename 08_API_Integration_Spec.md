# 08_API_Integration_Spec：API 集成说明

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 集成目标

定义 PoC 阶段需要对接的系统、数据流、API 能力、权限、失败处理与待验证事项。

## 2. 系统清单

| 系统 | 用途 | PoC 优先级 | 当前状态 |
|---|---|---|---|
| Email / Outlook / Gmail / PORTAL Email | 读取客户邮件、附件、回复；发送催票邮件 | P0 | 待确认具体系统与 API |
| file.ai / Blue Sheets / Push AI | OCR、发票数据提取、Rule 匹配 | P0 | API 可用性需确认 |
| Xero | 核心记账系统，创建 Draft | P0 | API 写入权限需确认 |
| Agent Internal DB | 保存状态、任务、日志、KPI | P0 | 新建 |
| XPM | 项目状态、workflow 信息 | P1 | PoC 可先不接或只读 |
| PORTAL | 客户主数据、AR / Invoice 状态 | P1 | 权限受限，待确认 |
| Excel Master List | 客户状态、手动维护主表 | P1 | PoC 可导入静态表 |
| SharePoint / OneDrive | 少数客户文件上传通道 | P2 | 后续扩展 |

## 3. 高层数据流

```text
Email API
  → EmailAgent
  → Attachment Store / Agent DB
  → file.ai / Blue Sheets API
  → OCR Result Normalizer
  → Review UI
  → XeroAgent
  → Xero Draft
  → Agent DB status update
  → Dashboard / KPI

Missing Document Trigger
  → SearchAgent
  → Email API historical search
  → Found attachment → OCR flow
  → Not found → ChaseAgent
  → Email sending API
  → Reply tracking
  → Status update
```

## 4. Email API Required Capabilities

| 能力 | 必需 | 说明 |
|---|---|---|
| List messages | Yes | 按日期、sender、folder、label 查询 |
| Read message body | Yes | 判断上下文和客户回复 |
| Read attachments | Yes | M8 核心 |
| Search historical messages | Yes | M9 核心 |
| Track thread / message ID | Yes | 回复追踪和证据链 |
| Send email | Preferred | 催票邮件发送；PoC 可先草稿 |
| Create draft | Preferred | 默认安全策略 |
| BCC generic mailbox | Preferred | 监控和备份 |

## 5. file.ai / Blue Sheets API Required Capabilities

| 能力 | 必需 | 说明 |
|---|---|---|
| Upload document | Yes | 上传附件进入 OCR |
| Get job status | Yes | processing / completed / failed |
| Get extracted fields | Yes | invoice / statement 字段 |
| Get confidence | Preferred | 字段级置信度 |
| Export to Xero | Optional | 若由 Blue Sheets 直接写 Xero，需确认 |
| Webhook callback | Preferred | OCR 完成后回调 |

## 6. Xero API Required Capabilities

| 能力 | 必需 | 说明 |
|---|---|---|
| Read contacts | Yes | 匹配客户 / vendor |
| Read chart of accounts | Yes | 科目映射 |
| Create draft bill / invoice | Yes | PoC 核心 |
| Attach source document | Preferred | 审计证据 |
| Read draft status | Preferred | 状态回流 |
| Update draft | Optional | 人工修改后回写 |

## 7. Agent Internal DB Tables

| Table | 用途 |
|---|---|
| clients | 客户主数据与临时 mapping |
| emails | 邮件记录 |
| attachments | 附件记录 |
| documents | 凭证处理状态 |
| ocr_results | OCR 输出和置信度 |
| review_tasks | 人工审核任务 |
| xero_writes | Xero 写入日志 |
| missing_documents | 缺票记录 |
| searches | 历史邮件检索记录 |
| chase_emails | 催票邮件记录 |
| audit_logs | 审计日志 |
| kpi_events | KPI 事件流 |

## 8. Idempotency Keys

| 操作 | 幂等键 |
|---|---|
| 邮件读取 | mailbox_id + message_id |
| 附件捕获 | message_id + attachment_id + hash |
| OCR 上传 | attachment_hash + document_type + client_id |
| Xero 写入 | client_id + invoice_number + date + amount |
| 催票发送 | client_id + missing_doc_id + chase_level + date |

## 9. API Error Handling

| 错误 | 处理 |
|---|---|
| 401 / 403 权限错误 | 停止自动重试，通知 admin |
| 429 rate limit | 指数退避重试 |
| 5xx server error | 重试 3 次，失败进入 Exception |
| OCR timeout | 标记 processing timeout，允许重试 |
| Xero validation error | 显示字段错误，创建 mapping review |
| Email send bounced | 更新 chase status，提示联系人可能失效 |

## 10. 待确认 API 问题

1. 邮箱是 Outlook 365、Gmail、PORTAL 内置 Email，还是混合？  
2. 是否允许读取 Staff 个人邮箱，还是只能读取 shared mailbox / generic mailbox？  
3. file.ai / Blue Sheets 是否提供 Upload Endpoint、Result API、Webhook？  
4. Blue Sheets 是否可直接 export 到 Xero，还是必须由自研 Agent 调 Xero？  
5. Xero 测试环境是否可用？Draft 写入权限申请周期多久？  
6. 是否允许保存客户附件副本？保存多久？  
7. 催票邮件发送是用个人邮箱、generic email，还是系统邮箱？
