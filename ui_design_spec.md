# UI Design Spec

---

## Page List

### 文档来源与校验

| 来源 | 用途 |
|------|------|
| `06_Wireframe_Design_Spec.md` §2 信息架构、§3–§10 各页线框 | Sidebar 主干与页面命名 |
| `05_Feature_Breakdown.md` F1–F12 | 功能模块与优先级 |
| `01_PRD.md`、`02_PoC_Plan.md` | 范围：M8、M9；文首「M1/M2 凭证状态追踪与邮件催票」 |
| `04_User_Journey_and_Task_Flow.md` | Dashboard → Client Workspace 动线 |

### M1–M9 覆盖说明（避免臆造）

- **文档明确出现的模块编号**：**M8**（邮件凭证自动处理）、**M9**（历史邮件检索催票），见 `01_PRD.md` §5。
- **M1 / M2**：仅在 `01_PRD.md`、`02_PoC_Plan.md` **文首对齐句**中出现「M1/M2 凭证状态追踪与邮件催票」，**未拆分为独立字段或子系统表**；侧栏标签 **M1\*** = 凭证状态与审阅；**M2\*** = 催票与回复追踪（与 F8、M9 催票链路重叠处并列标注）。
- **M3–M7**：交付包 **未** 将 M3–M7 定义为独立 PRD 模块条；侧栏 **M3\***（月结工作台语义）、**M6\***（报表/KPI 语义）为 **信息架构映射**，对应 `06` 中 **Dashboard + Client Workspace** 与 **KPI & Reports**，**非**新增 PRD 模块条文。

### Sidebar：一级 / 二级（完整路由，无遗漏）

以下与 `06_Wireframe_Design_Spec.md` §2 **Global Navigation** 对齐，并补足 `05` F9、F11、F12；**二级**为可路由子页或 Tab。

| 层级 | 侧栏名称（产品可显示名） | 文档页 / 功能 | 模块标签 |
|------|---------------------------|---------------|----------|
| **一级** | **Dashboard**（月结总览、覆盖率监控） | `06` 页面 1；F1 | F1；**M3\***；汇聚 M8/M9 状态 |
| **一级** | **Month-End Workspace**（客户工作台） | `06` 页面 2；`04` Journey | **M3\***；F1/F6/F8/F10 |
| **二级** | Overview | `06` §4 Tab | **M3\*** |
| **二级** | Documents（凭证列表） | `06` §4 Tab | **M1\*** |
| **二级** | Emails | `06` §4 Tab；F2 | **M8** |
| **二级** | Missing Docs | `06` §4 Tab；F6 | **M9** |
| **二级** | Chase History | `06` §4 Tab；F8 | **M2\*** |
| **二级** | Audit Trail | `06` §4 Tab；F10 | R-AUDIT-01 |
| **一级** | **Email Inbox**（邮件处理 / Intake Queue） | `06` 页面 3；F2 | **M8** |
| **一级** | **Document Classification** | `06` 页面 4；F3 | **M8** |
| **一级** | **Review Tasks**（待审队列；线框 IA 项） | `06` §2；与 V0「Review Page」对应 | **M1\*** |
| **一级** | **Document Review / OCR**（单证确认页） | `06` 页面 5；F4+F5 | **M1\*** |
| **一级** | **Voucher Board**（凭证管理总表；与上并列时二选一或 deep-link 同源） | 交付包 **06 未使用该英文名**；功能上对应 **Client › Documents + Review Tasks 列表** 的产品命名占位 | **M1\*** |
| **一级** | **Missing Documents**（缺票追踪） | `06` 页面 6；F6 | **M9** |
| **一级** | **Chase Center**（检索与催票；侧栏分组名） | `06` §2「Search & Chase」 | **M2\*** / **M9** |
| **二级** | Historical Email Search Results | `06` 页面 7；F7 | **M9** |
| **二级** | Chase Email Composer | `06` 页面 8；F8 | **M2\*** / **M9** |
| **一级** | **Exceptions**（异常队列） | `06` §2；F9；V2 Pilot 强化 | F9；**M8/M9** 异常汇聚 |
| **一级** | **Reports**（KPI & Reports） | `06` §2；F1 摘要 + `12_KPI_Measurement_Plan.md` | **M6\***；F1 |
| **一级** | **Settings**（系统设置） | `06` §2；F11 | F11 P1 |
| **二级** | Rule & Config | `05` F11 | F11 |
| **二级** | Vendor Rule Assistant | `05` F12；V3 P2 | F12 |

### 与用户给定示例条目的对照（便于评审）

- **Dashboard（覆盖率监控）** → 上表 **Dashboard**。
- **Email Inbox（邮件处理 / M8）** → **Email Inbox**；**Document Classification** 为同链路延伸（**M8**），列为一 **一级** 以免与 `06` 页面 4 冲突。
- **Voucher Board（凭证管理 / M1）** → 上表 **Voucher Board**；**Review Tasks**、**Document Review**、**Client › Documents** 为 **M1\*** 同源能力，实施时可合并路由，**本清单不删页**以满足「无遗漏线框页」。
- **Chase Center（催票 / M2/M9）** → **Chase Center** 下 **Historical Search Results** + **Chase Composer**。
- **Month-End Workspace（月结 / M3）** → **Month-End Workspace** 及 **6 个二级 Tab**。
- **Reports（报表 / M6）** → **Reports（KPI & Reports）**。
- **Settings（系统设置）** → **Settings** 及 **Rule & Config**、**Vendor Rule Assistant**。

### 遗漏校验结果

| 检查项 | 结果 |
|--------|------|
| `06` Global Navigation 八项 | 均已映射（Intake、Missing、Search&Chase、Review、Exceptions、KPI&Reports、Settings；Dashboard + Client 归入 Month-End + Dashboard）。 |
| `06` 线框页面 1–8 | 均已出现在上表（含 Document Classification、Document Review）。 |
| `05` F9 / F11 / F12 | **Exceptions**、**Settings** 二级已列。 |
| **M8** | Email Inbox、Classification、Client Emails、Intake 相关。 |
| **M9** | Missing Documents、Search Results、Chase、Client Missing Docs。 |
| **M1\*** / **M2\*** | Voucher Board、Review Tasks、Document Review、Documents、Chase History、Chase Composer。 |
| **M3\*** / **M6\*** | Dashboard、Month-End Workspace、Reports。 |
| **M4、M5、M7** | 交付包 **无** 对应模块定义；若商业侧栏必须显示 **M4–M7**，需 **FDE 另发模块定义** 后再增页，**本清单不臆造**。 |

### 扁平化页面清单（一条一路由，便于开发拆 Story）

- **Dashboard**（L1｜覆盖率监控 / F1 / **M3\***）
- **Month-End Workspace › Overview**（L2｜**M3\***）
- **Month-End Workspace › Documents**（L2｜凭证列表 / **M1\***）
- **Month-End Workspace › Emails**（L2｜**M8**）
- **Month-End Workspace › Missing Docs**（L2｜**M9**）
- **Month-End Workspace › Chase History**（L2｜**M2\***）
- **Month-End Workspace › Audit Trail**（L2｜F10）
- **Email Inbox**（L1｜邮件处理 / Intake / **M8**）
- **Document Classification**（L1｜**M8**）
- **Review Tasks**（L1｜待审队列 / **M1\***）
- **Document Review / OCR**（L1｜单证确认 / F4+F5 / **M1\***）
- **Voucher Board**（L1｜凭证管理总表 / **M1\***；与 Documents+Review 同源占位，见上表说明）
- **Missing Documents**（L1｜缺票追踪 / **M9**）
- **Chase Center › Historical Email Search Results**（L2｜**M9**）
- **Chase Center › Chase Email Composer**（L2｜催票 / **M2\*** / **M9**）
- **Exceptions**（L1｜异常队列 / F9）
- **Reports**（L1｜KPI & Reports / **M6\***）
- **Settings › Rule & Config**（L2｜F11）
- **Settings › Vendor Rule Assistant**（L2｜F12 P2）

---

## Page Designs

> 字段类型列：`string` | `number` | `date` | `datetime` | `enum` | `array` | `text` | `boolean`  
> 「数据来源」列：`09` = `09_Data_Mapping.md` 章节（§3 Client … §9 KPI Event）。

---

## Page: Dashboard

**路由**：一级 `Dashboard`  
**对齐**：`06_Wireframe_Design_Spec.md` §3；`05_Feature_Breakdown.md` F1；`01_PRD.md` R-DASH-01。

### 1. 页面目标

- **用户**：Junior Staff / Accountant、Senior / Manager（`01_PRD.md` §4）。
- **解决**：一屏识别客户月结阻塞、凭证覆盖与待确认量（R-DASH-01）；多系统状态汇聚（PRD §2）。
- **对应模块**：**F1**；**M3\***（月结总览语义）；汇聚 **M8**（邮件/附件链路 KPI）、**M9**（缺票/检索/催票 KPI）；**M1\***（待审凭证通过 Document 聚合体现）。

### 2. 页面结构

- **Header（Top Bar）**：产品名（无 09 字段）；周期上下文；同步状态（**非 09，标 UI-only / 待字典**）；当前用户角色（**非 09**）。
- **Filter Bar**：客户、期间、风险维度（筛选作用于下方主表聚合行）。
- **Main Content**：KPI 卡片区 + Risk Tabs + Customer Status 主表。
- **Side Panel**：Today’s Priority（与主表同源字段的快捷列表）。
- **Footer**：无（`06` 未要求）。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter — 客户 | `client_id` | string | §3 Client；联结 §6 Document / §8 Missing | 否 | 下拉筛选 |
| Filter — 客户展示 | `legal_name`, `trading_name` | string | §3 Client | 否 | 展示标签 |
| Filter — 期间 | `period` | string | §6 Document；§8 Missing | 否 | 选择期间 |
| Filter — 风险（映射枚举） | `missing_reason` | enum | §8 Missing（聚合行） | 否 | 多选 |
| Filter — 风险 | `blocker_level` | enum | §8 Missing | 否 | 多选 |
| Filter — 风险 | `review_status` | enum | §6 Document（聚合） | 否 | 多选 |
| Filter — 风险 | `xero_status` | enum | §6 Document（聚合） | 否 | 多选 |
| KPI Card — 邮件捕获 | `client_id`, `message_id`, `timestamp` | string, string, datetime | §9 `email_captured` Key Fields | 否 | 跳转 Email Inbox / Emails |
| KPI Card — 附件分类 | `doc_type`, `confidence` | string, number | §9 `attachment_classified` | 否 | 跳转 Document Classification |
| KPI Card — OCR 完成 | `duration`, `confidence` | number, number | §9 `ocr_completed` | 否 | 跳转 Review / Document Review |
| KPI Card — 审核完成 | `reviewer`, `duration`, `changes_count` | string, number, number | §9 `review_completed` | 否 | 跳转 Review Tasks |
| KPI Card — Xero Draft | `xero_id`, `success` | string, boolean | §9 `xero_draft_created` | 否 | 跳转 Document Review / Exceptions |
| KPI Card — 缺票检测 | `missing_doc_id`, `period` | string, string | §9 `missing_doc_detected` | 否 | 跳转 Missing Documents |
| KPI Card — 检索完成 | `result_type`, `candidate_count` | string, number | §9 `search_completed` | 否 | 跳转 Historical Search Results |
| KPI Card — 催票发送 | `chase_level`, `recipient` | string, string | §9 `chase_sent` | 否 | 跳转 Chase Composer |
| KPI Card — 客户回复 | `response_type`, `duration` | string, number | §9 `client_replied` | 否 | 跳转 Month-End › Emails |
| Customer Status — 客户列 | `client_id`, `legal_name`, `trading_name`, `status`, `mapping_confidence` | string, string, string, enum, number | §3 Client | 否 | 点击进 Month-End Workspace |
| Customer Status — 缺票聚合列 | `period`, `required_doc_type`, `expected_count`, `received_count`, `confirmed_count`, `missing_reason`, `blocker_level`, `status` | string, enum, number×3, enum×3 | §8 Missing（按 client 聚合多行时可取首行/最坏 blocker） | 否 | 点击进 Missing Documents |
| Customer Status — 凭证聚合列 | `document_type`, `review_status`, `xero_status`, `confidence_score` | enum, enum, enum, number | §6 Document（聚合） | 否 | 点击进 Review / Documents |
| Customer Status — 最近邮件 | `subject`, `received_at`, `sender_email` | string, datetime, string | §4 Email（按 client 最近一封） | 否 | 跳转 Month-End › Emails |
| Side — Today Priority | 同上 KPI / Missing / Document 关键列子集 | 同上 | 同上 | 否 | 快捷跳转同主表 |

**说明**：`06` 中 Deadline、Coverage%、Risk 文案、Next Action、Owner 等 **无 `09` 单列** → 不写入上表；若 UI 必须展示，标注 **待数据字典**，不得冒充 Data Mapping 字段。

### 4. 表格 / 列表

- **columns（Customer Status 主表）**：`client_id`, `legal_name`, `trading_name`, `mapping_confidence`, `status`, `period`, `required_doc_type`, `expected_count`, `received_count`, `confirmed_count`, `missing_reason`, `blocker_level`, `review_status`, `xero_status`, `confidence_score`, `subject`, `received_at`, `sender_email`（列集合随实现聚合策略裁剪，字段名不超出 09）。
- **row actions**：打开 **Month-End Workspace**（默认 Overview）；打开 **Missing Documents**（带 `client_id`/`period`）；打开 **Review Tasks** / **Document Review**（带 `client_id`）；打开 **Email Inbox**（可选 query）。

