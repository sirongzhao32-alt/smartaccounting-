# 02_PoC_Plan：智能会计交付助手 PoC 计划

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 内容来源与对齐说明

本交付包以 `03_srp_smart_accounting_b3_v2.md` 为主线，重点对齐 AG-B3-01 P0 场景：M8 邮件凭证自动处理、M9 历史邮件检索催票、M1/M2 凭证状态追踪与邮件催票。调研总结用于支撑真实业务痛点：邮件超载、文件命名混乱、附件下载与上传耗时、Blue Sheets 初始设置复杂、Vendor Rule 难复用、缺票发现滞后、客户历史沟通上下文丢失、Xero / Blue Sheets / Email / Excel / PORTAL / XPM 多系统数据分散。

核心边界：AI 不替代会计经理的专业判断；PoC 默认只创建 Xero Draft，不自动 approve；催票邮件默认生成草稿，由 Staff / Manager 审核后发送。

## 1. PoC 目标

验证 AG-B3-01 的最小可行闭环：

```text
客户邮件 → 附件自动捕获 → OCR / file.ai / Blue Sheets 处理 → 人工确认 → Xero Draft → 缺票识别 → 历史邮件检索 → 催票草稿 → 状态回流
```

PoC 不追求一次性自动化全部会计流程，而是验证 M8 和 M9 是否能减少人工查邮件、下载、上传、翻历史邮件和催票。

## 2. PoC 范围

| 范围 | 描述 |
|---|---|
| 试点客户 | 5–10 个典型客户，覆盖 Monthly / Quarterly / Annual 至少 2 类复杂度 |
| 邮件数据 | 指定 shared mailbox 或试点 staff 邮箱中的客户邮件，限定日期范围 |
| 附件类型 | Supplier Invoice、Sales Invoice、Bank Statement、Expense Claims、Other |
| OCR 工具 | file.ai / Blue Sheets；如 API 未开，用模拟接口替代 |
| Xero | 优先写入 Draft；如权限未开，用 mock endpoint 或 CSV |
| 缺票检测 | 基于月结清单 / 应收凭证清单识别缺失 |
| 催票邮件 | 默认生成草稿，由 Staff 审核后发送 |

## 3. PoC 阶段计划

| 阶段 | 时间 | 目标 | 输出物 |
|---|---|---|---|
| Phase 0：Day 0 Readiness | Week 0–1 | 确认 API、权限、样本、试点客户 | 依赖确认表、样本数据包、测试账号 |
| Phase 1：Email Intake | Week 1–2 | 读取邮件、附件、metadata | 邮件队列原型、附件分类结果 |
| Phase 2：OCR + Review | Week 2–3 | 上传 OCR，返回字段并人工确认 | OCR Review 页面、字段映射 |
| Phase 3：Xero Draft | Week 3–4 | 写入 Xero Draft 或模拟写入 | Xero 写入日志、失败处理 |
| Phase 4：Missing Docs + Search | Week 4–5 | 识别缺票并检索历史邮件 | 缺票追踪页面、检索结果 |
| Phase 5：Chase Email + KPI | Week 5–6 | 生成催票草稿、追踪响应、计算 KPI | Demo 版本、KPI 报告、UAT 结果 |

## 4. Day 0 前置依赖

| ID | 依赖 | 阻塞等级 | Owner | 验证方式 | 未满足时降级方案 |
|---|---|---|---|---|---|
| DR-01 | InCorp 邮箱 API | P0 | IT / FDE | 读取邮件、附件、thread_id | 人工导出 EML / MSG 或转发至监控邮箱 |
| DR-02 | file.ai / Blue Sheets API | P0 | IT / Vendor | 上传文件并返回 OCR | 手动上传后导出结果回填 |
| DR-03 | Xero API 写入权限 | P0 | IT / Finance | 创建 Draft / 测试记录 | CSV / mock Xero endpoint |
| DR-04 | 月结清单模板 | P1 | Accounting / FDE | 明确应收凭证和 deadline | 手工整理试点客户清单 |
| DR-05 | 客户映射表 | P0 | FDE / Accounting | client name、UEN、email、Xero contact 可匹配 | 先用人工 mapping |
| DR-06 | 邮件发送权限 | P1 | IT / Business Owner | 可发送草稿或正式邮件 | 只生成草稿 |

## 5. 试点客户选择标准

| 维度 | 建议 |
|---|---|
| 客户数量 | 5–10 个 |
| 文件量 | 包含低量和高量客户 |
| 文件类型 | 至少 invoice + bank statement |
| 数据质量 | 覆盖标准命名、混乱命名、多附件、缺票 |
| 系统可用性 | 有 Xero 数据、Blue Sheets 可处理、邮件可访问 |
| 业务代表性 | 覆盖 Monthly / Quarterly / Annual 至少两类 |

## 6. 成功标准

| 模块 | 成功标准 |
|---|---|
| Email Intake | 80% 以上试点邮件可被拉取并识别附件 |
| 附件分类 | invoice / bank statement / expense claim / other 分类可用，错误可人工修正 |
| OCR 回收 | 关键字段可展示并支持人工编辑 |
| Xero Draft | 可成功写入 Draft 或生成可导入数据 |
| 缺票识别 | 能识别缺月份、缺 invoice、缺 bank statement |
| 历史邮件检索 | 能返回候选邮件、附件和匹配理由 |
| 催票草稿 | 能生成清晰、可编辑、带缺失清单的邮件草稿 |

## 7. 业务 KPI

| KPI | PoC 目标 | 采集方式 |
|---|---|---|
| 凭证处理人工时间 | 相比人工流程下降 30%+ | task timestamp |
| 缺票发现提前量 | 缺票能在月结开始前或更早暴露 | missing docs log |
| 催票响应率 | 目标 ≥70%，基线待确认 | sent / replied / file received |
| 凭证覆盖率 | 试点客户月结前 ≥90% | required docs vs confirmed docs |
| Xero 写入成功率 | ≥90% if API 可用 | xero write log |
| 系统错误率 | 严重阻塞错误 <5% | exception log |

## 8. Go / No-Go 决策

| 条件 | Go | No-Go |
|---|---|---|
| 邮件读取 | 可稳定读取试点邮箱 | 无法读取邮件且无转发替代 |
| OCR | 可返回结构化字段 | 只能人工上传且无法拿到结果 |
| Xero | 可写 Draft / mock | 完全无法模拟写入 |
| 缺票清单 | 有可用试点清单 | 无法定义应收凭证 |
| 业务 Owner | Accounting Manager 愿意试点 | 无明确业务 Owner |
