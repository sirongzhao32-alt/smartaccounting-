# 06_Wireframe_Design_Spec：线框图与设计说明

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 设计定位

界面应是 **operations dashboard + workflow review system**，不是聊天窗口。核心体验是让用户快速判断哪些客户月结被阻塞、哪些文件已收到 / 已 OCR / 已确认 / 已进 Xero、哪些凭证缺失、AI 找到了哪些历史邮件证据、哪些催票邮件需要人工审核。

## 2. 信息架构

```text
Global Navigation
├── Dashboard
├── Intake Queue
├── Missing Documents
├── Search & Chase
├── Review Tasks
├── Exceptions
├── KPI & Reports
└── Settings
```

## 3. 页面 1：Dashboard / 月结总览

```text
[Top Bar]
Product name | Period selector | Sync status | User role

[KPI Cards]
Month-end cycle | Credential coverage | Pending review | Missing docs | Chase response

[Risk Tabs]
All | On Track | Missing Docs | Pending Review | Xero Failed | Overdue

[Customer Status Table]
Client | Period | Deadline | Coverage | Missing | Pending Review | Last Email | Risk | Next Action

[Right Side Panel]
Today's Priority
- 5 high-risk missing docs
- 3 Xero write failures
- 8 OCR review tasks
```

## 4. 页面 2：Client Workspace / 客户工作台

```text
[Client Header]
Client name | UEN | Xero contact | Period | Owner | Risk status

[Tabs]
Overview | Documents | Emails | Missing Docs | Chase History | Audit Trail

[Overview]
- Document coverage by type
- Latest incoming emails
- Pending review tasks
- Missing documents
- Recent chase activity
```

设计重点：客户名称旁显示 mapping confidence；显示 aliases / email domains；所有凭证都能回到 source email。

## 5. 页面 3：Email Intake Queue

```text
[Filters]
Date | Client | Document type | Confidence | Status | Has exception

[Email Group Card]
Sender | Subject | Received time | Matched client | Thread ID
Attachments:
  - file1.pdf | predicted invoice | confidence | status
  - file2.pdf | bank statement | confidence | status
Actions: Review classification | Send to OCR | Mark irrelevant
```

## 6. 页面 4：Document Classification

```text
[Left] File preview

[Right]
Predicted client: ABC Pte Ltd [confidence 82%]
Predicted document type: Supplier Invoice [confidence 91%]
Period: June 2026 [confidence 75%]
Vendor: Singtel [confidence 68%]

Actions:
- Confirm and send to OCR
- Change client
- Change document type
- Mark as duplicate
- Mark as non-accounting document
```

## 7. 页面 5：Document Review / OCR 确认页

```text
[Header]
Client | Document type | Source email | OCR confidence | Review status

[Left: Document Preview]
PDF / Image preview
Page thumbnails
Highlight extracted region

[Right: Extracted Fields]
Vendor
Invoice No.
Invoice Date
Due Date
Amount
Currency
GST
Account Code
Line Items

[Bottom: Actions]
Save changes | Send to Senior Review | Create Xero Draft | Mark exception
```

字段状态：

| 状态 | UI 表现 | 操作 |
|---|---|---|
| High confidence | 普通字段 | 可确认 |
| Medium confidence | 轻提示 | 建议检查 |
| Low confidence | 强提示 | 必须人工确认 |
| Missing | 空值警告 | 必填后才能提交 |
| Conflict | 红色冲突 | 需解决后提交 |

## 8. 页面 6：Missing Document Tracker

```text
[Summary]
Required docs | Received | Confirmed | Missing | Blocking close

[Missing Document Table]
Client | Period | Doc Type | Vendor / Account | Expected | Evidence | Days open | Next action

[Action Buttons]
Search history | Generate chase email | Mark not applicable | Assign owner
```

## 9. 页面 7：Historical Email Search Results

```text
[Search Query Summary]
Client: ABC Pte Ltd
Missing: June 2026 Bank Statement
Search terms: ABC, bank statement, Jun, June, DBS, OCBC

[Result Cards]
Match score | Sender | Date | Subject | Snippet | Attachments | Why matched
Actions: Open email | Send attachment to OCR | Mark not relevant

[No result state]
No matching attachment found.
Suggested next action: Generate chase email.
```

## 10. 页面 8：Chase Email Composer

```text
[Left]
Missing list
Client contact
Previous chase history
Source evidence

[Right]
Email template selector: L1 / L2 / L3
Recipient
Subject
Body editor

[Actions]
Save draft | Send for review | Send now | Cancel
```

## 11. 交互原则

1. 证据在旁边：用户做判断时，同时看到原邮件、原附件和 AI 理由。  
2. 默认安全：低置信不能自动写入 Xero，催票默认草稿。  
3. 少弹窗：复杂任务用 side panel / detail page。  
4. 批量但可控：允许批量处理高置信项，但异常项必须排除。  
5. 状态可恢复：失败任务不能消失，必须可重试和可追踪。
