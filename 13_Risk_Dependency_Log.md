# 13_Risk_Dependency_Log：风险与依赖清单

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 风险管理目标

记录 AG-B3-01 从 PoC 到试点上线的技术、数据、业务、合规和采用风险。重点关注 Day 0 阻塞项：邮箱 API、file.ai / Blue Sheets API、Xero 写入权限。

## 2. Dependency Log

| ID | 依赖 | 阻塞级别 | Owner | 状态 | 解除条件 |
|---|---|---|---|---|---|
| DEP-01 | 邮箱 API 接入 | P0 | IT / FDE | Open | 可读取邮件、附件、thread_id |
| DEP-02 | file.ai / Blue Sheets API | P0 | IT / Vendor | Open | 可上传文件并获取 OCR 结果 |
| DEP-03 | Xero API 写入权限 | P0 | IT / Finance | Open | 可创建 Draft / 测试写入 |
| DEP-04 | 试点客户 mapping 表 | P0 | FDE / Accounting | Open | client_id、email、Xero contact 对齐 |
| DEP-05 | 月结清单模板 | P1 | Accounting Manager | Open | 明确 required docs 和 deadline |
| DEP-06 | 催票邮件模板 | P1 | CST / SDT | Open | L1 / L2 / L3 模板确认 |
| DEP-07 | 数据合规边界 | P0 | Legal / IT | Open | 明确邮件和附件保存、访问、训练限制 |

## 3. Risk Register

| Risk ID | 风险 | 影响 | 概率 | 严重度 | 缓解措施 |
|---|---|---|---|---|---|
| R-01 | 邮箱 API 不可用 | M8 / M9 主链路无法启动 | Medium | Critical | generic mailbox 转发或手工导出邮件 |
| R-02 | file.ai / Blue Sheets API 不支持结果回传 | OCR 自动化断裂 | Medium | Critical | 手动导出 OCR 结果或 mock API |
| R-03 | Xero 写入权限审批慢 | 无法形成闭环 | Medium | High | mock endpoint / CSV 模拟 Draft |
| R-04 | 客户主数据无法匹配 | 邮件归属错误 | High | High | PoC 维护 5–10 个客户 mapping 表 |
| R-05 | 客户附件质量差 | OCR 准确率低，异常多 | High | Medium | Exception Queue 和人工修正 |
| R-06 | 员工不信任 AI 判断 | 采用率低 | Medium | High | 证据链、置信度、人工可控、先 Draft |
| R-07 | 自动催票引发客户关系风险 | 客户体验受损 | Medium | High | PoC 默认生成草稿，不自动发送 |
| R-08 | 员工跳过审核 | OCR 错误进入 Xero | Medium | High | 低置信禁用批量确认，默认 Draft |
| R-09 | 数据保存不合规 | 法务 / 安全风险 | Low-Medium | Critical | 最小权限、数据保留策略、audit log |
| R-10 | KPI 基线缺失 | 难以证明价值 | High | Medium | PoC 前先采集基线或标明无基线 |
| R-11 | 多系统状态不同步 | Dashboard 不可信 | Medium | High | 明确 source of truth 和 sync timestamp |
| R-12 | Vendor Rule 难标准化 | 科目推荐价值有限 | High | Medium | V1 不强依赖，作为 P2 扩展 |

## 4. Data Risks

| 数据风险 | 例子 | 缓解 |
|---|---|---|
| 客户名称不一致 | Email 写简称，Xero 是 legal name | client alias / UEN mapping |
| 同一邮箱服务多个客户 | external accounting contact | 人工确认或 thread context |
| 文件名无意义 | scan001.pdf | 用 OCR 内容判断 |
| 多页发票被拆分 | page1 / page2 单独处理 | 多页合并建议 |
| 客户历史邮件缺失 | 清理 / 不在可读邮箱 | 标记 Search Coverage 低 |
| 月结清单不完整 | 应收凭证定义不清 | 统一模板 |

## 5. Go-Live Readiness Checklist

| Checklist | 状态 |
|---|---|
| 邮箱 API 可用 | TBD |
| Blue Sheets / file.ai API 可用 | TBD |
| Xero Draft 写入可用 | TBD |
| 试点客户 mapping 完成 | TBD |
| 月结清单模板确认 | TBD |
| 催票模板确认 | TBD |
| Human gate 规则确认 | TBD |
| 数据保存与权限确认 | TBD |
| UAT P0 通过 | TBD |
| KPI 采集事件上线 | TBD |
