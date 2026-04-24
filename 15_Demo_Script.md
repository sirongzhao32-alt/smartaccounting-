# 15_Demo_Script：产品演示脚本

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. Demo 目标

让客户和内部决策者在 8–12 分钟内看懂：智能会计交付助手如何把月结前端最耗时的邮件凭证处理和缺票催票流程串起来，并保留人工确认和审计追溯。

## 2. Demo 核心故事线

> 今天的会计团队不是不会做账，而是被大量邮件、附件、缺票和状态追踪拖慢。这个助手不是替代会计判断，而是把客户邮件里的凭证自动带到正确的工作流里，让 Staff 只审核需要人判断的地方，让 Manager 看到风险和进度。

## 3. Demo 场景设定

| 项目 | 内容 |
|---|---|
| 客户 | ABC Pte Ltd |
| Period | 2026 年 6 月月结 |
| 输入 | 客户邮件包含 2 张 invoice 和 1 份 bank statement |
| 问题 | 月结清单显示缺 6 月 DBS bank statement |
| 系统动作 | 自动处理已收到附件；历史邮件找不到缺失 bank statement；生成催票草稿 |

## 4. Demo Flow

### Step 1：打开 Dashboard

讲解词：  
“这是月结总览。我们不是从邮箱开始，而是从业务状态开始。系统把所有试点客户按月结风险排序，显示凭证覆盖率、缺票数量、待人工确认任务和 Xero 写入失败。Manager 可以立刻看到哪些客户会影响 deadline。”

展示点：KPI cards、ABC Pte Ltd 风险为 Missing Docs、Next Action。

### Step 2：进入 Email Intake Queue

讲解词：  
“过去 Staff 需要自己在邮箱里找客户邮件、下载附件、再上传 Blue Sheets。现在 EmailAgent 已经把试点客户的邮件和附件抓到 Intake Queue，并自动识别附件类型。”

展示点：sender、subject、matched client、invoice / bank statement 附件分类。

### Step 3：附件分类确认

讲解词：  
“客户文件命名通常不标准，所以系统会先给出分类和客户匹配结果。高置信可以直接进入 OCR；不确定的文件会要求人工确认。”

展示点：文件预览、Predicted client、Predicted document type、Confirm and send to OCR。

### Step 4：Document Review / OCR 确认

讲解词：  
“file.ai / Blue Sheets 返回结构化字段后，系统不会直接自动入账，而是进入 Review 页面。Staff 可以在同一屏幕对照原始文件和 OCR 字段，只处理低置信或异常字段。”

展示点：PDF 预览、vendor、invoice number、amount、GST、低置信高亮、Confirm。

### Step 5：创建 Xero Draft

讲解词：  
“确认后的凭证会创建 Xero Draft。PoC 阶段我们默认只写 Draft，不自动 approve，这样既节省录入时间，也保留会计人员的控制权。”

展示点：Xero payload preview、Create Draft、Draft ID、Audit Trail。

### Step 6：Missing Document Tracker

讲解词：  
“接下来是月结时最常见的痛点：缺票。系统将应收凭证清单和已确认凭证对比，自动发现 ABC 仍缺 6 月 DBS bank statement。”

展示点：Missing Document Table、Next Action: Search History。

### Step 7：历史邮件检索

讲解词：  
“过去 Staff 需要翻大量历史邮件。现在 SearchAgent 会按客户、月份、文档类型、关键词和附件名称检索历史邮件，并给出匹配理由。”

展示点：Search query summary、候选邮件、No exact matching attachment found。

### Step 8：生成催票草稿

讲解词：  
“如果历史邮件里没有找到附件，系统会自动生成催票草稿，把缺失清单写清楚。PoC 默认由 Staff 审核后发送，避免客户沟通风险。”

展示点：Chase Email Composer、Missing list、L1 friendly reminder、Send / Save draft。

### Step 9：客户回复后状态回流

讲解词：  
“客户回复后，EmailAgent 会识别该回复属于哪一次催票。如果客户补发了附件，文件会重新进入 Intake Queue，同时 Missing Document 状态从 Waiting Client 更新为 Received。”

展示点：Chase status、Missing status、Dashboard coverage 更新。

## 5. 可能被问到的问题与回答

| 问题 | 回答 |
|---|---|
| AI 会不会直接替代会计人员判断？ | 不会。AI 负责邮件捕获、附件分类、OCR 调用、历史邮件检索和催票草稿；会计判断、低置信字段、GST / 科目映射、Xero approve 都保留人工关卡。 |
| 如果 OCR 错了怎么办？ | 系统展示置信度，低置信字段高亮，Staff 必须人工确认后才能进入 Xero Draft，所有修改进入 audit trail。 |
| 客户文件命名很乱怎么办？ | 不依赖文件名，而是结合邮件上下文、附件内容、OCR 结果和人工修正；无法判断进入 Exception Queue。 |
| 如果邮箱 API 或 Xero 权限暂时不开怎么办？ | PoC 有降级方案：邮箱可转发或导出样本，Xero 可用 mock endpoint 或 CSV 模拟 Draft。 |
| 催票邮件可以自动发吗？ | 技术上可以，但 PoC 默认生成草稿，由 Staff 审核后发送。 |

## 6. 结束页总结

> Smart Accounting Delivery Assistant turns accounting email chaos into a controlled, auditable month-end workflow — with AI handling repetitive intake and retrieval, and humans retaining control over accounting judgment.