### 5. 状态

- **loading**：Top Bar、KPI 卡、主表、Side Panel 骨架或遮罩。
- **empty**：无试点客户 / 所选期间无任何 §3/§6/§8 可展示行 → 空态文案 + 引导 Settings（F11）或扩大期间（若产品允许）。
- **error**：邮件 API、聚合服务失败 → 错误条/Toast + 重试（PRD NFR）；**不静默失败**。
- **success**：筛选、排序、行点击可用。

### 6. 交互流程

- **点击**：客户行 → **Month-End Workspace**；缺票相关 → **Missing Documents**；审核态 → **Review Tasks** / **Document Review**；KPI 卡 → 对应一级/二级页。
- **编辑**：本页 **不编辑** 业务主数据（只读总览）。
- **跳转**：见上；全局导航切换。
- **触发模块**：不直接调用 Agent；展示 **Orchestrator** 下游结果（`07_AI_Agent_Workflow.md`）反映在 KPI 与表数据。

### 7. 边界情况

- **数据缺失**：`trading_name`、`primary_contact_email` 等 Preferred 空（§3）→ 空占位；`expected_count` Preferred 空（§8）→ 不显示比率类指标。
- **OCR 失败**：`missing_reason = ocr_failed`（§8）行高亮；链至 Missing / Review。
- **API 失败**：见 **error** 状态。
- **重复数据**：`duplicate_candidate`（§5 Attachment，经 Document 联结）在跳转 Documents/Review 后处理；Dashboard 仅聚合提示（若有）。

### 8. 页面跳转关系

- **来源**：登录落地、全局 **Dashboard**。
- **去向**：**Month-End Workspace › Overview**；**Missing Documents**；**Email Inbox**；**Review Tasks**；**Document Review / OCR**；**Historical Search Results**；**Chase Composer**；**Exceptions**；**Reports**；**Settings**。

---

## Page: Month-End Workspace › Overview

**路由**：一级 `Month-End Workspace` + 二级 Tab **Overview**  
**对齐**：`06_Wireframe_Design_Spec.md` §4 Tabs「Overview」；`04_User_Journey_and_Task_Flow.md`；`05` F1/F6/F8/F10 摘要。

### 1. 页面目标

- **用户**：Staff、Senior、Manager、CST/SDT（`01_PRD.md` §4）。
- **解决**：在**已选客户**上下文下，单屏掌握文档覆盖、最新邮件、待审、缺票与催票动态（`06` §4 Overview bullets）。
- **对应模块**：**M3\***（客户月结工作台）；**M1\***（待审/凭证）；**M8**（邮件）；**M9**（缺票）；**M2\***（Chase 活动摘要）；**F10**（审计摘要入口）。

### 2. 页面结构

- **Header**：`Client §3` 全字段条（客户名、UEN、Xero contact 等）；`period` 上下文（§6/§8）。
- **Filter Bar**：`period`（string，§6 Document / §8 Missing）；可选 `document_type`（enum，§6）。
- **Main Content**：分块 — Document coverage by type；Latest incoming emails；Pending review tasks；Missing documents；Recent chase activity（`06` §4）。
- **Side Panel**：可选「本客户 KPI 子集」（§9 事件 Key Fields，与 Dashboard KPI 卡同结构）。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Client Header | `client_id` | string | §3 Client | 否 | 复制 |
| Client Header | `legal_name`, `trading_name` | string | §3 Client | 否 | — |
| Client Header | `uen` | string | §3 Client | 否 | — |
| Client Header | `email_domains` | array | §3 Client | 否 | 展开 |
| Client Header | `primary_contact_email` | string | §3 Client | 否 | 复制 |
| Client Header | `xero_contact_id` | string | §3 Client | 是（权限内） | 跳转 Settings 或内联保存 |
| Client Header | `xpm_client_id`, `portal_client_id` | string | §3 Client | 否 | — |
| Client Header | `status` | enum | §3 Client | 否 | — |
| Client Header | `mapping_confidence` | number | §3 Client | 否 | 低置信提示 |
| Filter | `period` | string | §6 Document；§8 Missing | 否 | 切换期间 |
| Filter | `document_type` | enum | §6 Document | 否 | 筛选 coverage 块 |
| Block — Coverage by type | `document_type` | enum | §6 Document | 否 | 点击进 **Documents** Tab |
| Block — Coverage by type | `review_status`, `xero_status`, `confidence_score` | enum, enum, number | §6 Document | 否 | 同上 |
| Block — Latest emails | `email_id`, `message_id`, `thread_id`, `mailbox_id`, `client_id`, `sender_email`, `subject`, `body_text`, `received_at`, `direction`, `email_intent`, `processing_status` | string / text / datetime / enum | §4 Email（按 `client_id` 最近 N 封） | `client_id` 可编辑（F2 Manual override） | 展开正文；跳转 **Emails** Tab |
| Block — Pending review | `document_id`, `attachment_id`, `client_id`, `document_type`, `period`, `vendor_name`, `invoice_number`, `invoice_date`, `currency`, `total_amount`, `gst_rate`, `account_code`, `confidence_score`, `review_status`, `xero_status`, `source_evidence` | 见 §6 各类型 | §6 Document（`review_status` ∈ pending\_*） | 抽屉内可编辑字段同 Document Review 策略 | 跳转 **Review** / 打开抽屉 |
| Block — Missing | `missing_doc_id`, `client_id`, `period`, `required_doc_type`, `expected_count`, `received_count`, `confirmed_count`, `missing_reason`, `blocker_level`, `status` | 见 §8 | §8 Missing | `status` 可编辑（与 F6 一致） | 跳转 **Missing Docs** Tab / **Missing Documents** 一级 |
| Block — Chase / reply 摘要 | `chase_level`, `recipient`；`response_type`, `duration` | string；string, number | §9 `chase_sent`；`client_replied` | 否 | 跳转 **Chase History** |
| Block — Chase / reply 邮件补充 | `subject`, `received_at`, `email_intent` | string, datetime, enum | §4 Email（intent 含 chase_response 等） | 否 | 跳转 **Chase History** / **Emails** |
| Side — KPI 子集 | 同 Dashboard KPI Key Fields | 同 §9 | §9 KPI Event | 否 | 跳转 Dashboard / Reports |

### 4. 表格 / 列表

- **Latest emails mini-table columns**：`received_at`, `sender_email`, `subject`, `processing_status`, `email_intent`。
- **Pending review mini-table columns**：`document_id`, `vendor_name`, `invoice_number`, `total_amount`, `currency`, `confidence_score`, `review_status`, `xero_status`。
- **Missing mini-table columns**：`period`, `required_doc_type`, `received_count`, `confirmed_count`, `expected_count`, `missing_reason`, `blocker_level`, `status`。
- **row actions**：跳转对应 Tab 或 **Document Review**；邮件行 **更正 `client_id`**（F2）；缺票行 **更新 `status`**。

### 5. 状态

- **loading**：Header、各分块独立 skeleton。
- **empty**：新客户无 §4 Email / §6 Document / §8 Missing → 各块独立 empty 文案。
- **error**：客户 ID 非法、分块 API 失败 → 分块 error + 重试。
- **success**：各块可点击跳转。

### 6. 交互流程

- **点击**：Coverage → **Documents**；邮件 → **Emails**；待审 → **Review Tasks** / **Document Review**；缺票 → **Missing Docs** / 一级 Missing；Chase → **Chase History**。
- **编辑**：**Email.client_id**（override）；**Missing.status**；**Client.xero_contact_id**（权限内）；不在 Overview 深编 Document 全量（导向 Document Review）。
- **跳转**：见上；**Dashboard** 返回。
- **触发模块**：**M8**（邮件展示/override）；**M9**（缺票）；**M1\***（待审）；**ChaseAgent**（仅展示 KPI，发送在 Chase Composer）。

### 7. 边界情况

- **数据缺失**：§3 Preferred 字段空；§4 `body_text` 空；§6 Conditional 字段空 → 轻提示。
- **OCR 失败**：§8 `missing_reason = ocr_failed` 在 Missing 块高亮。
- **API 失败**：分块 error，不静默。
- **重复数据**：§5 `duplicate_candidate` 经 Document 在 Pending 块标签提示。

### 8. 页面跳转关系

- **来源**：**Dashboard** 行点击；全局进入客户。
- **去向**：**Month-End Workspace** 其他 Tab（Documents、Emails、Missing Docs、Chase History、Audit Trail）；**Missing Documents**；**Review Tasks**；**Document Review**；**Email Inbox**；**Chase Composer**；**Settings**。

---

## Page: Month-End Workspace › Documents

**路由**：一级 `Month-End Workspace` + 二级 Tab **Documents**  
**对齐**：`06_Wireframe_Design_Spec.md` §4 Tab「Documents」；`05_Feature_Breakdown.md` F4/F5 入口；`01_PRD.md` R-OCR-02。

### 1. 页面目标

- **用户**：Junior Staff / Accountant、Senior / Manager（`01_PRD.md` §4）。
- **解决**：在**当前客户**下浏览、筛选、进入单条凭证（Document）及关联附件/邮件上下文，衔接 OCR 确认与 Xero Draft（`06` §4；`05` F4/F5）。
- **对应模块**：**M1\***（凭证状态追踪与审阅）；上游 **M8**；**F4、F5**。

### 2. 页面结构

- **Header**：Workspace 壳 — `Client §3` 全字段条（同 Overview）。
- **Filter Bar**：`Document §6` + 联结 `Attachment §5` 筛选字段。
- **Main Content**：凭证主表；可选批量操作条（`06` §11「批量但可控」— 若 PoC 不做则隐藏）。
- **Side Panel / Drawer**：选中行 → **Document + Attachment + Email** 详情抽屉。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Client Header（壳） | `client_id`, `legal_name`, `trading_name`, `uen`, `email_domains`, `primary_contact_email`, `xero_contact_id`, `xpm_client_id`, `portal_client_id`, `status`, `mapping_confidence` | string / array / enum / number | §3 Client | `xero_contact_id` 等权限内可编辑 | 同 Overview |
| Filter | `period` | string | §6 Document | 否 | 筛选 |
| Filter | `document_type` | enum | §6 Document | 否 | 多选 |
| Filter | `review_status` | enum | §6 Document | 否 | 多选 |
| Filter | `xero_status` | enum | §6 Document | 否 | 多选 |
| Filter | `vendor_name` | string | §6 Document | 否 | 搜索 |
| Filter | `invoice_number` | string | §6 Document | 否 | 搜索 |
| Filter | `confidence_score` | number | §6 Document | 否 | 区间 |
| Filter | `duplicate_candidate` | boolean | §5 Attachment（联结） | 否 | 开关 |
| Filter | `password_protected` | boolean | §5 Attachment（联结） | 否 | 开关 |
| Table 行 | `document_id` | string | §6 Document | 否 | 选行 / 开抽屉 |
| Table 行 | `attachment_id` | string | §6 Document | 否 | — |
| Table 行 | `client_id` | string | §6 Document | 否 | — |
| Table 行 | `document_type` | enum | §6 Document | 否 | — |
| Table 行 | `period` | string | §6 Document | 否 | — |
| Table 行 | `vendor_name` | string | §6 Document | 否 | — |
| Table 行 | `invoice_number` | string | §6 Document | 否 | — |
| Table 行 | `invoice_date` | date | §6 Document | 否 | — |
| Table 行 | `currency` | string | §6 Document | 否 | — |
| Table 行 | `total_amount` | number | §6 Document | 否 | — |
| Table 行 | `gst_rate` | string | §6 Document | 否 | — |
| Table 行 | `account_code` | string | §6 Document | 否 | — |
| Table 行 | `confidence_score` | number | §6 Document | 否 | 排序 |
| Table 行 | `review_status` | enum | §6 Document | 否 | — |
| Table 行 | `xero_status` | enum | §6 Document | 否 | — |
| Table 行 | `filename` | string | §5 Attachment | 否 | — |
| Table 行 | `hash` | string | §5 Attachment | 否 | — |
| Table 行 | `mime_type` | string | §5 Attachment | 否 | — |
| Table 行 | `size_bytes` | integer | §5 Attachment | 否 | — |
| Table 行 | `duplicate_candidate` | boolean | §5 Attachment | 否 | 标签 |
| Table 行 | `password_protected` | boolean | §5 Attachment | 否 | 标签 |
| Table 行 | `subject`, `received_at` | string, datetime | §4 Email（联结） | 否 | — |
| Drawer — Document | `document_id` … `source_evidence` | 同 §6 全表各类型 | §6 Document | `period`,`document_type`,`vendor_name`,`invoice_number`,`invoice_date`,`currency`,`total_amount`,`gst_rate`,`account_code` 可编辑；`confidence_score` 只读；`review_status`/`xero_status` 由动作驱动 | 保存、跳转 Review |
| Drawer — Attachment | `attachment_id`,`email_id`,`filename`,`file_extension`,`mime_type`,`size_bytes`,`hash`,`storage_uri`,`password_protected`,`duplicate_candidate` | §5 全表 | §5 Attachment | 一般不直接改元数据 | 预览 / 下载 |
| Drawer — Email 摘要 | `message_id`,`thread_id`,`sender_email`,`subject`,`received_at` | string, datetime | §4 Email | 否 | 跳转 **Emails** Tab |

### 4. 表格 / 列表

