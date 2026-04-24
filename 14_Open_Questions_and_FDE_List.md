# 14_Open_Questions_and_FDE_List：待确认问题与 FDE 清单

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 文件目的

整理产品设计、PoC、API、数据、业务规则和客户汇报前必须确认的问题。建议 FDE 将这些问题分配给 IT、Accounting Manager、CST / SDT、Legal / Compliance 和 Vendor 方。

## 2. P0 阻塞问题

| ID | 问题 | 当前假设 | 确认对象 | 影响 |
|---|---|---|---|---|
| Q-P0-01 | InCorp 会计团队使用什么邮箱系统？ | Outlook 365 或 Gmail | IT | 决定 M8 / M9 是否可启动 |
| Q-P0-02 | 是否允许 AI 读取个人邮箱，还是只能读取 shared mailbox？ | 优先 shared mailbox / generic mailbox | IT / Legal | 权限和合规 |
| Q-P0-03 | file.ai / Blue Sheets 是否有 Upload API？ | 有，但需确认 | Vendor / IT | OCR 链路 |
| Q-P0-04 | Xero 是否可开测试环境和 Draft 写入权限？ | 可申请 | Finance IT | 闭环写入 |
| Q-P0-05 | PoC 试点客户是哪 5–10 个？ | 待选 | Accounting Manager | 测试代表性 |
| Q-P0-06 | 月结 required docs 清单如何定义？ | 由 Accounting 提供 | Accounting Manager | 缺票检测 |

## 3. 数据问题

| ID | 问题 | 确认对象 | 说明 |
|---|---|---|---|
| Q-DATA-01 | 是否已有 Global Client ID？ | IT / Data | 如无，PoC 用临时 client_id |
| Q-DATA-02 | UEN 是否可用于客户匹配？ | Accounting / PORTAL owner | 新加坡客户建议用 UEN |
| Q-DATA-03 | Excel Master List 字段有哪些？ | CST | 需要客户、联系人、服务、FY、状态 |
| Q-DATA-04 | Xero Contact 如何映射到客户？ | Finance IT | 需 xero_contact_id |
| Q-DATA-05 | 客户 email domain 是否可靠？ | CST / SDT | 个人邮箱和代理联系人可能误匹配 |
| Q-DATA-06 | 是否允许保存邮件正文全文？ | Legal / IT | 若不允许，保存摘要和 metadata |
| Q-DATA-07 | 附件保存期限多久？ | Legal / IT | 财务凭证可能有合规要求 |

## 4. 业务规则问题

| ID | 问题 | 确认对象 | 说明 |
|---|---|---|---|
| Q-BIZ-01 | 哪些文档类型属于 PoC 必须覆盖？ | Accounting | 建议先 invoice + bank statement |
| Q-BIZ-02 | Bank Statement 每月是否必须一份？ | Accounting | 缺失规则口径 |
| Q-BIZ-03 | Supplier Invoice 如何判断缺失？ | Accounting | 按序号、vendor、月份还是 expected count |
| Q-BIZ-04 | GST 9% 校验是否放入 PoC？ | Accounting | 建议先提示，不自动判断最终税务 |
| Q-BIZ-05 | Vendor Rule 由谁确认？ | Senior / Manager | Junior 不应独立确定复杂科目 |
| Q-BIZ-06 | 什么情况需要 Senior Review？ | Manager | 金额异常、GST、低置信、客户不确定 |
| Q-BIZ-07 | 什么情况需要 Manager Review？ | Manager | 催票升级、客户争议、长期欠款 |

## 5. 催票与邮件问题

| ID | 问题 | 确认对象 | 说明 |
|---|---|---|---|
| Q-EMAIL-01 | 催票邮件是否允许自动发送？ | Manager / Legal | PoC 建议默认草稿 |
| Q-EMAIL-02 | L1 / L2 / L3 催票间隔是多少？ | CST / SDT | 如 0天、3天、7天 |
| Q-EMAIL-03 | 催票邮件从谁的邮箱发？ | IT / Manager | 个人邮箱、generic email、系统邮箱 |
| Q-EMAIL-04 | 是否需要 BCC generic mailbox？ | IT / Manager | 用于监控和备份 |
| Q-EMAIL-05 | 客户回复到 Manager 个人邮箱怎么办？ | CST / Manager | 是否要求 forward / BCC |
| Q-EMAIL-06 | 邮件 bounce 后如何处理？ | CST | 更新联系人，暂停自动催票 |

## 6. FDE 行动清单

| 优先级 | 行动 | 输出 |
|---|---|---|
| P0 | 召开 IT API 确认会 | 邮箱 / Blue Sheets / Xero API 可行性表 |
| P0 | 选择试点客户 | Pilot client list |
| P0 | 收集邮件与附件样本 | Sample email & document pack |
| P0 | 整理 client mapping | Client mapping table |
| P0 | 整理月结 required docs 模板 | Month-end checklist |
| P1 | 收集催票模板 | L1 / L2 / L3 email templates |
| P1 | 访谈 Staff 页面需求 | UX notes |
| P1 | 定义 KPI baseline | Baseline data sheet |
| P2 | 收集 Vendor Rule 样本 | Vendor Master List draft |
