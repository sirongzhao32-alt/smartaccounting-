# 09_Data_Mapping：数据映射说明

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 数据映射目标

定义从 Email、附件、file.ai / Blue Sheets、Xero、月结清单、催票记录到 Agent 内部状态表的数据字段，解决多系统数据分散、客户名称不一致、状态无法回流和证据不可追溯的问题。

## 2. 核心实体关系

```text
Client
  ├── EmailThread
  │   └── EmailMessage
  │       └── Attachment
  │           └── Document
  │               ├── OCRResult
  │               ├── ReviewTask
  │               └── XeroDraft
  ├── MissingDocument
  │   ├── SearchResult
  │   └── ChaseEmail
  └── KPIEvent
```

## 3. Client Mapping

| Field | Type | Source | Required | 说明 |
|---|---|---|---|---|
| client_id | string | Agent DB | Yes | PoC 临时唯一 ID |
| legal_name | string | Excel / Xero / PORTAL | Yes | 法定公司名 |
| trading_name | string | Excel / Email | No | 业务名 / 常用名 |
| uen | string | PORTAL / Excel | Preferred | 新加坡公司 UEN |
| email_domains | array | Email / manual | Yes | 客户邮箱域名 |
| primary_contact_email | string | Excel / Email | Preferred | 主要联系人 |
| xero_contact_id | string | Xero | Preferred | Xero 联系人 ID |
| xpm_client_id | string | XPM | Optional | 项目管理系统 ID |
| portal_client_id | string | PORTAL | Optional | 外部系统 ID |
| status | enum | Agent DB | Yes | active / inactive / unknown |
| mapping_confidence | number | Agent | Yes | 客户匹配置信度 |

## 4. Email Mapping

| Field | Type | Source | Required |
|---|---|---|---|
| email_id | string | Agent DB | Yes |
| message_id | string | Email API | Yes |
| thread_id | string | Email API | Yes |
| mailbox_id | string | Email API | Yes |
| client_id | string | Agent mapping | Preferred |
| sender_email | string | Email API | Yes |
| subject | string | Email API | Yes |
| body_text | text | Email API | Preferred |
| received_at | datetime | Email API | Yes |
| direction | enum | Email API | Yes |
| email_intent | enum | Agent | No |
| processing_status | enum | Agent | Yes |

email_intent：document_submission、client_reply、payment_confirmation、chase_response、service_inquiry、termination_notice、out_of_scope、unknown。

## 5. Attachment Mapping

| Field | Type | Source | Required |
|---|---|---|---|
| attachment_id | string | Email API / Agent | Yes |
| email_id | string | Agent DB | Yes |
| filename | string | Email API | Yes |
| file_extension | string | Agent | Yes |
| mime_type | string | Email API | Yes |
| size_bytes | integer | Email API | Yes |
| hash | string | Agent | Yes |
| storage_uri | string | Agent Storage | Preferred |
| password_protected | boolean | Agent | Preferred |
| duplicate_candidate | boolean | Agent | Preferred |

## 6. Document Mapping

| Field | Type | Source | Required |
|---|---|---|---|
| document_id | string | Agent DB | Yes |
| attachment_id | string | Agent DB | Yes |
| client_id | string | Agent mapping | Yes |
| document_type | enum | Agent / human | Yes |
| period | string | Agent / human | Preferred |
| vendor_name | string | OCR / human | Preferred |
| invoice_number | string | OCR / human | Conditional |
| invoice_date | date | OCR / human | Conditional |
| currency | string | OCR / human | Preferred |
| total_amount | number | OCR / human | Conditional |
| gst_rate | string | OCR / human | No |
| account_code | string | Xero / human | No |
| confidence_score | number | Agent | Yes |
| review_status | enum | Agent / human | Yes |
| xero_status | enum | XeroAgent | Yes |
| source_evidence | array | Agent | Yes |

document_type：supplier_invoice、sales_invoice、bank_statement、expense_claim、supporting_document、contract、unknown、irrelevant。  
review_status：not_required、pending_staff_review、pending_senior_review、confirmed、rejected、exception。  
xero_status：not_ready、ready_to_draft、drafting、drafted、write_failed、not_applicable。

## 7. Xero Mapping

| Agent Field | Xero Field | 说明 |
|---|---|---|
| client_id / xero_contact_id | Contact.ContactID | 联系人 |
| invoice_number | InvoiceNumber | 发票编号 |
| invoice_date | Date | 发票日期 |
| due_date | DueDate | 到期日 |
| currency | CurrencyCode | 币种 |
| line_items.description | LineItems.Description | 描述 |
| account_code | LineItems.AccountCode | 科目编码 |
| total_amount / unit_amount | LineItems.UnitAmount | 金额 |
| gst_rate / tax_type | LineItems.TaxType | 税种 |
| source_attachment | Attachment | 附件证据 |
| status | Status = DRAFT | PoC 默认 Draft |

## 8. Missing Document Mapping

| Field | Type | Source | Required |
|---|---|---|---|
| missing_doc_id | string | Agent DB | Yes |
| client_id | string | Agent DB | Yes |
| period | string | Month-end checklist | Yes |
| required_doc_type | enum | Month-end checklist | Yes |
| expected_count | integer | Rule / checklist | Preferred |
| received_count | integer | Agent DB | Yes |
| confirmed_count | integer | Agent DB | Yes |
| missing_reason | enum | Agent | Yes |
| blocker_level | enum | Agent / human | Yes |
| status | enum | Agent / human | Yes |

missing_reason：not_received、received_but_not_confirmed、ocr_failed、xero_failed、unclear_document_type、client_match_uncertain、not_applicable。  
status：open、searching_history、found_in_email、waiting_client、received、confirmed、not_applicable、escalated、closed。

## 9. KPI Event Mapping

| Event | Trigger | Key Fields |
|---|---|---|
| email_captured | EmailAgent reads email | client_id, message_id, timestamp |
| attachment_classified | DocumentAgent classifies file | doc_type, confidence |
| ocr_completed | OCR result returned | duration, confidence |
| review_completed | Human confirms document | reviewer, duration, changes_count |
| xero_draft_created | Xero draft created | xero_id, success |
| missing_doc_detected | Gap found | missing_doc_id, period |
| search_completed | Historical search done | result_type, candidate_count |
| chase_sent | Email sent | chase_level, recipient |
| client_replied | Reply captured | response_type, duration |