- **columns**：`document_id`, `document_type`, `period`, `vendor_name`, `invoice_number`, `invoice_date`, `currency`, `total_amount`, `confidence_score`, `review_status`, `xero_status`, `filename`, `hash`, `duplicate_candidate`, `password_protected`, `received_at`, `subject`。
- **row actions**：打开 **Drawer**；跳转 **Document Review / OCR**；跳转 **Document Classification**；跳转 **Exceptions**（`review_status=exception` 或附件异常）；跳转 **Email Inbox**（`message_id` query）。

### 5. 状态

- **loading**：表、抽屉、保存请求。
- **empty**：当前 `client_id` + 筛选下无 Document。
- **error**：列表/抽屉/保存 API 失败 + 重试（PRD NFR）。
- **success**：表排序、抽屉、保存成功反馈。

### 6. 交互流程

- **点击**：行 → 抽屉或直达 **Document Review**。
- **编辑**：抽屉内 **Document** 可编辑字段保存（R-OCR-02）。
- **跳转**：→ **Review**；→ **Classification**；→ **Exceptions**；→ **Emails**；→ **Voucher Board**（若独立路由）。
- **触发模块**：**M1\***（审阅数据准备）；**DocumentAgent / ReviewAgent / XeroAgent**（`07_AI_Agent_Workflow.md`）经保存与跳转触发。

### 7. 边界情况

- **数据缺失**：§6 Conditional 字段空 → 标缺失 + 引导 Review（`10_Decision_Rules_and_Human_Gates.md` §6）。
- **OCR 失败**：与 §8 `missing_reason=ocr_failed` 并列提示（无 Document→Missing 外键，仅 UI 提示）。
- **API 失败**：见 **error**。
- **重复数据**：`duplicate_candidate` + `hash` + `invoice_number`+`total_amount`（`05` F2/F4）。

### 8. 页面跳转关系

- **来源**：**Month-End Overview**；**Dashboard**；**Email Inbox**；**Review Tasks**。
- **去向**：**Document Review**；**Document Classification**；**Exceptions**；**Emails** Tab；**Email Inbox**。

---

## Page: Month-End Workspace › Emails

**路由**：一级 `Month-End Workspace` + 二级 Tab **Emails**  
**对齐**：`06_Wireframe_Design_Spec.md` §4 Tab「Emails」；`05_Feature_Breakdown.md` F2；`07_AI_Agent_Workflow.md` §4 EmailAgent。

### 1. 页面目标

- **用户**：Staff、Senior（`01_PRD.md` §4）。
- **解决**：单客户邮件时间线、thread 上下文、附件列表与客户匹配人工覆盖（`05` F2 Manual override）。
- **对应模块**：**M8**；支撑 **F10** 证据链（PRD R-AUDIT-01）。

### 2. 页面结构

- **Header**：Workspace 壳 — `Client §3`。
- **Filter Bar**：`Email §4` 筛选字段。
- **Main Content**：邮件列表；展开行展示 **Attachment 子表**（§5，经 `email_id`）。
- **Side Panel / Drawer**：单封邮件 **Email §4 全字段** + 附件全字段列表。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Client Header（壳） | 同 Documents 页 §3 全表 | 同 §3 | §3 Client | 同 Documents | 同 Documents |
| Filter | `mailbox_id` | string | §4 Email | 否 | 筛选 |
| Filter | `sender_email` | string | §4 Email | 否 | 筛选 |
| Filter | `subject` | string | §4 Email | 否 | 搜索 |
| Filter | `received_at` | datetime | §4 Email | 否 | 范围 |
| Filter | `direction` | enum | §4 Email | 否 | 筛选 |
| Filter | `email_intent` | enum | §4 Email | 否 | 筛选 |
| Filter | `processing_status` | enum | §4 Email | 否 | 筛选 |
| List 行 — Email | `email_id` | string | §4 Email | 否 | 展开 / 开抽屉 |
| List 行 | `message_id`, `thread_id` | string | §4 Email | 否 | 复制 |
| List 行 | `mailbox_id` | string | §4 Email | 否 | — |
| List 行 | `client_id` | string | §4 Email | **是**（F2 override） | 保存更正 |
| List 行 | `sender_email`, `subject` | string | §4 Email | 否 | — |
| List 行 | `body_text` | text | §4 Email | 否 | Drawer 展开 |
| List 行 | `received_at` | datetime | §4 Email | 否 | 排序 |
| List 行 | `direction`, `email_intent`, `processing_status` | enum | §4 Email | 否 | 标签 |
| 子表 — Attachment | `attachment_id`,`email_id`,`filename`,`file_extension`,`mime_type`,`size_bytes`,`hash`,`storage_uri`,`password_protected`,`duplicate_candidate` | §5 全表 | §5 Attachment | 否 | 跳转 Classification / Documents |
| Drawer — Email 全量 | `email_id` … `processing_status` | §4 全表 | §4 Email | `client_id` 可编辑 | 保存 override |

### 4. 表格 / 列表

- **columns（主表）**：`received_at`, `sender_email`, `subject`, `direction`, `email_intent`, `processing_status`, `thread_id`, `client_id`。
- **row actions**：展开附件子表；打开 Drawer；**保存 `client_id` 更正**；跳转 **Email Inbox**（`message_id`）；跳转 **Documents**（若已存在 `document_id` 联结）；跳转 **Document Classification**。

### 5. 状态

- **loading**：列表、子表、Drawer、保存。
- **empty**：该 `client_id` 下无邮件（含筛选）。
- **error**：查询 / override 保存失败 + 重试。
- **success**：列表与保存反馈。

### 6. 交互流程

- **点击**：展开行；打开 Drawer。
- **编辑**：**`Email.client_id`**（Manual override，`05` F2）。
- **跳转**：→ **Email Inbox**；→ **Document Classification**；→ **Documents**；→ **Document Review**。
- **触发模块**：**M8**（EmailAgent）；人工反馈（`07` §10）。

### 7. 边界情况

- **数据缺失**：`body_text`、`client_id` Preferred 空（§4）→ 空态；`processing_status` 枚举未在 09 展开 → 展示 raw + 待 FDE。
- **OCR 失败**：本页主数据为 Email；若子表已挂 Document 可展示 `review_status`（§6）— 可选列。
- **API 失败**：见 **error**。
- **重复数据**：`duplicate_candidate`（§5）+ `hash`（`05` F2）。

### 8. 页面跳转关系

- **来源**：**Month-End Overview**；**Dashboard**；**Email Inbox**。
- **去向**：**Email Inbox**；**Document Classification**；**Documents**；**Document Review**；**Chase History**（intent 相关）。

---

## Page: Month-End Workspace › Missing Docs

**路由**：一级 `Month-End Workspace` + 二级 Tab **Missing Docs**  
**对齐**：`06_Wireframe_Design_Spec.md` §4 Tab「Missing Docs」；`06` §8 Missing Document Tracker；`05_Feature_Breakdown.md` F6；PRD R-MISS-01。

### 1. 页面目标

- **用户**：Staff、Senior、Manager、CST/SDT（`01_PRD.md` §4）。
- **解决**：在**当前客户**下查看缺票行、阻塞原因与状态，并发起检索/催票/不适用标记（`06` §8 Summary + Table；`05` F6）。
- **对应模块**：**M9**；**F6**；与 **M1\***（`received_but_not_confirmed` 等与凭证衔接）。

### 2. 页面结构

- **Header**：Workspace 壳 — `Client §3`。
- **Filter Bar**：`Missing §8` 枚举与 `period`。
- **Main Content**：汇总卡（由 `expected_count` / `received_count` / `confirmed_count` 聚合）+ **Missing Document 主表**（仅 `client_id` = 当前客户）。
- **Side Panel / Drawer**：单行 `missing_doc_id` 详情（§8 全字段）。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Client Header（壳） | 同 Documents 页 §3 全表 | 同 §3 | §3 Client | 权限内同前 | 同前 |
| Summary 卡 | `expected_count`, `received_count`, `confirmed_count` | integer | §8 Missing（聚合） | 否 | 只读 |
| Filter | `period` | string | §8 Missing | 否 | 筛选 |
| Filter | `required_doc_type` | enum | §8 Missing | 否 | 筛选 |
| Filter | `missing_reason` | enum | §8 Missing | 否 | 多选 |
| Filter | `blocker_level` | enum | §8 Missing | 否 | 多选 |
| Filter | `status` | enum | §8 Missing | 否 | 多选 |
| Table 行 | `missing_doc_id` | string | §8 Missing | 否 | 打开 Drawer |
| Table 行 | `client_id` | string | §8 Missing | 否 | 校验 = 当前客户 |
| Table 行 | `period` | string | §8 Missing | 否 | — |
| Table 行 | `required_doc_type` | enum | §8 Missing | 否 | — |
| Table 行 | `expected_count` | integer | §8 Missing | 否 | — |
| Table 行 | `received_count` | integer | §8 Missing | 否 | — |
| Table 行 | `confirmed_count` | integer | §8 Missing | 否 | — |
| Table 行 | `missing_reason` | enum | §8 Missing | 否 | — |
| Table 行 | `blocker_level` | enum | §8 Missing | 否 | — |
| Table 行 | `status` | enum | §8 Missing | **是**（流程写回） | 行内或 Drawer 保存 |
| Drawer — 全量 | 上列 §8 全表字段 | 同 §8 | §8 Missing | `status` 等按 F6 可编辑 | 保存 |

**说明**：`05` F6 中的 `missing_count`、`next_action` **不在 `09` §8** → 不作为 Data Mapping 字段列入；若 UI 需要，标 **待数据字典** 或派生展示。

### 4. 表格 / 列表

- **columns**：`missing_doc_id`, `period`, `required_doc_type`, `expected_count`, `received_count`, `confirmed_count`, `missing_reason`, `blocker_level`, `status`。
- **row actions**：**Search history** → **Historical Email Search Results**（query：`client_id`,`period`,`required_doc_type`）；**Generate chase email** → **Chase Email Composer**；**Mark not applicable** → 更新 `status = not_applicable`（§8 枚举）；**Assign owner** → **非 09 字段**，不写入本表定义。

### 5. 状态

- **loading**：汇总、表、Drawer、保存。
- **empty**：当前客户 + 筛选下无 Missing 行。
- **error**：查询/保存失败 + 重试。
- **success**：表与 Drawer 可用。

### 6. 交互流程

- **点击**：行 → Drawer。
- **编辑**：**`Missing.status`**（及流程允许的其他 §8 字段写回）。
- **跳转**：→ **Historical Search Results**；→ **Chase Composer**；→ **Missing Documents**（一级，同筛选）；→ **Document Review**（`missing_reason` 与待确认凭证相关时）。
- **触发模块**：**M9**（SearchAgent / ChaseAgent，`07` §8–9）；Orchestrator `missing_doc_detected`（`07` §3）。

### 7. 边界情况

- **数据缺失**：`expected_count` Preferred 空（§8）→ 不展示比率类文案。
- **OCR 失败**：`missing_reason = ocr_failed`（§8）高亮。
- **API 失败**：见 **error**。
- **重复数据**：缺票行不按发票重复建模；重复凭证见 **Documents** + §5。

### 8. 页面跳转关系

- **来源**：**Month-End Overview**；**Dashboard**；**Missing Documents** 一级。
- **去向**：**Historical Email Search Results**；**Chase Email Composer**；**Document Review**；**Documents**；**Missing Documents**（一级）。

---

## Page: Month-End Workspace › Chase History

**路由**：一级 `Month-End Workspace` + 二级 Tab **Chase History**  
**对齐**：`06_Wireframe_Design_Spec.md` §4 Tab「Chase History」；`05_Feature_Breakdown.md` F8（Reply tracking）；`07_AI_Agent_Workflow.md` §8–9。

### 1. 页面目标

- **用户**：Staff、Senior、Manager（`01_PRD.md` §4）。
- **解决**：单客户维度查看催票发送、客户回复与相关邮件事实，支撑跟进与审计（`05` F8；PRD R-CHASE-01、R-AUDIT-01）。
- **对应模块**：**M2\***（邮件催票语义）；**M9**；**F8**。

### 2. 页面结构

- **Header**：Workspace 壳 — `Client §3`。
- **Filter Bar**：`Email.received_at` 范围；`email_intent`；`sender_email`；`subject`（均 §4）。
- **Main Content**：**合并时间线** —（A）`§9` KPI 事件行；（B）`§4` Email 行；按时间排序（时间列规则见 §3 说明）。
- **Side Panel / Drawer**：选中 **Email** 或 KPI 聚合行的详情。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Client Header（壳） | 同 §3 Client 全表 | 同 §3 | §3 Client | 权限内同前 | 同前 |
| Filter | `received_at` | datetime | §4 Email | 否 | 范围 |
| Filter | `email_intent` | enum | §4 Email | 否 | 多选 |
| Filter | `sender_email`, `subject` | string | §4 Email | 否 | 搜索 |
| 时间线 — KPI chase_sent | `chase_level`, `recipient` | string | §9 Key Fields | 否 | 跳转 **Chase Composer** |
| 时间线 — KPI client_replied | `response_type`, `duration` | string, number | §9 Key Fields | 否 | — |
| 时间线 — KPI search_completed | `result_type`, `candidate_count` | string, number | §9 Key Fields | 否 | 跳转 **Historical Search Results** |
| 时间线 — KPI missing_doc_detected | `missing_doc_id`, `period` | string, string | §9 Key Fields | 否 | 跳转 **Missing Docs** |
| 时间线 — Email 行 | `email_id`,`message_id`,`thread_id`,`mailbox_id`,`client_id`,`sender_email`,`subject`,`body_text`,`received_at`,`direction`,`email_intent`,`processing_status` | §4 各类型 | §4 Email | `client_id` 可编辑（F2） | Drawer；override |

