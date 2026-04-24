# 11_UAT_Test_Cases：用户验收测试用例

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. UAT 目标

验证智能会计交付助手是否能支持 M8 邮件凭证处理和 M9 历史邮件检索催票的 PoC 闭环，并确保低置信度、异常、Xero 写入和催票动作都有人工控制和可追溯记录。

## 2. UAT 用例总览

| ID | 场景 | 优先级 |
|---|---|---|
| UAT-01 | 正常邮件附件进入 OCR | P0 |
| UAT-02 | 多附件邮件分类 | P0 |
| UAT-03 | 客户匹配不确定 | P0 |
| UAT-04 | OCR 低置信字段人工确认 | P0 |
| UAT-05 | Xero Draft 创建成功 | P0 |
| UAT-06 | Xero 写入失败处理 | P0 |
| UAT-07 | 缺票识别 | P0 |
| UAT-08 | 历史邮件找到附件 | P0 |
| UAT-09 | 历史邮件未找到，生成催票草稿 | P0 |
| UAT-10 | 客户回复补发附件后状态回流 | P0 |
| UAT-11 | 密码保护文件异常 | P1 |
| UAT-12 | 多页发票合并建议 | P1 |
| UAT-13 | 重复 invoice 检测 | P1 |
| UAT-14 | 催票邮件 bounce | P1 |
| UAT-15 | Audit Trail 完整性 | P0 |

## 3. Detailed Test Cases

### UAT-01：正常邮件附件进入 OCR
前置条件：试点邮箱 API 可读取；客户 mapping 已存在；Blue Sheets API 可用。  
步骤：系统同步邮件 → 捕获附件 → 自动识别 supplier invoice → 发送 OCR。  
预期：邮件出现在 Intake Queue；附件状态为 OCR Processing / Ready for Review；source email 被记录。

### UAT-02：多附件邮件分类
测试数据：邮件中包含 invoice、bank statement、irrelevant file。  
预期：三个附件分别标记为 supplier_invoice、bank_statement、other / irrelevant；用户可人工修正分类。

### UAT-03：客户匹配不确定
测试数据：sender 为个人邮箱，subject 中客户名称模糊。  
预期：任务进入 Client Match Review，显示候选客户和匹配理由；Staff 选择后继续 OCR。

### UAT-04：OCR 低置信字段人工确认
测试数据：OCR 返回 amount confidence = 0.62。  
预期：amount 字段高亮，无法直接提交，必须确认或修改；修改后保存 audit log。

### UAT-05：Xero Draft 创建成功
前置条件：OCR 字段已确认，Xero contact 和 account code 已 mapping。  
预期：Xero 返回 draft ID，document xero_status = drafted；保存 payload、response、source evidence。

### UAT-06：Xero 写入失败处理
测试数据：account_code 缺失或无效。  
预期：系统阻止写入或显示 Xero validation error；任务进入 Mapping Required，可修正后重试。

### UAT-07：缺票识别
测试数据：月结清单显示客户 ABC 应有 6 月 bank statement，但系统未确认。  
预期：Missing Document Tracker 显示缺 2026-06 bank statement，next action = Search History。

### UAT-08：历史邮件找到附件
测试数据：历史邮件中存在 2026-06 bank statement 附件。  
预期：SearchAgent 返回 exact match，显示邮件、附件、匹配理由；可一键 Send to OCR。

### UAT-09：历史邮件未找到，生成催票草稿
测试数据：历史邮件中无缺失附件。  
预期：生成催票草稿，自动插入缺失清单；默认不自动发送。

### UAT-10：客户回复补发附件后状态回流
前置条件：已发送催票邮件，客户回复并附上文件。  
预期：新附件进入 Intake Queue；对应 missing_doc status 更新为 received。

### UAT-11：密码保护文件异常
预期：文件进入 Exception Queue，提示 Password Protected；不进入 OCR，可生成请求密码邮件草稿。

### UAT-12：多页发票合并建议
预期：系统提示 possible multi-page invoice；Staff 可合并或分开处理。

### UAT-13：重复 invoice 检测
预期：同 client、vendor、invoice_number、amount 的文件标记 duplicate candidate；Staff 确认保留 / 合并 / 忽略。

### UAT-14：催票邮件 bounce
预期：status = bounced，创建联系人更新任务；不继续自动发送给同一无效地址。

### UAT-15：Audit Trail 完整性
预期：任一完成凭证可看到 source email、attachment、OCR result、人工修改、Xero write、催票关联。

## 4. UAT Exit Criteria

| 标准 | 要求 |
|---|---|
| P0 用例通过率 | 100% 或有明确 workaround |
| P1 用例通过率 | ≥80% |
| 阻塞 bug | 0 个开放 |
| 高风险 bug | 有 owner 和修复计划 |
| 数据追溯 | P0 场景均有 audit trail |
| 业务 Owner | 确认 PoC 可进入下一阶段 |
