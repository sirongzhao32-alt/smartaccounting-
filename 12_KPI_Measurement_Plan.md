# 12_KPI_Measurement_Plan：KPI 衡量方案

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. KPI 目标

证明智能会计交付助手是否真正降低月结前端处理成本、提高凭证覆盖率、减少缺票滞后、提升催票响应和月结准时率。

## 2. KPI 层级

| 层级 | KPI | 说明 |
|---|---|---|
| Business KPI | 月结周期、准时率、凭证覆盖率、催票响应率 | 体现端到端业务价值 |
| Operational KPI | 人工处理时间、OCR review 时间、Xero 写入成功率 | 体现流程效率 |
| Quality KPI | 低置信率、错误率、人工修改率、异常率 | 体现质量和风险 |
| Adoption KPI | 使用率、任务完成率、人工 override 率 | 体现用户接受度 |

## 3. 核心 KPI

| KPI ID | 名称 | 定义 | PoC 目标 | 数据源 |
|---|---|---|---|---|
| A-01 | 月结周期 | 从月结任务启动到客户该 period 凭证确认完成 / 进入下一步的天数 | ≤10 天，基线待确认 | month_end_task events |
| A-02 | 催票响应率 | 客户在催票后回复或补发文件的数量 / 催票发送数量 | ≥70%，基线待确认 | chase_emails + email replies |
| A-03 | 月结准时完成率 | deadline 前完成的客户数 / 总试点客户数 | ≥80% | dashboard status |
| A-06 | 凭证覆盖率 | 已确认凭证数 / 应收凭证数 | ≥90% | missing_documents + documents |

## 4. Operational Metrics

| 指标 | 计算方式 | 目标 |
|---|---|---|
| Email-to-Intake Time | intake_created_at - email_received_at | 越短越好 |
| Attachment Classification Accuracy | 人工确认正确分类 / 总分类 | ≥85% for PoC |
| OCR Review Time | review_completed_at - review_started_at | 比人工流程下降 30%+ |
| Xero Draft Success Rate | successful_drafts / draft_attempts | ≥90% if API 可用 |
| Missing Detection Lead Time | missing_detected_at 距 deadline 的提前天数 | 越早越好 |
| Search Success Rate | found_exact_or_possible / search_tasks | 记录基线 |
| Chase Closure Time | missing_resolved_at - chase_sent_at | 越短越好 |

## 5. Quality Metrics

| 指标 | 定义 | 用途 |
|---|---|---|
| Low Confidence Rate | low confidence documents / total documents | 判断 OCR / 分类质量 |
| Human Correction Rate | 人工修改字段数 / OCR 字段数 | 判断 AI 输出可靠性 |
| Duplicate Detection Rate | duplicate candidates / total documents | 防重复入账 |
| Exception Rate | exception tasks / total tasks | 衡量异常负担 |
| Xero Validation Error Rate | Xero validation errors / draft attempts | 判断 mapping 质量 |
| Audit Completeness Rate | 有完整 source evidence 的任务 / 总任务 | 会计合规追溯 |

## 6. KPI Event Instrumentation

| Event | Required Properties |
|---|---|
| email_captured | client_id, message_id, received_at, captured_at |
| attachment_classified | attachment_id, predicted_type, final_type, confidence |
| ocr_completed | document_id, provider, duration, confidence, status |
| review_completed | document_id, reviewer_id, duration, fields_changed |
| xero_draft_created | document_id, xero_draft_id, timestamp |
| missing_doc_detected | missing_doc_id, client_id, period, doc_type |
| historical_search_completed | missing_doc_id, result_type, candidate_count |
| chase_email_sent | chase_email_id, recipient, sent_at |
| client_reply_captured | chase_email_id, reply_type, replied_at |
| missing_doc_resolved | missing_doc_id, resolution_type, resolved_at |

## 7. Baseline Collection Plan

| 基线 | 如何收集 | Owner |
|---|---|---|
| 当前月结周期 | 抽样最近 3 个月客户完成时间 | Accounting Manager / FDE |
| 当前人工催票响应率 | 从历史 follow-up 邮件抽样 | CST / SDT |
| 当前凭证覆盖率 | 月结前应收 vs 实收凭证 | Accounting team |
| 当前人工处理时间 | 观察 Staff 处理 10–20 个文件 | FDE |
| 当前错误率 | Xero / Blue Sheets / manual review 返工记录 | Accounting team |

## 8. PoC KPI Report Template

| KPI | Baseline | PoC Result | Target | Status | Notes |
|---|---|---|---|---|---|
| 月结周期 | 待确认 | TBD | ≤10 days | TBD | 需客户提供历史数据 |
| 催票响应率 | 待确认 | TBD | ≥70% | TBD | PoC 可先记录实际值 |
| 凭证覆盖率 | 待确认 | TBD | ≥90% | TBD | 需 month-end checklist |
| 人工 review time | 待观察 | TBD | -30% | TBD | 通过 task timestamp |
| Xero Draft 成功率 | N/A | TBD | ≥90% | TBD | 取决于 API 权限 |
| 系统错误率 | N/A | TBD | <5% | TBD | 阻塞性错误 |