**说明**：`09` **无 ChaseEmail 字段表**（仅 §2 实体名）；本页 **不发明** chase_id、template_id。绝对事件时间：§9 除 `email_captured` 的 `timestamp` 外 **未逐事件列 datetime** → 实现层挂载事件记录时间标 **待数据字典**；UI 可用 `Email.received_at` 与 `duration` 展示组合。

### 4. 表格 / 列表

- **columns（虚拟合并表）**：`sort_key`（实现派生，**非 09 字段名** → 列标题可用「时间」）；`row_kind`（enum：kpi \| email，**UI-only**）；对 **kpi** 行展示 §9 该事件 Key Fields；对 **email** 行展示 `received_at`, `sender_email`, `subject`, `email_intent`, `processing_status`。
- **row actions**：打开 Drawer；跳转 **Chase Composer**；跳转 **Historical Search Results**；跳转 **Missing Docs**；**保存 Email.client_id**。

### 5. 状态

- **loading**：时间线。
- **empty**：无 KPI 事件且无满足筛选的 §4 邮件。
- **error**：聚合失败 + 重试。
- **success**：时间线可浏览、可跳转。

### 6. 交互流程

- **点击**：打开 Drawer；按行类型跳转目标页。
- **编辑**：**`Email.client_id`**（override）。
- **跳转**：→ **Chase Composer**；→ **Historical Search Results**；→ **Missing Docs**；→ **Emails**（同 Tab 刷新）。
- **触发模块**：**ChaseAgent**、**SearchAgent**（`07` §8–9）；**EmailAgent**（`07` §4）。

### 7. 边界情况

- **数据缺失**：仅 KPI 无 Email 或反之 → 分块 empty。
- **OCR 失败**：非主路径；经 `missing_doc_id` → **Missing Docs**。
- **API 失败**：见 **error**。
- **重复数据**：同 `thread_id` 多封邮件 → UI 折叠（行为层，不新增 09 字段）。

### 8. 页面跳转关系

- **来源**：**Month-End Overview**；**Chase Composer** 发送后返回；**Emails** Tab。
- **去向**：**Chase Email Composer**；**Historical Email Search Results**；**Missing Docs**；**Emails**。

---

## Page: Month-End Workspace › Audit Trail

**路由**：一级 `Month-End Workspace` + 二级 Tab **Audit Trail**  
**对齐**：`06_Wireframe_Design_Spec.md` §4 Tab「Audit Trail」；`05_Feature_Breakdown.md` F10；PRD R-AUDIT-01。

### 1. 页面目标

- **用户**：Staff、Senior、Manager、FDE（`01_PRD.md` §4；审计需求）。
- **解决**：在**当前客户**下追溯邮件捕获、分类、OCR、审核、Xero、缺票、检索、催票、回复等事件与凭证 **`source_evidence`**（`09` §6、§9）。
- **对应模块**：**F10**；支撑 **M8/M9/M1\*** 证据链；不替代合规存档系统边界（PRD 核心边界）。

### 2. 页面结构

- **Header**：Workspace 壳 — `Client §3`。
- **Filter Bar**：时间范围（`Email.received_at` / KPI 行展示时间 — 见 §3 说明）；事件类型（**UI 枚举**，取值自 `09` §9 **Event** 列名，**非新增库字段**）；可选 `document_id`（§6）聚焦单证。
- **Main Content**：**Block A — KPI 事件表**（§9 全事件类型 + 各 Key Fields）；**Block B — Document 证据摘要表**（§6 含 `source_evidence`）。
- **Side Panel / Drawer**：选中 KPI 行或 Document 行 → 展开 Key Fields 全文 / `source_evidence` 数组项只读展示。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Client Header（壳） | 同 §3 Client 全表 | 同 §3 | §3 Client | 权限内同前 | 同前 |
| Filter | `received_at` | datetime | §4 Email（辅助时间轴下界） | 否 | 范围 |
| Filter | `document_id` | string | §6 Document | 否 | 可选聚焦 |
| Block A — 事件名 | （UI 展示 `09` §9 Event 列：email_captured 等） | string（只读标签） | §9 KPI Event | 否 | 多选筛选 |
| Block A — email_captured | `client_id`, `message_id`, `timestamp` | string, string, datetime | §9 Key Fields | 否 | 跳转 **Emails** |
| Block A — attachment_classified | `doc_type`, `confidence` | string, number | §9 Key Fields | 否 | 跳转 **Documents** / **Classification** |
| Block A — ocr_completed | `duration`, `confidence` | number, number | §9 Key Fields | 否 | 跳转 **Document Review** |
| Block A — review_completed | `reviewer`, `duration`, `changes_count` | string, number, number | §9 Key Fields | 否 | 跳转 **Document Review** |
| Block A — xero_draft_created | `xero_id`, `success` | string, boolean | §9 Key Fields | 否 | 跳转 **Document Review** / **Exceptions** |
| Block A — missing_doc_detected | `missing_doc_id`, `period` | string, string | §9 Key Fields | 否 | 跳转 **Missing Docs** |
| Block A — search_completed | `result_type`, `candidate_count` | string, number | §9 Key Fields | 否 | 跳转 **Historical Search Results** |
| Block A — chase_sent | `chase_level`, `recipient` | string, string | §9 Key Fields | 否 | 跳转 **Chase Composer** |
| Block A — client_replied | `response_type`, `duration` | string, number | §9 Key Fields | 否 | 跳转 **Chase History** |
| Block B — Document | `document_id`, `attachment_id`, `client_id`, `document_type`, `period`, `review_status`, `xero_status`, `source_evidence` | string / enum / array | §6 Document | **否**（审计只读） | 跳转 **Document Review** |
| Drawer | 选中行的 §9 Key Fields 全集或 §6 `source_evidence` 展开 | 同 §9 / §6 | §9；§6 | 否 | 复制 / 导出（若产品支持，**非 09**） |

**说明**：§9 各事件 **未统一列 `client_id`**；本 Tab 限定 **当前 Workspace 客户** 时，实现层按 `message_id` / `document_id` / `missing_doc_id` 等与 §3 `client_id` 联结过滤 — **不新增 Data Mapping 字段**。

### 4. 表格 / 列表

- **Block A columns**：`event`（UI 标签=§9 Event 名）+ 该事件 **Key Fields** 动态列（列集随 `event` 变化，字段名不超出 §9）。
- **Block B columns**：`document_id`, `document_type`, `period`, `review_status`, `xero_status`, `attachment_id`, `source_evidence`（折叠/条数）。
- **row actions**：跳转 **Emails**、**Documents**、**Document Review**、**Missing Docs**、**Historical Search Results**、**Chase Composer**、**Exceptions**。

### 5. 状态

- **loading**：Block A / B 独立 loading。
- **empty**：无 §9 事件、无 §6 Document（或均被过滤）。
- **error**：查询失败 + 重试。
- **success**：双块只读展示完整。

### 6. 交互流程

- **点击**：打开 Drawer；跳转证据上下游页面。
- **编辑**：**本页不编辑**业务数据（F10 只读审计视图）。
- **跳转**：见 row actions。
- **触发模块**：无写操作；展示 **AuditAgent / Orchestrator** 产出与持久化结果（`07_AI_Agent_Workflow.md` §2）。

### 7. 边界情况

- **数据缺失**：某事件 Key Field 在存储中缺失 → 空单元格；`source_evidence` 空数组（§6）→ 提示 R-AUDIT-01 门槛（`10_Decision_Rules_and_Human_Gates.md` §2 证据优先 — 展示为警告链至补录页，**不新增字段**）。
- **OCR 失败**：经 `missing_reason` / Missing 跳转，不在此页改数据。
- **API 失败**：见 **error**。
- **重复数据**：同 `message_id` / `document_id` 多事件 → 全量展示不合并（或 UI 折叠，**不新增 09 字段**）。

### 8. 页面跳转关系

- **来源**：**Month-End** 各 Tab；**Document Review**「查看审计」。
- **去向**：**Emails**；**Documents**；**Document Review**；**Missing Docs**；**Historical Search Results**；**Chase Composer**；**Exceptions**。

---

## Page: Email Inbox

**路由**：一级 **Email Inbox**（Intake Queue）  
**对齐**：`06_Wireframe_Design_Spec.md` §5 页面 3；`05_Feature_Breakdown.md` F2；PRD R-EMAIL-01、R-EMAIL-02。

### 1. 页面目标

- **用户**：Junior Staff / Accountant（`01_PRD.md` §4）。
- **解决**：跨客户查看邮件与附件捕获状态、thread、客户匹配与重复风险，进入分类或 OCR 链路（`06` §5；`05` F2）。
- **对应模块**：**M8**；**F2**；**F3** 入口。

### 2. 页面结构

- **Header**：产品上下文、试点范围提示（PRD NFR 最小权限 — **无 09 字段**，文案层）。
- **Filter Bar**：日期 / 客户 / 类型 / 置信度 / 状态 / 异常（映射见 §3）。
- **Main Content**：**邮件分组卡片列表**（`06` §5「Email Group Card」）；每卡内 **附件子列表**。
- **Side Panel / Drawer**：单邮件 + 全附件 + 已存在 **Document** 摘要（联结）。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter — 日期 | `received_at` | datetime | §4 Email | 否 | 范围 |
| Filter — 客户 | `client_id`；展示 `legal_name`,`trading_name` | string | §4 Email；§3 Client | `client_id` 可编辑（override） | 筛选 / 更正 |
| Filter — 类型 | `document_type` | enum | §6 Document（联结附件） | 否 | 筛选（无 Document 前行可能无值 → empty 筛选项） |
| Filter — 置信度 | `confidence_score` | number | §6 Document（联结） | 否 | 区间 |
| Filter — 状态 | `review_status`, `xero_status` | enum | §6 Document（联结） | 否 | 多选 |
| Filter — 异常 | `password_protected`, `duplicate_candidate` | boolean | §5 Attachment | 否 | 开关 |
| Card — Email | `email_id`,`message_id`,`thread_id`,`mailbox_id`,`client_id`,`sender_email`,`subject`,`body_text`,`received_at`,`direction`,`email_intent`,`processing_status` | §4 各类型 | §4 Email | `client_id` 可编辑 | 展开卡 / Drawer |
| Card — 展示客户 | `legal_name`,`trading_name`,`mapping_confidence` | string, number | §3 Client（联结 `Email.client_id`） | 否 | — |
| 子行 — Attachment | `attachment_id`,`email_id`,`filename`,`file_extension`,`mime_type`,`size_bytes`,`hash`,`storage_uri`,`password_protected`,`duplicate_candidate` | §5 全表 | §5 Attachment | 否 | 预览 |
| 子行 — Document（若已存在） | `document_id`,`document_type`,`confidence_score`,`review_status`,`xero_status` | §6 | §6 Document | 否 | 跳转 **Document Review** |
| Drawer | Email §4 全表 + Attachment §5 列表 + 联结 Document §6 摘要 | 同上 | §4；§5；§6 | `client_id` 可编辑 | 保存 override |

**说明**：`06`「predicted document type / predicted invoice」在附件**尚未**写入 §6 前 **无 `09` 字段** → 仅在有 `Document` 时显示 `document_type`；否则 UI 标「待分类」**不写映射列**。

### 4. 表格 / 列表

- **Card 主行（每邮件）**：`sender_email`, `subject`, `received_at`, `thread_id`, `client_id`, `legal_name`, `processing_status`。
- **附件子表 columns**：`filename`, `mime_type`, `size_bytes`, `hash`, `password_protected`, `duplicate_candidate`, `document_type`, `confidence_score`, `review_status`（后三列依赖 §6 联结，无则空）。
- **row actions**：**Review classification** → **Document Classification**；**Send to OCR** → **Document Review** / 触发 DocumentAgent 流程（`07` §5，产品按钮）；**Mark irrelevant** → 写回 `Document.document_type = irrelevant` 或新建 Document（**实现策略须一致**，字段仍只用 §6 枚举）；跳转 **Month-End › Emails**（带 `client_id`）。

### 5. 状态

- **loading**：卡列表、Drawer。
- **empty**：筛选下无邮件。
- **error**：同步/读取失败 + 重试（PRD NFR；`13_Risk_Dependency_Log.md` R-01）。
- **success**：卡与附件操作可用。

### 6. 交互流程

- **点击**：展开卡；打开 Drawer。
- **编辑**：**`Email.client_id`**（F2 Manual override）。
- **跳转**：→ **Document Classification**；→ **Document Review**；→ **Exceptions**；→ **Month-End Workspace**。
- **触发模块**：**M8**（EmailAgent）；**DocumentAgent**（送 OCR，`07` §5）。

### 7. 边界情况

- **数据缺失**：`client_id` Preferred 空 → 强制匹配提示（`10` §4）；`storage_uri` Preferred 空 → 无法预览。
- **OCR 失败**：已有关联 Document 时展示 `review_status` / 跳转 Review；无 Document 则仅提示走 Classification。
- **API 失败**：见 **error**。
- **重复数据**：`duplicate_candidate` + `hash`（`05` F2）。

### 8. 页面跳转关系

- **来源**：**Dashboard**；全局 **Email Inbox**；**Month-End › Emails**。
- **去向**：**Document Classification**；**Document Review**；**Exceptions**；**Month-End Workspace**（Emails / Documents）。

---

## Page: Document Classification

**路由**：一级 **Document Classification**  
**对齐**：`06_Wireframe_Design_Spec.md` §6 页面 4；`05_Feature_Breakdown.md` F3；`07_AI_Agent_Workflow.md` §5 DocumentAgent。

