# 01_PRD：智能会计交付助手产品需求文档

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 内容来源与对齐说明

本交付包以 `03_srp_smart_accounting_b3_v2.md` 为主线，重点对齐 AG-B3-01 P0 场景：M8 邮件凭证自动处理、M9 历史邮件检索催票、M1/M2 凭证状态追踪与邮件催票。调研总结用于支撑真实业务痛点：邮件超载、文件命名混乱、附件下载与上传耗时、Blue Sheets 初始设置复杂、Vendor Rule 难复用、缺票发现滞后、客户历史沟通上下文丢失、Xero / Blue Sheets / Email / Excel / PORTAL / XPM 多系统数据分散。

核心边界：AI 不替代会计经理的专业判断；PoC 默认只创建 Xero Draft，不自动 approve；催票邮件默认生成草稿，由 Staff / Manager 审核后发送。

## 1. 产品一句话

智能会计交付助手是一个面向新加坡会计团队月结前端流程的 AI workflow system，帮助会计人员自动捕获客户邮件中的 invoice / bank statement 等凭证，调用 file.ai / Blue Sheets 完成结构化提取，经人工确认后进入 Xero，并在月结缺票时自动检索历史邮件、生成催票建议和追踪响应状态。

## 2. 背景与问题

| 痛点 | 业务表现 | 影响 |
|---|---|---|
| 邮件超载 | 大量客户邮件、内部邮件、CC / Distribution List，重要邮件容易被淹没 | 客户响应慢、文件处理延迟 |
| 附件处理人工化 | 客户通过邮件发送 invoice、bank statement、expense claims，员工逐一下载并上传 Blue Sheets | 重复劳动高，容易遗漏 |
| 文件命名和分类混乱 | Supplier Invoice、Sales Invoice、Bank Statement 混在同一邮件或文件夹 | Staff 需要人工分类 |
| 缺票发现滞后 | 到 SDT 开始做账或月结时才发现凭证缺失 | 反复催客户，月结周期变长 |
| 历史邮件检索耗时 | 缺票时需人工翻找大量历史邮件 | 会计经理和 Staff 时间被低价值检索消耗 |
| 多系统数据分散 | Email、Blue Sheets、Xero、XPM、PORTAL、Excel 状态不一致 | 无统一视图 |
| Blue Sheets 初始设置复杂 | 新客户 / 新 Vendor 需要创建 Rule，科目和 GST 判断依赖经验 | Junior 易错，Senior Review 压力大 |

## 3. 产品目标

将月结前端处理从：

```text
人工查邮件 → 手动下载附件 → 手动分类 → 手动上传 OCR → 人工确认 → 手动/半手动进 Xero → 月结时翻历史邮件催票
```

转变为：

```text
AI 监控邮件 → 自动识别附件 → 自动上传 file.ai / Blue Sheets → OCR 结果结构化 → 人工确认 → 写入 Xero Draft → 缺票自动检索历史邮件 → 生成催票邮件 → 状态回流到月结面板
```

## 4. 用户角色

| 用户 | 目标 |
|---|---|
| Junior Staff / Accountant | 少做下载、分类、上传；快速确认 OCR 结果和异常项 |
| Senior / Manager | 看见风险项、低置信项、缺票状态和月结进度 |
| CST / SDT | 知道客户文件是否已提交、哪些客户需要 follow-up |
| 客户 | 更早收到清晰的缺票请求，减少反复沟通 |
| FDE / 技术团队 | 有明确 API、数据字段、状态流和验收边界 |

## 5. 范围定义

### In Scope

| 模块 | 范围 |
|---|---|
| M8 邮件凭证自动处理 | 读取客户邮件、识别附件、分类、上传 file.ai / Blue Sheets、回收 OCR、生成待确认任务 |
| M9 历史邮件检索催票 | 月结缺票时自动检索历史邮件，若未找到则生成催票邮件草稿 |
| 凭证状态追踪 | 追踪每个客户每个期间的凭证完整度、OCR、人工确认、Xero 写入 |
| 人工审核关卡 | 对低置信 OCR、金额异常、客户匹配不确定、GST / 科目不确定进行人工确认 |
| 邮件催票 | 生成催票邮件，可配置草稿、人工审核后发送或高置信自动发送 |
| KPI 追踪 | 记录月结周期、凭证覆盖率、催票响应率、错误率、人工处理时间 |

