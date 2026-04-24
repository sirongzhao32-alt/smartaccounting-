# 07_AI_Agent_Workflow：AI Agent 工作流说明

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. Agent 设计原则

AI Agent 不应被设计为独立聊天机器人，而应作为 workflow backend 中的自动化执行与决策辅助层。Agent 处理邮件、附件、检索、状态追踪和催票草稿；会计专业判断仍由 Staff / Senior / Manager 保留。

## 2. Agent 架构

```text
L1 Orchestrator
├── EmailAgent      // M8 邮件凭证捕获
├── DocumentAgent   // 附件分类与 OCR 管理
├── ReviewAgent     // 置信度判断与人工审核任务分发
├── XeroAgent       // Xero Draft 写入与错误处理
├── SearchAgent     // M9 历史邮件检索
├── ChaseAgent      // 催票邮件生成与跟踪
├── KPIAgent        // KPI 计算与状态汇总
└── AuditAgent      // 证据链与日志
```

## 3. Orchestrator

职责：监听 new_email、ocr_completed、review_confirmed、xero_failed、missing_doc_detected、client_replied 等事件；分配任务；维护状态机；控制 human gate；处理失败重试和降级。

```text
New Email
  → Captured
  → Classified
  → OCR Processing
  → Ready for Review
  → Reviewed
  → Xero Drafted
  → Confirmed

Exception branch:
Captured / Classified / OCR / Xero
  → Exception
  → Human Review
  → Retry / Resolve / Close

Missing branch:
Missing Detected
  → Searching History
  → Found / Not Found / Possible Match
  → OCR Flow / Chase Draft / Human Review
```

## 4. EmailAgent

| 输入 | 字段 |
|---|---|
| Email message | message_id、thread_id、sender、to、cc、subject、body、timestamp |
| Attachments | filename、mime_type、size、hash、attachment_id |
| Pilot scope | client list、date range、mailbox list |

输出：email_record、attachment_records、client_match_candidates、intake_task。  
规则：只处理试点客户或白名单；客户匹配低置信进入 Client Match Review；AI 发出的催票邮件保留 message_id / thread_id。

## 5. DocumentAgent

职责：判断附件类型；识别密码、损坏、重复、过大、无效格式；调用 file.ai / Blue Sheets；解析 OCR 返回结果；标准化字段。

```text
supplier_invoice
sales_invoice
bank_statement
expense_claim
supporting_document
contract
unknown
password_protected
corrupted
irrelevant
```

## 6. ReviewAgent

| 条件 | 处理 |
|---|---|
| overall confidence ≥ 90% 且关键字段完整 | Staff quick confirm |
| 70%–90% 或单字段低置信 | Staff required review |
| <70%、金额异常、客户不确定、GST 不确定 | Senior review |
| 涉及催款升级、客户争议、长期欠款 | Manager review |

## 7. XeroAgent

职责：将确认后的 OCR 字段转换为 Xero payload；创建 Draft，不默认 Approve；处理 Xero contact、account code、tax type mapping；记录写入结果和错误。

状态：ready_to_draft、drafting、drafted、write_failed、mapping_required。

## 8. SearchAgent

搜索策略：

```text
1. exact: client_id + period + document_type + invoice_number
2. strong fuzzy: client alias + vendor + period + attachment keywords
3. context: email body mentions sent / attached / statement / invoice
4. fallback: broader date range + sender domain + keywords
```

输出分级：

| 结果 | 含义 | 后续动作 |
|---|---|---|
| found_exact | 高度匹配 | 送入 OCR |
| found_possible | 可能匹配 | Staff review |
| context_only | 邮件提到但无附件 | 用作催票上下文 |
| not_found | 未找到 | 生成催票草稿 |

## 9. ChaseAgent

| 级别 | 触发条件 | 语气 | 是否自动 |
|---|---|---|---|
| L1 | 首次缺票提醒 | 礼貌、清晰 | PoC 默认草稿 |
| L2 | 3–7 天无回复 | 明确 deadline | 人工审核 |
| L3 | 多次无回复或阻塞月结 | 升级给 Manager | 必须人工审核 |

## 10. Feedback Loop

| 人工反馈 | 用途 |
|---|---|
| 更正客户归属 | 改进 client matching |
| 更正文档类型 | 改进 attachment classification |
| 修改 OCR 字段 | 标记 OCR 弱点和高风险字段 |
| 修改科目 / GST | 建立 Vendor Rule 建议库 |
| 催票邮件编辑 | 优化模板语气和缺失清单表达 |