### 1. 页面目标

- **用户**：Junior Staff / Accountant（`01_PRD.md` §4）。
- **解决**：对照附件原文确认或修正 **客户**、**文档类型**、**期间/供应商** 等，再送入 OCR（`06` §6；`05` F3）。
- **对应模块**：**M8**；**F3**；衔接 **M1\***（生成/更新 §6 Document 后进入审阅）。

### 2. 页面结构

- **Header**：面包屑（`Email Inbox` → 本页）；当前 `attachment_id` / `email_id`（§5 / §4）。
- **Filter Bar**：无全局列表时可为空；若从队列进入则 **单附件上下文**，可隐藏 Filter。
- **Main Content**：**左** 文件预览区；**右** 分类字段与置信展示（`06` §6）。
- **Side Panel / Drawer**：可选 **Email §4** 摘要条（同 thread 上下文）。
- **Footer**：操作条（`06` §6 Actions）— Confirm / Change client / Change type / Duplicate / Non-accounting。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Preview — Attachment | `storage_uri`, `filename`, `mime_type`, `size_bytes`, `hash` | string / integer | §5 Attachment | 否 | 缩放、翻页（`05` F4 预览能力） |
| Preview — 加密 | `password_protected` | boolean | §5 Attachment | 否 | 阻断送 OCR → 跳转 **Exceptions**（`05` §4） |
| 右栏 — Email 上下文 | `sender_email`, `subject`, `received_at`, `thread_id`, `message_id` | string, datetime | §4 Email | 否 | 只读 |
| 右栏 — 选中客户 | `client_id`, `legal_name`, `trading_name`, `mapping_confidence` | string, number | §3 Client（当前候选） | **`client_id` 可编辑**（确认归属） | Change client |
| 右栏 — Document（新建或已有） | `document_id`, `attachment_id`, `client_id`, `document_type`, `period`, `vendor_name`, `invoice_number`, `invoice_date`, `currency`, `total_amount`, `gst_rate`, `account_code`, `confidence_score`, `review_status`, `xero_status`, `source_evidence` | §6 各类型 | §6 Document（无则创建后写入同字段集） | `document_type`,`period`,`vendor_name` 等分类阶段可编辑；`confidence_score` 来自 Agent 时只读 | 保存草稿 |
| 右栏 — 重复提示 | `duplicate_candidate`, `hash` | boolean, string | §5 Attachment | 否 | Mark duplicate（流程：见 §6 交互） |

**说明**：`06`「Predicted … confidence 82%」若 **无** Agent 分项分数写入 §6，则 **仅展示 `Document.confidence_score`**（§6）；不发明 `field_confidence_*` 列。

### 4. 表格 / 列表

- 单附件模式：**无主表**；若产品为「队列列表 + 右侧详情」则列表列：`attachment_id`, `filename`, `received_at`, `sender_email`, `client_id`, `document_type`, `confidence_score`（§5+§4+§6 联结）。
- **row actions**（队列模式）：选中一行加载左右栏；跳转 **Email Inbox**。

### 5. 状态

- **loading**：预览、右栏、保存、送 OCR。
- **empty**：无 `attachment_id` 路由参数且队列为空。
- **error**：预览加载失败、保存失败、OCR API 失败（`10` §2 异常不沉默）。
- **success**：保存成功、送 OCR 已排队。

### 6. 交互流程

- **点击**：预览区交互；按钮区。
- **编辑**：**`client_id`**, **`document_type`**, **`period`**, **`vendor_name`** 等 §6 可编辑字段；**Confirm and send to OCR** → 更新/创建 §6 并触发 **DocumentAgent**（`07` §5）；**Mark as duplicate** → 依赖 `duplicate_candidate`/`hash` 人工结案或写 `review_status`（§6 枚举策略与产品一致）；**Mark non-accounting** → `document_type = irrelevant`（§6 枚举）。
- **跳转**：→ **Document Review**；→ **Exceptions**；→ **Email Inbox**。
- **触发模块**：**M8**；**DocumentAgent**（分类与送 OCR）。

### 7. 边界情况

- **数据缺失**：`vendor_name` Preferred 空；`period` Preferred 空 → 允许保存但提示后续 Review（`10` §5）。
- **OCR 失败**：送 OCR 后失败 → **Exception** 分支（`07` §3），跳转 **Exceptions**。
- **API 失败**：见 **error**。
- **重复数据**：`duplicate_candidate`（§5）+ `hash` + 后续 `invoice_number`/`total_amount`（§6，若已 OCR）— `05` F2/F4。

### 8. 页面跳转关系

- **来源**：**Email Inbox**；**Month-End › Emails**；**Documents**。
- **去向**：**Document Review**；**Exceptions**；**Email Inbox**；**Review Tasks**。

---

## Page: Review Tasks

**路由**：一级 **Review Tasks**（待审队列）  
**对齐**：`06_Wireframe_Design_Spec.md` §2 IA「Review Tasks」；`05_Feature_Breakdown.md` F4；`07_AI_Agent_Workflow.md` §6 ReviewAgent。

### 1. 页面目标

- **用户**：Staff、Senior（`01_PRD.md` §4）。
- **解决**：跨客户集中处理 **待 Staff / 待 Senior / 异常** 凭证队列，快速进入单证 OCR 页（`05` F4；`10` §3 置信度阈值）。
- **对应模块**：**M1\***；**F4**；衔接 **F5**。

### 2. 页面结构

- **Header**：队列标题、当前筛选摘要。
- **Filter Bar**：`client_id`（§3/§6）；`period`；`document_type`；`review_status`；`confidence_score` 区间；`xero_status`；联结 `duplicate_candidate`（§5）。
- **Main Content**：**Document 任务表**（仅 `review_status` ∈ `pending_staff_review` \| `pending_senior_review` \| `exception`）。
- **Side Panel / Drawer**：可选行摘要（同 **Documents** Tab 抽屉字段子集）。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter | `client_id` | string | §6 Document；§3 Client 展示名 | 否 | 筛选 |
| Filter | `period` | string | §6 Document | 否 | 筛选 |
| Filter | `document_type` | enum | §6 Document | 否 | 多选 |
| Filter | `review_status` | enum | §6 Document | 否 | 固定子集或全选 |
| Filter | `confidence_score` | number | §6 Document | 否 | 区间 |
| Filter | `xero_status` | enum | §6 Document | 否 | 多选 |
| Filter | `duplicate_candidate` | boolean | §5 Attachment（联结） | 否 | 开关 |
| Table 行 | `document_id`, `attachment_id`, `client_id` | string | §6 Document | 否 | 打开 **Document Review** |
| Table 行 | `document_type`, `period`, `vendor_name`, `invoice_number`, `invoice_date`, `currency`, `total_amount` | §6 各类型 | §6 Document | 否 | — |
| Table 行 | `confidence_score`, `review_status`, `xero_status` | number, enum, enum | §6 Document | 否 | — |
| Table 行 | `filename`, `hash` | string | §5 Attachment（联结） | 否 | — |
| Table 行 | `legal_name` | string | §3 Client（联结） | 否 | — |
| Drawer（可选） | 同 **Month-End › Documents** 抽屉 §6+§5+§4 摘要 | 同前 | §6；§5；§4 | 否或同 Documents 策略 | 跳转 **Document Review** |

### 4. 表格 / 列表

- **columns**：`document_id`, `legal_name`, `client_id`, `document_type`, `period`, `vendor_name`, `invoice_number`, `total_amount`, `currency`, `confidence_score`, `review_status`, `xero_status`, `filename`, `received_at`（`received_at` 来自 §4 Email 联结）。
- **row actions**：打开 **Document Review / OCR**；打开 **Document Classification**（类型不明回退）；打开 **Exceptions**；打开 **Month-End › Documents**（带 `client_id`）。

### 5. 状态

- **loading**：表、Drawer。
- **empty**：无待审行（「队列已清空」）。
- **error**：查询失败 + 重试。
- **success**：表可排序、可跳转。

### 6. 交互流程

- **点击**：行 → **Document Review**（主路径）。
- **编辑**：本页 **以跳转后编辑为主**；若 Drawer 开启则同 Documents 抽屉策略。
- **跳转**：见 row actions。
- **触发模块**：**M1\***；**ReviewAgent**（任务分级，`07` §6）。

### 7. 边界情况

- **数据缺失**：§6 Conditional 字段空 → 行内标「缺字段」；`received_at` 联结失败 → 列空。
- **OCR 失败**：`review_status=exception` 或 Missing `ocr_failed` 联动展示（经 `client_id` 查 §8，**不增 FK**）。
- **API 失败**：见 **error**。
- **重复数据**：`duplicate_candidate`（§5）高亮。

### 8. 页面跳转关系

- **来源**：**Dashboard**；**Email Inbox**；**Month-End › Documents**；**Voucher Board**。
- **去向**：**Document Review**；**Document Classification**；**Exceptions**；**Month-End Workspace**；**Missing Documents**。

---

## Page: Document Review / OCR

**路由**：一级 **Document Review / OCR**（单证详情，常带 `document_id` query）  
**对齐**：`06_Wireframe_Design_Spec.md` §7 页面 5；`05_Feature_Breakdown.md` F4、F5；PRD R-OCR-02、R-XERO-01；`07_AI_Agent_Workflow.md` ReviewAgent、XeroAgent。

### 1. 页面目标

- **用户**：Junior Staff、Senior（`01_PRD.md` §4）。
- **解决**：对照原附件核对/修改 OCR 字段、置信与警告，完成人工闸门并创建 **Xero Draft**（不自动 approve，`01_PRD.md` §5、R-XERO-01）。
- **对应模块**：**M1\***；**F4、F5**；上游 **M8**。

### 2. 页面结构

- **Header**：`Client` 摘要 + `Document` 类型 + 来源邮件 + `confidence_score` + `review_status`（字段均来自 `09` §3–§6、§4）。
- **Filter Bar**：无（单证页）；若嵌入「上一条/下一条」队列则仅 **UI 导航**，**不增 09 字段**。
- **Main Content**：**左** 预览（`05` F4）；**右** 提取字段区 + 置信/警告区（`05` F4）；**Xero Payload 区**（`05` F5；`09` §7）。
- **Side Panel / Drawer**：可选 **KPI §9** 与本证相关事件只读列表（同 **Audit Trail** Block A 子集）。
- **Footer**：`Save changes` \| `Send to Senior Review` \| `Create Xero Draft` \| `Mark exception`（`06` §7 Bottom；`05` F4 操作区扩展含 F5）。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Header — Client | `legal_name`, `trading_name`, `client_id`, `uen`, `xero_contact_id`, `mapping_confidence` | string, number | §3 Client | `xero_contact_id` 权限内可编辑 | 跳转 **Settings** |
| Header — Document | `document_id`, `document_type`, `confidence_score`, `review_status`, `xero_status` | string, enum, number, enum, enum | §6 Document | `review_status`/`xero_status` 由动作驱动 | — |
| Header — Email | `subject`, `received_at`, `sender_email`, `message_id` | string, datetime | §4 Email | 否 | 跳转 **Email Inbox** |
| Preview — Attachment | `storage_uri`, `filename`, `mime_type`, `password_protected` | string, boolean | §5 Attachment | 否 | 缩放、翻页 |
| 字段区 — Document | `period`, `vendor_name`, `invoice_number`, `invoice_date`, `currency`, `total_amount`, `gst_rate`, `account_code`, `source_evidence` | §6 各类型 | §6 Document | 除 `confidence_score`、只读标识外可编辑 | Save |
| 字段区 — 只读 | `document_id`, `attachment_id`, `client_id`, `confidence_score` | string, number | §6 Document | 否 | 复制 |
| 警告区（逻辑） | 引用 `05` F4：missing amount、date mismatch、duplicate invoice、GST uncertain | — | 规则输出；**不新增 09 列名** | 否 | 跳转对应字段 |
| Xero Payload — 映射 | `client_id` / `xero_contact_id` | string | §7 Xero Mapping；§3 `xero_contact_id` | `xero_contact_id` 可编辑 | Mapping review（`05` F5） |
| Xero Payload | `invoice_number`, `invoice_date`, `due_date`, `currency` | string, date | §7 | 可编辑 | 与 §6 同步或独立以产品为准 |
| Xero Payload | `line_items.description`, `account_code`, `total_amount`, `unit_amount`, `gst_rate`, `tax_type` | string, number | §7 | 可编辑 | 行编辑 |
| Xero Payload | `source_attachment`, `status` | reference, enum | §7；`status=DRAFT` | `status` 只读 DRAFT | — |
| Footer 动作 | （无独立字段） | — | — | — | 见 §6 |

**说明**：`05` F4「field confidence」**无 `09` 单列** → 不写入上表；可与 **警告区** 合并展示。

### 4. 表格 / 列表

- **Line items 子表**（若结构化）：列来自 §7 `line_items.description`, `account_code`, `unit_amount` / `total_amount`, `tax_type` / `gst_rate`。
- **row actions**（行内）：删除/新增行若产品支持 — **须保持写入 §7 语义**，**不新增 09 字段名**。

### 5. 状态

- **loading**：预览、字段、Xero 提交、`xero_status=drafting` 遮罩。
- **empty**：无效 `document_id` → 404 式空态。
- **error**：预览失败、保存失败、`xero_status=write_failed`（§6）+ Retry（`05` F5）。
- **success**：保存成功、`xero_status=drafted`。

### 6. 交互流程