### Out of Scope

| 不做 | 原因 |
|---|---|
| 不替代会计经理最终专业判断 | 中游会计判断专业性强、风险高 |
| 不自动发送法律函件或正式催款函 | 涉及合规和客户关系风险 |
| 不在 PoC 阶段覆盖 UFS / XBRL 全流程 | 当前聚焦 AG-B3-01 月结前端 |
| 不在 PoC 阶段解决 Global Client ID 长期治理 | 先通过临时 client mapping 表试点 |
| 不强制客户迁移到标准 SharePoint 文件夹 | 客户配合度未知，邮件仍是主通道 |

## 6. 核心功能需求

| Requirement ID | 需求 | 优先级 | 验收标准 |
|---|---|---|---|
| R-DASH-01 | 显示客户月结进度、凭证覆盖率、缺票数量、待人工确认数量 | P0 | 一个页面识别阻塞客户 |
| R-EMAIL-01 | 自动读取指定邮箱中的客户邮件和附件 | P0 | 邮件 metadata、thread_id、附件列表进入队列 |
| R-EMAIL-02 | 自动判断邮件是否包含会计凭证 | P0 | invoice / bank statement / expense claim / other 可分类 |
| R-OCR-01 | 调用 file.ai / Blue Sheets 并获取 OCR 结果 | P0 | 返回 vendor、invoice no、date、amount、currency、GST、line items |
| R-OCR-02 | 显示原附件预览、OCR 字段、置信度和异常提示 | P0 | 用户可对照原文修改字段 |
| R-XERO-01 | 创建 Xero Draft，不自动 approve | P0 | 成功返回 draft ID 或 mock draft ID |
| R-MISS-01 | 基于月结清单识别应收凭证与实收凭证差异 | P0 | 显示缺失月份、类型、客户、vendor |
| R-SEARCH-01 | 按 client、period、vendor、document type、invoice number 检索历史邮件 | P0 | 返回候选邮件、附件和匹配理由 |
| R-CHASE-01 | 生成催票邮件草稿，包含缺失凭证清单 | P0 | 邮件可编辑、预览、发送或保存草稿 |
| R-AUDIT-01 | 保存 source email、attachment、OCR、人工确认、Xero 写入、催票记录 | P0 | 任一凭证可追溯证据链 |

## 7. 非功能需求

| 类别 | 需求 |
|---|---|
| 安全 | 最小权限，只读取试点客户 / 指定邮箱 / 指定日期范围 |
| 隐私 | 邮件正文、附件、客户财务数据不得用于无关模型训练 |
| 审计 | 所有 AI 判断、人工修改、Xero 写入、邮件发送均需日志 |
| 可解释性 | 每个状态和建议必须能追溯来源证据 |
| 可靠性 | API 失败时重试、降级和提示，不得静默失败 |
| 可配置性 | 置信度阈值、催票间隔、自动发送开关、客户白名单可配置 |

## 8. 验收标准

| 验收维度 | PoC 标准 |
|---|---|
| 邮件读取 | 读取试点客户指定范围内邮件、附件和 thread_id |
| 附件分类 | 支持 invoice / bank statement / expense claim / other 四类 |
| OCR 链路 | 完成上传、结果回收、字段展示、人工修改 |
| Xero 链路 | 至少写入 Draft 或模拟写入 |
| 缺票链路 | 基于月结清单识别缺票并触发历史邮件检索 |
| 催票链路 | 生成催票草稿并记录发送 / 回复状态 |
| 审计链路 | 追踪邮件来源、附件来源、AI 判断、人工确认和系统写入 |
