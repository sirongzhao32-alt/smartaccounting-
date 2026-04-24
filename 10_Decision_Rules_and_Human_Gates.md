# 10_Decision_Rules_and_Human_Gates：决策规则与人工关卡

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 设计目标

定义 AI 自动处理和人工确认之间的边界。原则是：能自动化重复动作，但不能绕过会计判断、异常处理和高风险决策。

## 2. 总体规则

| 原则 | 说明 |
|---|---|
| 默认安全 | PoC 阶段默认创建 Xero Draft，不自动 approve |
| 证据优先 | 没有 source email / attachment 的凭证不能进入确认状态 |
| 低置信必审 | 低置信、缺字段、金额异常、客户匹配不确定必须人工处理 |
| 催票可控 | PoC 默认生成草稿，由人审后发送 |
| 异常不沉默 | API 失败、OCR 失败、邮件 bounce 必须进入 Exception Queue |
| 规则可配置 | 阈值、催票间隔、自动发送开关需可配置 |

## 3. Confidence Thresholds

| 分数 | 等级 | 默认动作 |
|---|---|---|
| ≥ 0.90 | High | Staff Quick Confirm；部分非关键字段可批量确认 |
| 0.70–0.89 | Medium | Staff 必须审核关键字段 |
| < 0.70 | Low | Senior Review 或 Exception |
| N/A | Missing | 不能提交，必须补字段或标记异常 |

## 4. Client Matching Rules

| 条件 | 决策 |
|---|---|
| sender domain 与 client email_domains 完全匹配 | 自动匹配，高置信 |
| subject / body 出现 legal_name 或 UEN | 提升置信度 |
| 同一 thread 历史已绑定 client_id | 继承 client_id，但显示来源 |
| 多个客户共享同一 contact / domain | Client Match Review |
| sender 为个人邮箱或不在白名单 | 低置信，需人工确认 |

## 5. Document Classification Rules

| 条件 | 决策 |
|---|---|
| 文件包含 invoice no、vendor、amount、GST | classify as invoice |
| 文件包含 bank name、account no、statement period、transaction rows | classify as bank_statement |
| 文件包含 claim / reimbursement / receipt | classify as expense_claim |
| 文件加密 | password_protected exception |
| 文件损坏 / 无法打开 | corrupted exception |
| 类型不明确 | unknown → human classification |

## 6. OCR Review Rules

| 场景 | Gate |
|---|---|
| 关键字段完整且高置信 | Staff Quick Confirm |
| total amount 低置信 | Staff Required Review |
| invoice date 不在 period 内 | Senior Review |
| GST rate / tax code 不确定 | Senior Review |
| vendor rule 不存在 | Staff / Senior Review |
| 多页发票疑似拆分 | Staff Review |
| 重复 invoice 疑似 | Staff Review |

## 7. Xero Write Rules

| 条件 | 动作 |
|---|---|
| review_status = confirmed | 可创建 Xero Draft |
| xero_contact_id 缺失 | mapping_required，不能写入 |
| account_code 缺失 | mapping_required，不能写入 |
| tax_type 缺失且涉及 GST | Senior Review |
| amount / currency 缺失 | 不能写入 |
| source_evidence 缺失 | 不能写入 |
| Xero API validation error | 进入 Xero Failed Queue |

## 8. Missing Document Rules

| 文档 | 完整性规则 |
|---|---|
| Supplier Invoice | 按 period、vendor、invoice number / date / expected count 检查 |
| Sales Invoice | 按 sales invoice sequence、period 检查 |
| Bank Statement | 每个 bank account 每月应有 statement |
| Expense Claim | 若客户有固定报销习惯，可按 period 检查 |

## 9. Chase Email Rules

| 条件 | 级别 | 动作 |
|---|---|---|
| 第一次缺票 | L1 | 生成友好提醒草稿 |
| 3–7 天无回复 | L2 | 生成 follow-up 草稿，语气更明确 |
| 7–14 天无回复且阻塞月结 | L3 | Manager review 后发送 |
| 客户回复“已发送”但未找到附件 | L1 clarification | 礼貌请求重新发送 |
| 邮件 bounce | Contact update task | 不继续自动发送 |
| 客户争议 / 投诉 | Manager review | 不自动回复 |

## 10. 禁止自动化清单

| 禁止项 | 原因 |
|---|---|
| 自动 approve Xero entries | 会计风险高 |
| 自动发送法律 / 威胁性催款函 | 合规风险 |
| 自动判断客户终止服务 / 清盘结论 | 需要人工确认 |
| 自动修改客户主数据 | 需人工审核 |
| 自动删除疑似重复文件 | 可能误删证据 |
| 自动覆盖人工修改 | 保留人工优先 |

## 11. 审计要求

每次决策必须记录：决策时间、来源、状态变更、置信度、源证据、人工修改前后值、自动动作规则 ID。