- **点击**：预览、行编辑、打开 Side KPI。
- **编辑**：§6、§7 可编辑字段；**Save**；**Send to Senior Review** → `review_status=pending_senior_review`（§6）；**Create Xero Draft** → **XeroAgent**（`07` §7）；**Mark exception** → `review_status=exception` 或 Orchestrator Exception（`07` §3）。
- **跳转**：→ **Exceptions**；→ **Email Inbox**；→ **Audit Trail**。
- **触发模块**：**M1\***；**DocumentAgent**（字段修正反馈 `07` §10）；**ReviewAgent**；**XeroAgent**。

### 7. 边界情况

- **数据缺失**：§6 Conditional 空 → 禁用 Create Draft（`10` §7 Xero Write Rules）；`source_evidence` 空 → 不满足证据门槛（`10` §2）。
- **OCR 失败**：异常分支 + Retry（`07` §3）。
- **API 失败**：Xero API error → `write_failed` + Retry（`05` F5）。
- **重复数据**：警告区 duplicate invoice + §5 `duplicate_candidate`。

### 8. 页面跳转关系

- **来源**：**Review Tasks**；**Voucher Board**；**Documents**；**Email Inbox**；**Classification**。
- **去向**：**Exceptions**；**Audit Trail**；**Email Inbox**；**Review Tasks**（下一条）。

---

## Page: Voucher Board

**路由**：一级 **Voucher Board**（产品命名；`06` 无此英文名，见 `ui_design_spec.md` Page List 说明）  
**对齐**：与 **Month-End › Documents** 同构、**跨客户**全量/试点范围凭证表；`05` F4/F5 入口；PRD R-DASH-01 钻取需求。

### 1. 页面目标

- **用户**：Staff、Senior、Manager（`01_PRD.md` §4）。
- **解决**：不进入单客户 Workspace 亦可浏览、筛选全量凭证并进入审阅/Xero（与 **Review Tasks** 互补：本页 **不限** `review_status` 子集，除非用户筛选）。
- **对应模块**：**M1\***；**M3\***（总览钻取）；**M8** 上游证据联结。

### 2. 页面结构

- **Header**：页面标题；试点范围提示（PRD NFR — **无 09 字段**）。
- **Filter Bar**：`client_id`（可选，§6）；`period`；`document_type`；`review_status`；`xero_status`；`vendor_name`；`invoice_number`；`confidence_score`；联结 `duplicate_candidate`, `password_protected`（§5）；`sender_email`, `subject`, `received_at`（§4，联结）。
- **Main Content**：**Document 主表**（全客户或试点白名单，由权限与 F11 配置决定 — **配置本身非 09**）。
- **Side Panel / Drawer**：与 **Month-End › Documents** 抽屉 **同字段集**（§6+§5+§4 摘要）。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter | `client_id` | string | §6 Document；§3 `legal_name` 展示 | 否 | 可选筛选 |
| Filter | `period`, `document_type`, `review_status`, `xero_status`, `vendor_name`, `invoice_number`, `confidence_score` | §6 各类型 | §6 Document | 否 | 同 Documents |
| Filter | `duplicate_candidate`, `password_protected` | boolean | §5 Attachment（联结） | 否 | 同 Documents |
| Filter | `sender_email`, `subject`, `received_at` | string, datetime | §4 Email（联结） | 否 | 同 Documents |
| Table 行 | `document_id`, `attachment_id`, `client_id`, `legal_name`, `trading_name` | string | §6；§3 Client（联结） | 否 | 选行 |
| Table 行 | §6 业务列全集 | 同 §6 | §6 Document | 否 | 同 Documents |
| Table 行 | `filename`, `hash`, `mime_type`, `size_bytes`, `duplicate_candidate`, `password_protected` | §5 | §5 Attachment | 否 | 同 Documents |
| Table 行 | `subject`, `received_at` | string, datetime | §4 Email | 否 | 同 Documents |
| Drawer | 同 **Month-End › Documents** 抽屉定义 | §6+§5+§4 | 同上 | 同 Documents | 同 Documents |

### 4. 表格 / 列表

- **columns**：`document_id`, `client_id`, `legal_name`, `document_type`, `period`, `vendor_name`, `invoice_number`, `invoice_date`, `currency`, `total_amount`, `confidence_score`, `review_status`, `xero_status`, `filename`, `hash`, `duplicate_candidate`, `password_protected`, `received_at`, `subject`。
- **row actions**：打开 Drawer；**Document Review**；**Document Classification**；**Exceptions**；**Month-End Workspace › Documents**（带 `client_id`）；**Email Inbox**。

### 5. 状态

- **loading**：主表、抽屉、保存请求（与 **Month-End › Documents** 同技术路径）。
- **empty**：**全局**（或未选 `client_id` 的试点全集）下无 Document 行 → 文案「当前范围无凭证」；仅筛选过严 → 「无匹配结果」+ 清除筛选。
- **error**：列表/抽屉/保存 API 失败 + 重试（PRD NFR）。
- **success**：表排序、抽屉、保存成功反馈可用。

### 6. 交互流程

- **点击** / **编辑** / **跳转** / **触发模块**：同 **Documents**，区别为 **默认不按 `client_id` 限定**（可选筛选）。

### 7. 边界情况

- **数据缺失** / **OCR 失败** / **API 失败** / **重复数据**：同 **Month-End › Documents**。

### 8. 页面跳转关系

- **来源**：**Dashboard**；**Review Tasks**；全局导航。
- **去向**：**Document Review**；**Document Classification**；**Exceptions**；**Month-End Workspace**；**Email Inbox**；**Missing Documents**（经缺票上下文）。

---

## Page: Missing Documents

**路由**：一级 **Missing Documents**（缺票追踪，**跨客户**）  
**对齐**：`06_Wireframe_Design_Spec.md` §8 页面 6；`05_Feature_Breakdown.md` F6；PRD R-MISS-01；`07_AI_Agent_Workflow.md` §3 Missing 分支。

### 1. 页面目标

- **用户**：Staff、Senior、Manager、CST/SDT（`01_PRD.md` §4）。
- **解决**：跨客户查看缺票、阻塞与下一步，发起历史检索与催票（`06` §8 Summary + Table；`05` F6）。
- **对应模块**：**M9**；**F6**；与 **M1\***（`received_but_not_confirmed` 等）衔接。

### 2. 页面结构

- **Header**：页面标题；试点范围（PRD NFR — **无 09 字段**）。
- **Filter Bar**：`client_id`；`period`；`required_doc_type`；`missing_reason`；`blocker_level`；`status`（均 §8）；联结 §3 `legal_name` 展示。
- **Main Content**：**汇总区**（由 §8 `expected_count` / `received_count` / `confirmed_count` 聚合）；**Missing 主表**。
- **Side Panel / Drawer**：单行 §8 全字段详情。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter | `client_id` | string | §8 Missing；§3 展示名 | 否 | 筛选 |
| Filter | `period` | string | §8 Missing | 否 | 筛选 |
| Filter | `required_doc_type` | enum | §8 Missing | 否 | 筛选 |
| Filter | `missing_reason` | enum | §8 Missing | 否 | 多选 |
| Filter | `blocker_level` | enum | §8 Missing | 否 | 多选 |
| Filter | `status` | enum | §8 Missing | 否 | 多选 |
| Summary | `expected_count`, `received_count`, `confirmed_count` | integer | §8 Missing（聚合） | 否 | 只读 |
| Table 行 | `missing_doc_id`, `client_id`, `period`, `required_doc_type`, `expected_count`, `received_count`, `confirmed_count`, `missing_reason`, `blocker_level`, `status` | §8 各类型 | §8 Missing | `status` 可编辑 | 打开 Drawer |
| Table 行 — 客户展示 | `legal_name`, `trading_name` | string | §3 Client（联结 `client_id`） | 否 | 跳转 **Month-End › Missing Docs** |
| Drawer | §8 全表字段 | 同 §8 | §8 Missing | `status` 等按 F6 可编辑 | 保存 |

**说明**：`06` 表列 **Vendor / Account**、**Days open**、**Evidence**、**Next action**、**Assign owner** — **不在 `09` §8** → 不作为 Data Mapping 字段；若 UI 保留，标 **待数据字典** 或派生自 §6 `vendor_name` / `account_code`（需另 join **Document**，非缺票表本体）。

### 4. 表格 / 列表

- **columns**：`missing_doc_id`, `client_id`, `legal_name`, `period`, `required_doc_type`, `expected_count`, `received_count`, `confirmed_count`, `missing_reason`, `blocker_level`, `status`。
- **row actions**：**Search history** → **Historical Email Search Results**（query：`client_id`,`period`,`required_doc_type`）；**Generate chase** → **Chase Email Composer**；**Mark not applicable** → `status=not_applicable`；**Month-End Workspace**（带 `client_id`）；**Assign owner** → **非 09**，不写入组件表。

### 5. 状态

- **loading**：汇总、表、Drawer。
- **empty**：筛选下无 Missing 行。
- **error**：查询/保存失败 + 重试。
- **success**：表与 Drawer 可用。

### 6. 交互流程

- **点击**：行 → Drawer。
- **编辑**：**`Missing.status`** 等 §8 允许写回字段。
- **跳转**：→ **Historical Search Results**；→ **Chase Composer**；→ **Month-End Missing Docs**；→ **Document Review**（与缺票理由关联时）。
- **触发模块**：**M9**（SearchAgent / ChaseAgent，`07` §8–9）。

### 7. 边界情况

- **数据缺失**：`expected_count` Preferred 空。
- **OCR 失败**：`missing_reason=ocr_failed`（§8）。
- **API 失败**：见 **error**。
- **重复数据**：缺票行维度不建模发票重复；凭证重复见 **Voucher Board**。

### 8. 页面跳转关系

- **来源**：**Dashboard**；**Month-End › Missing Docs**；**Missing Docs**（一级自链）。
- **去向**：**Historical Email Search Results**；**Chase Email Composer**；**Month-End Workspace**；**Document Review**。

---

## Page: Historical Email Search Results

**路由**：二级 **Chase Center › Historical Email Search Results**（可深链为一级）  
**对齐**：`06_Wireframe_Design_Spec.md` §9 页面 7；`05_Feature_Breakdown.md` F7；PRD R-SEARCH-01；`07_AI_Agent_Workflow.md` §8 SearchAgent。

### 1. 页面目标

- **用户**：Staff、Senior（`01_PRD.md` §4）。
- **解决**：展示历史邮件检索结果与候选附件，支持送入 OCR 或标记不相关，并在无结果时引导催票（`06` §9；`07` §8 输出分级）。
- **对应模块**：**M9**；**F7**；衔接 **M8**（附件→OCR）。

### 2. 页面结构

- **Header**：检索任务标题。
- **Filter Bar**：结果内二次筛选 — `sender_email`, `received_at`, `subject`（§4）；`filename`（§5）。
- **Main Content**：**Query Summary 条**（见 §3）；**结果卡片列表**（每卡一封 **Email** + 子 **Attachment**）。
- **Side Panel / Drawer**：单卡详情（§4 全量 + §5 列表）。
- **Footer**：无结果态 CTA → **Chase Composer**（`06` §9 No result）。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Summary — 检索上下文 | `client_id`, `legal_name` | string | §3 Client；检索入参 | 否 | 跳转 **Month-End Workspace** |
| Summary — 缺票上下文 | `missing_doc_id`, `period`, `required_doc_type` | string, enum | §8 Missing；入参 | 否 | 跳转 **Missing Documents** |
| Summary — KPI | `result_type`, `candidate_count` | string, number | §9 `search_completed` Key Fields（本次检索完成后回写展示） | 否 | 标签 |
| Summary — 检索词 | `query_terms` | string | **非 09**；UI 入参状态 | 否 | 只读展示 |
| Card — Email | `email_id`,`sender_email`,`subject`,`received_at`,`thread_id`,`message_id`,`body_text` | §4 各类型 | §4 Email | 否 | 展开 snippet |
| Card — Attachment | `attachment_id`,`filename`,`mime_type`,`size_bytes`,`hash`,`password_protected`,`duplicate_candidate` | §5 | §5 Attachment | 否 | Send to OCR |
| Card — 联结 Document（若有） | `document_id`,`document_type`,`review_status` | §6 | §6 Document | 否 | 跳转 **Document Review** |
| 匹配表现 | `match_score`, `why_matched` | string | **`09` 无此列**；`07` §8 SearchAgent 输出 | 否 | 只读 |
| Drawer | §4 全表 + §5 子表 | 同上 | §4；§5 | 否 | Open email（系统内详情） |

**说明**：`07` §8 结果分级 `found_exact` / `found_possible` / `context_only` / `not_found` — 可映射为 **`result_type`（§9）** 展示文案；**不新增库字段名**。

### 4. 表格 / 列表

- **列表即卡片栅格**；每卡 **主行 columns**：`result_type`（或 §9 标签）、`sender_email`, `received_at`, `subject`, `match_score`（待字典）、`why_matched`（待字典）。
- **row actions**：**Open email**（Drawer）；**Send attachment to OCR** → **Document Review** / 触发 **DocumentAgent**；**Mark not relevant**（流程：`email_intent` / 标签策略 **非 09** — 标 **待产品/字典** 或仅用 §4 只读标记不采纳）。

### 5. 状态

- **loading**：检索中。
- **empty**：`not_found` 或无候选 → `06` §9 No result 文案 + CTA **Chase Composer**。
- **error**：Search API 失败 + 重试。
- **success**：卡片列表可交互。

### 6. 交互流程

- **点击**：开 Drawer；选附件送 OCR。
- **编辑**：本页 **默认不编辑** §4/§5 主数据；若支持「标记不相关」见 §4 row actions 说明。
- **跳转**：→ **Chase Composer**；→ **Missing Documents**；→ **Document Review**；→ **Email Inbox**。
- **触发模块**：**M9**（SearchAgent）；送 OCR → **M8** / **DocumentAgent**（`07` §5）。

### 7. 边界情况

- **数据缺失**：无附件仅有邮件正文 → 仍展示 §4；`context_only`（`07` §8）→ 提示无附件。
- **OCR 失败**：送 OCR 后失败 → **Exceptions**。
- **API 失败**：见 **error**。
- **重复数据**：§5 `duplicate_candidate` / `hash` 标签。

### 8. 页面跳转关系

- **来源**：**Missing Documents**；**Month-End › Missing Docs**；**Chase History**（KPI 跳转）。
- **去向**：**Chase Email Composer**；**Document Review**；**Email Inbox**；**Missing Documents**。

---

## Page: Chase Email Composer

**路由**：二级 **Chase Center › Chase Email Composer**（可深链一级）  
**对齐**：`06_Wireframe_Design_Spec.md` §10 页面 8；`05_Feature_Breakdown.md` F8；PRD R-CHASE-01；`07_AI_Agent_Workflow.md` §9 ChaseAgent。

### 1. 页面目标

- **用户**：Staff、Senior、Manager（`01_PRD.md` §4）。
- **解决**：基于缺票清单与客户联系人起草催票邮件，支持 L1–L3 模板、人工审核后发送或保存草稿（PoC 默认草稿，`01_PRD.md` §5、R-CHASE-01）。
- **对应模块**：**M2\***（邮件催票）；**M9**；**F8**。

### 2. 页面结构

- **Header**：任务标题；客户上下文。
- **Filter Bar**：无（单任务页）；多缺票合并时可 **Missing 多选**（§8 `missing_doc_id` 列表）。
- **Main Content**：**左** — Missing 列表 + 客户联系 + 历史催票/邮件证据；**右** — 模板与邮件编辑器（见 §3 非 09 说明）。
- **Side Panel / Drawer**：可选 **§4 Email** 原文引用（客户回复）。
- **Footer**：`Save draft` \| `Send for review` \| `Send now` \| `Cancel`（`06` §10）。

### 3. 组件定义（逐个组件）

#### A. 仅 `09` 已定义字段（可绑定 UI）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Missing 列表项 | `missing_doc_id`, `client_id`, `period`, `required_doc_type`, `expected_count`, `received_count`, `confirmed_count`, `missing_reason`, `blocker_level`, `status` | §8 各类型 | §8 Missing | `status` 按权限可编辑 | 勾选插入正文清单 |
| Client — 联系人 | `client_id`, `legal_name`, `trading_name`, `primary_contact_email`, `email_domains`, `mapping_confidence` | string, array, number | §3 Client | `primary_contact_email` 权限内可编辑 | 插入「收件人」默认 |
| 历史催票 — KPI | `chase_level`, `recipient` | string | §9 `chase_sent` | 否 | 只读时间线 |
| 历史邮件 — 证据 | `email_id`,`subject`,`received_at`,`sender_email`,`body_text`,`email_intent`,`thread_id` | §4 各类型 | §4 Email | 否 | 引用 snippet |
| 凭证证据（可选） | `document_id`, `source_evidence` | string, array | §6 Document | 否 | 展示证据链 |

#### B. 邮件草稿区（`09` **无** ChaseEmail / Message 字段表）

| 组件 | 字段名 | 类型 | 数据来源 | 是否可编辑 | 用户操作 |
|------|--------|------|----------|------------|----------|
| 模板档位 | `template_level` | enum（L1/L2/L3） | `05` F8；**非 09** | 是 | 切换语气档位（`07` §9） |
| 收件人草稿 | `recipient` | string | UI 状态；**默认** `§3.primary_contact_email` | 是 | 编辑 |
| 主题 | `subject` | string | UI 状态 / 持久化 **待数据字典** | 是 | 编辑 |
| 正文 | `body` | text | UI 状态 / 持久化 **待数据字典** | 是 | 编辑 |

发送成功后，可记录 **§9 `chase_sent`** 的 Key Fields（`chase_level`, `recipient`）及关联 `client_id`（实现层）；**不发明** `chase_id` 列名。

### 4. 表格 / 列表

- **Missing 插入表 columns**：`period`, `required_doc_type`, `missing_reason`, `blocker_level`, `status`。
- **row actions**：勾选/取消插入邮件正文；跳转 **Missing Documents**。

### 5. 状态

- **loading**：客户/Missing/历史数据加载；提交发送。
- **empty**：无选中 Missing 且无手动上下文 → 提示从 **Missing Documents** 进入。
- **error**：SMTP/API、权限、校验失败 + 重试或保存草稿。
- **success**：草稿已保存 / 已送审 / 已发送（PoC 以实际集成为准）。

### 6. 交互流程

- **点击**：插入缺失清单、插入模板段落（`05` F8）。
- **编辑**：§3、§8 可编辑项；草稿 **subject/body/recipient**。
- **跳转**：→ **Missing Documents**；→ **Chase History**；→ **Email Inbox**。
- **触发模块**：**M2\*** / **M9**；**ChaseAgent**（`07` §9）；发送后 **EmailAgent** 侧记录 `message_id`/`thread_id`（`07` §4，实现层）。

### 7. 边界情况

- **数据缺失**：`primary_contact_email` Preferred 空（§3）→ 强制用户填 `recipient`。
- **OCR 失败**：非主路径；Missing 文案可含 `ocr_failed`（§8）。
- **API 失败**：见 **error**；**Save draft** 降级。
- **重复数据**：多次 `chase_sent`（§9）仅展示，不合并。

### 8. 页面跳转关系

- **来源**：**Missing Documents**；**Month-End › Missing Docs**；**Historical Search Results**（无结果 CTA）；**Chase History**。
- **去向**：**Chase History**；**Missing Documents**；**Email Inbox**；**Dashboard**。

---

## Page: Exceptions

**路由**：一级 **Exceptions**（异常队列）  
**对齐**：`06_Wireframe_Design_Spec.md` §2「Exceptions」；`05_Feature_Breakdown.md` F9；`10_Decision_Rules_and_Human_Gates.md` §2、§6；`07_AI_Agent_Workflow.md` §3 Exception 分支。

### 1. 页面目标

- **用户**：Staff、Senior、Manager（`01_PRD.md` §4）。
- **解决**：集中处理低置信、API 失败、加密件、客户不确定、Xero 写入失败等异常项，支持 **Retry / Resolve / Close**（`07` §3）。
- **对应模块**：**F9**；汇聚 **M8**（邮件/附件）、**M9**（检索失败等）、**M1\***（OCR/审核异常）。

### 2. 页面结构

- **Header**：队列标题；风险摘要（聚合计数 — **实现派生**，字段仍只引用 §6/§5/§4/§3）。
- **Filter Bar**：`queue_row_kind`（**UI-only**：document \| attachment \| email \| xero）；`client_id`；`period`；`review_status`；`xero_status`；`password_protected`；`duplicate_candidate`；`mapping_confidence` 区间（§3）。
- **Main Content**：**统一异常表**（多实体联结，见 §3）。
- **Side Panel / Drawer**：选中行详情（按 `queue_row_kind` 加载 §6 / §5 / §4 / §3 对应全字段）。
- **Footer**：无或批量 **Retry**（`06` §11 批量可控 — 可选）。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter | `queue_row_kind` | enum（UI-only） | — | 否 | 筛选实体类型 |
| Filter | `client_id` | string | §6 Document / §4 Email / §8 Missing | 否 | 筛选 |
| Filter | `period` | string | §6 / §8 | 否 | 筛选 |
| Filter | `review_status` | enum | §6 Document | 否 | 含 `exception` 等 |
| Filter | `xero_status` | enum | §6 Document | 否 | 含 `write_failed` |
| Filter | `password_protected`, `duplicate_candidate` | boolean | §5 Attachment | 否 | 筛选 |
| Filter | `mapping_confidence` | number | §3 Client（联结） | 否 | 低置信筛选 |
| Row — Document 异常 | `document_id`, `attachment_id`, `client_id`, `document_type`, `period`, `confidence_score`, `review_status`, `xero_status`, `source_evidence` | §6 各类型 | §6 Document | `review_status` 等按流程可编辑 | Retry / Resolve |
| Row — Attachment 异常 | `attachment_id`, `email_id`, `filename`, `password_protected`, `duplicate_candidate`, `hash` | §5 | §5 Attachment | 否 | Request password / 跳转 Classification |
| Row — Email 异常 | `email_id`, `client_id`, `sender_email`, `processing_status`, `subject`, `received_at` | §4 | §4 Email | `client_id` 可编辑（匹配修正） | Override |
| Row — Client 展示 | `legal_name`, `mapping_confidence` | string, number | §3 Client | 否 | 跳转 **Month-End Workspace** |
| Drawer | 按行类型加载 §6 或 §5 或 §4 或 §8 全表 | 混合 | 混合 | 同各实体页策略 | 深度处理 |

**说明**：`queue_row_kind` 与 **主键列**（`document_id` / `attachment_id` / `email_id`）为 **UI 联结键**，**非 `09` 新表**。

### 4. 表格 / 列表

- **columns**：`queue_row_kind`, `primary_id`（= 上列三类之一，**UI 列名**）, `client_id`, `legal_name`, `period`, `review_status`, `xero_status`, `confidence_score`, `password_protected`, `duplicate_candidate`, `filename`, `subject`, `received_at`。
- **row actions**：**Retry**（OCR/Xero/同步，`07` §3）；**Resolve**；**Close**；跳转 **Document Review**；**Document Classification**；**Email Inbox**；**Chase Composer**（缺票升级）。

### 5. 状态

- **loading**：表、Drawer、Retry 请求。
- **empty**：无异常行。
- **error**：队列查询 / Retry API 失败。
- **success**：操作完成刷新。

### 6. 交互流程

- **点击**：行 → Drawer。
- **编辑**：同 Drawer 策略；**Email.client_id** override。
- **跳转**：见 row actions。
- **触发模块**：**Orchestrator** Exception 分支；**DocumentAgent**；**XeroAgent**；**EmailAgent**（`07`）。

### 7. 边界情况

- **数据缺失**：行字段部分空 → 仍展示可解析列。
- **OCR 失败**：`review_status=exception` 或 Missing `ocr_failed` 联动入口。
- **API 失败**：`xero_status=write_failed` + Retry；邮件 API → 行保留（`06` §11 状态可恢复）。
- **重复数据**：§5 `duplicate_candidate` 高亮。

### 8. 页面跳转关系

- **来源**：**Dashboard**；**Document Review**；**Email Inbox**；**Voucher Board**；各页 **error** 引导。
- **去向**：**Document Review**；**Document Classification**；**Email Inbox**；**Chase Composer**；**Missing Documents**；**Month-End Workspace**。

---

## Page: Reports

**路由**：一级 **Reports**（KPI & Reports）  
**对齐**：`06_Wireframe_Design_Spec.md` §2「KPI & Reports」；`05_Feature_Breakdown.md` F1；`12_KPI_Measurement_Plan.md`（度量计划，**非新数据表**）。

### 1. 页面目标

- **用户**：Senior、Manager、FDE（`01_PRD.md` §4；KPI 读者）。
- **解决**：按期间/客户查看 KPI 事件与业务实体聚合，支撑 PoC 验收与运营复盘（PRD §8 KPI；`12` 各维度）。
- **对应模块**：**M6\***（信息架构映射）；**F1**；汇聚 **M8/M9/M1\*** 结果在只读报表中体现。

### 2. 页面结构

- **Header**：报表名；**期间**（`period` 来自 §6/§8 筛选上下文，string）。
- **Filter Bar**：`client_id`（§3/§6）；`period`；`document_type`；`review_status`；`xero_status`；KPI **Event** 类型（UI 枚举 = `09` §9 Event 列名）。
- **Main Content**：**Tab A — KPI 事件明细表**（§9）；**Tab B — 业务聚合**（§6 Document 计数、§8 Missing 计数、§4 Email 计数 — **SQL 聚合，字段仍属 09**）；**Tab C — 导出**（CSV 为 **UI 行为**，列集来自 Tab A/B 已列字段）。
- **Side Panel / Drawer**：无或「指标定义」静态帮助（引用 `12`，**无 09 字段**）。
- **Footer**：无。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter | `client_id` | string | §3 / §6 / §8 联结 | 否 | 筛选 |
| Filter | `period` | string | §6 Document；§8 Missing | 否 | 筛选 |
| Filter | `document_type` | enum | §6 Document | 否 | 筛选 |
| Filter | `review_status`, `xero_status` | enum | §6 Document | 否 | 筛选 |
| Filter | `event` | enum（UI = §9 Event 名） | §9 KPI Event | 否 | 筛选事件类型 |
| Tab A — 行 | `event` + 各事件 **Key Fields** | 见 §9 | §9 KPI Event | 否 | 钻取 **Dashboard** / **Audit Trail** |
| Tab B — Document 聚合 | `document_id` 计数、`review_status` 分布、`xero_status` 分布、`confidence_score` 分桶 | number / enum | §6（聚合查询） | 否 | 钻取 **Voucher Board** |
| Tab B — Missing 聚合 | `missing_doc_id` 计数、`missing_reason` 分布、`blocker_level` 分布 | number / enum | §8（聚合） | 否 | 钻取 **Missing Documents** |
| Tab B — Email 聚合 | `email_id` 计数、`email_intent` 分布、`processing_status` 分布 | number / enum | §4（聚合） | 否 | 钻取 **Email Inbox** |
| Tab B — Client 列表 | `client_id`, `legal_name`, `status`, `mapping_confidence` | §3 Client | §3 | 否 | 钻取 **Month-End Workspace** |

**说明**：图表坐标轴标签若使用「月结周期」「催票响应率」等 **来自 `12` 的指标名**，**不冒充 `09` 字段**；底层数据仍须能回溯至 §3–§9 列。

### 4. 表格 / 列表

- **Tab A columns**：`event` + 动态 Key Field 列（与 §9 表一致）。
- **Tab B columns**：按所选聚合维度展开（实现定义），**列名不超出 09**。
- **row actions**：钻取至各业务一级页并带筛选 query。

### 5. 状态

- **loading**：聚合查询、导出任务。
- **empty**：筛选范围内无事件/无实体。
- **error**：查询超时 / 权限 / 导出失败。
- **success**：表与导出可用。

### 6. 交互流程

- **点击**：钻取业务页。
- **编辑**：**本页只读**（报表不写回业务主数据）。
- **跳转**：→ **Dashboard**；→ **Voucher Board**；→ **Missing Documents**；→ **Email Inbox**；→ **Month-End Workspace**。
- **触发模块**：无 Agent 写；读 **KPIAgent** 持久化结果（`07` §2）。

### 7. 边界情况

- **数据缺失**：部分 §9 Key Field 在历史事件中为空 → 空单元格。
- **OCR 失败**：经 §8 `missing_reason=ocr_failed` 聚合体现。
- **API 失败**：见 **error**。
- **重复数据**：聚合层去重策略 **实现层**；**不新增 09 字段**。

### 8. 页面跳转关系

- **来源**：**Dashboard**；**Settings**；全局 **Reports**。
- **去向**：**Dashboard**；**Voucher Board**；**Missing Documents**；**Email Inbox**；**Audit Trail**（客户内）。

---

## Page: Rule & Config

**路由**：二级 **Settings › Rule & Config**  
**对齐**：`06_Wireframe_Design_Spec.md` §2「Settings」；`05_Feature_Breakdown.md` F11（P1）；`10_Decision_Rules_and_Human_Gates.md` §3、§6；PRD §7 可配置性。

### 1. 页面目标

- **用户**：Manager、FDE（`01_PRD.md` §4）。
- **解决**：维护阈值、自动发送开关、客户白名单、催票模板等 **运行参数**（`05` F11；PRD 可配置性）。
- **对应模块**：**F11**；影响 **M8/M9/M2\*** 行为边界（`10`）。

### 2. 页面结构

- **Header**：设置分区标题。
- **Filter Bar**：配置分组 Tab（**UI-only**：thresholds \| chase \| whitelist \| templates）。
- **Main Content**：**配置表单区**（见 §3：`09` **无** Rule/Config 字段表）。
- **Side Panel / Drawer**：变更说明 / 回滚提示（静态或审计日志入口 → **Audit** 若接 §9，**非必须**）。
- **Footer**：`Save` \| `Reset`（UI 标准）。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| 置信度阈值 — High | `confidence_threshold_high` | number | **`09` 无**；`10` §3 文案 0.90 | 是（配置存储 **待数据字典**） | 保存 |
| 置信度阈值 — Medium | `confidence_threshold_medium_low` | number | **`09` 无**；`10` §3 文案 0.70 | 是 | 保存 |
| 自动发送开关 | `auto_send_chase_enabled` | boolean | **`09` 无**；PRD PoC 默认关 | 是 | 保存 |
| 客户白名单 | `client_id` 列表 | array of string | **引用** §3 `client_id` 合法值；白名单容器 **待数据字典** | 是 | 增删 client |
| 试点邮箱范围 | `mailbox_id` 列表 | array of string | **引用** §4 `mailbox_id`；范围策略 **待数据字典** | 是 | 维护 |
| 催票模板 body | `chase_template_L1` 等 | text | **`09` 无**；`05` F8 L1/L2/L3 | 是 | 编辑模板 |
| 只读引用 — Client | `legal_name`, `client_id` | string | §3 Client | 否 | 白名单行展示 |

**说明**：F11 全部持久化键值 **不在 `09_Data_Mapping.md`** → 上表字段名为 **实现占位**；上线前须 **独立配置字典** 与迁移策略。

### 4. 表格 / 列表

- **白名单表 columns**：`client_id`, `legal_name`, `status`, `mapping_confidence`（§3，联结只读）。
- **row actions**：移除白名单；跳转 **Month-End Workspace**。

### 5. 状态

- **loading**：拉取配置。
- **empty**：无白名单 / 无自定义模板 → 默认文案。
- **error**：保存失败、校验失败（阈值 0–1、互斥规则）。
- **success**：保存成功。

### 6. 交互流程

- **点击**：切换分组 Tab；选择客户加入白名单。
- **编辑**：各配置项表单。
- **跳转**：→ **Client** 详情（§3 维护若另有页）；→ **Reports**。
- **触发模块**：配置变更后影响 **Orchestrator / ChaseAgent / ReviewAgent** 行为（`07`）；**不写 `09` 业务实体**。

### 7. 边界情况

- **数据缺失**：§3 中客户 inactive → 白名单警告。
- **OCR 失败**：非本页主路径。
- **API 失败**：见 **error**；禁止静默（PRD NFR）。
- **重复数据**：白名单重复 `client_id` → 表单校验拒绝。

### 8. 页面跳转关系

- **来源**：**Settings**；**Dashboard**（管理员入口）。
- **去向**：**Reports**；**Dashboard**；**Chase Composer**（模板预览）。

---

## Page: Vendor Rule Assistant

**路由**：二级 **Settings › Vendor Rule Assistant**  
**对齐**：`05_Feature_Breakdown.md` F12（P2 / V3）；`01_PRD.md` Out of Scope 备注 Vendor Rule 难复用 — 本页为 **路线图占位**。

### 1. 页面目标

- **用户**：Senior、Manager（`01_PRD.md` §4）。
- **解决**：基于历史凭证中的 **vendor / 科目 / GST** 出现模式，辅助建立或浏览规则建议（`05` F12；**PoC 可不实现 UI**）。
- **对应模块**：**F12**（P2）；与 **M1\***（科目/GST 确认）衔接。

### 2. 页面结构

- **Header**：功能 Beta / P2 标识（**无 09 字段**）。
- **Filter Bar**：`vendor_name`（§6）；`client_id`；`period`；`document_type`。
- **Main Content**：**Vendor 聚合表**（由 §6 派生 **distinct `vendor_name`**）；**规则建议区**（`09` **无 Rule 表** → 见 §3）。
- **Side Panel / Drawer**：选中 vendor → 展示代表性 **Document** 行样本（§6）。
- **Footer**：无或「导出 CSV」（列仅限 §6）。

### 3. 组件定义（逐个组件）

| 组件 | 字段名 | 类型 | 数据来源（09） | 是否可编辑 | 用户操作 |
|------|--------|------|----------------|------------|----------|
| Filter | `vendor_name` | string | §6 Document | 否 | 搜索 |
| Filter | `client_id` | string | §6 Document | 否 | 筛选 |
| Filter | `period` | string | §6 Document | 否 | 筛选 |
| Filter | `document_type` | enum | §6 Document | 否 | 筛选 |
| 聚合行 — Vendor | `vendor_name` | string | §6 Document（GROUP BY） | 否 | 展开样本 |
| 聚合统计 | `document_id` 计数、`confirmed` 态计数（`review_status=confirmed`） | number | §6（聚合） | 否 | 只读 |
| 建议科目 — 众数 | `account_code` | string | §6 Document（MODE 聚合） | **否**（P2 建议只读） | 复制到剪贴板 |
| 建议税 — 众数 | `gst_rate` | string | §6 Document（MODE） | 否 | 复制 |
| 样本行 | `document_id`, `invoice_number`, `invoice_date`, `total_amount`, `currency`, `account_code`, `gst_rate`, `confidence_score` | §6 各类型 | §6 Document | 否 | 跳转 **Document Review** |
| 规则持久化 | `rule_id`, `rule_payload` | string | **`09` 无** | 是 | **待 Vendor Rule 数据字典** |

**说明**：`05`「Vendor Master List」**无 `09` 表** → 本页 **最小可行** 仅为 §6 聚合视图；**写入 Rule** 标 **待字典**。

### 4. 表格 / 列表

- **Vendor 聚合 columns**：`vendor_name`, `doc_count`, `mode_account_code`, `mode_gst_rate`（后两列 **派生**，列名实现层定义，值仍来自 §6）。
- **row actions**：展开样本；跳转 **Document Review**；**应用建议到 Rule**（若 `rule_payload` 字典落地）。

### 5. 状态

- **loading**：聚合慢查询。
- **empty**：无 §6 `vendor_name` 非空行。
- **error**：查询失败。
- **success**：表可用。

### 6. 交互流程

- **点击**：展开样本；跳转 **Document Review**。
- **编辑**：仅当 **Rule 字典** 落地后可编辑规则实体；否则 **只读**。
- **跳转**：→ **Document Review**；→ **Rule & Config**（若规则并入 F11）。
- **触发模块**：只读分析；写规则时 **待产品**（无 `07` 专名 Agent）。

### 7. 边界情况

- **数据缺失**：`vendor_name` Preferred 空（§6）→ 归入「Unknown」桶（**UI 桶名非 09**）。
- **OCR 失败**：低 `confidence_score` 样本可降权（聚合策略，**不增字段**）。
- **API 失败**：见 **error**。
- **重复数据**：同一 `vendor_name` 大小写变体 → 归一化策略 **实现层**。

### 8. 页面跳转关系

- **来源**：**Settings**；**Document Review**（「查看 vendor 规则」入口，可选）。
- **去向**：**Document Review**；**Rule & Config**；**Voucher Board**。

---

## Page Designs — 完成状态

| 扁平清单页 | 状态 |
|------------|------|
| Dashboard；Month-End 6 Tabs；Email Inbox；Document Classification；Review Tasks；Document Review；Voucher Board；Missing Documents；Historical Search；Chase Composer；Exceptions；Reports；Rule & Config；Vendor Rule Assistant | **已在本文档写入设计节** |

### 扁平清单 ↔ 设计节标题对照

| # | 扁平清单路由 | `## Page:` 标题 |
|---|----------------|-----------------|
| 1 | Dashboard | `## Page: Dashboard` |
| 2 | Month-End Workspace › Overview | `## Page: Month-End Workspace › Overview` |
| 3 | Month-End Workspace › Documents | `## Page: Month-End Workspace › Documents` |
| 4 | Month-End Workspace › Emails | `## Page: Month-End Workspace › Emails` |
| 5 | Month-End Workspace › Missing Docs | `## Page: Month-End Workspace › Missing Docs` |
| 6 | Month-End Workspace › Chase History | `## Page: Month-End Workspace › Chase History` |
| 7 | Month-End Workspace › Audit Trail | `## Page: Month-End Workspace › Audit Trail` |
| 8 | Email Inbox | `## Page: Email Inbox` |
| 9 | Document Classification | `## Page: Document Classification` |
| 10 | Review Tasks | `## Page: Review Tasks` |
| 11 | Document Review / OCR | `## Page: Document Review / OCR` |
| 12 | Voucher Board | `## Page: Voucher Board` |
| 13 | Missing Documents | `## Page: Missing Documents` |
| 14 | Chase Center › Historical Email Search Results | `## Page: Historical Email Search Results` |
| 15 | Chase Center › Chase Email Composer | `## Page: Chase Email Composer` |
| 16 | Exceptions | `## Page: Exceptions` |
| 17 | Reports | `## Page: Reports` |
| 18 | Settings › Rule & Config | `## Page: Rule & Config` |
| 19 | Settings › Vendor Rule Assistant | `## Page: Vendor Rule Assistant` |

---

## 最终检查报告（审计日期：交付包内审）

### 检查项结论

| # | 检查项 | 结论 | 说明 / 修复 |
|---|--------|------|----------------|
| 1 | 是否所有页面都有设计 | **通过** | 扁平清单 **19** 条 ↔ `## Page:` **19** 节（上表对照）。 |
| 2 | 是否有遗漏页面 | **通过** | **Chase Center** 为侧栏分组名，无单独落地页（与 `06` §2 一致）；**Settings** 一级无独立壳页，扁平清单仅含 **Rule & Config**、**Vendor Rule Assistant** 二级路由，**不视为遗漏**。 |
| 3 | 是否有页面结构不完整 | **通过** | 各页均含 **§1 目标 — §8 跳转**；**§2 页面结构** 均含 Header / Main；无 Footer 要求的页面已注明「无」。 |
| 4 | 是否有字段缺失 | **有条件通过** | 业务主数据字段以 **`09_Data_Mapping.md`** 为界；**Chase Composer** 草稿正文、**Rule & Config** 配置键、**Search** 的 `match_score` 等已标 **「待数据字典」**，**非遗漏**而是交付包未定义列。 |
| 5 | 是否有缺少状态（loading / empty / error / success） | **已修复并通过** | 全部 19 页 **§5 状态** 均显式含 **loading、empty、error、success**（**Voucher Board** 已由「同 Documents」简写改为四条独立描述）。 |

### 签署

- **文档状态**：**已完成**（PoC 设计交付）；配置类 / 催票草稿类字段待独立数据字典后可增量改 `## Page: Rule & Config` 与 `## Page: Chase Email Composer` 的 §3 表。

---
