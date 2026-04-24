# 智能会计交付助手设计交付包 README

> Project: 智能会计交付助手（新加坡） / Smart Accounting Delivery Assistant  
> Scenario: AG-B3-01（原 S4） | Priority: P0 | Agent Layer: Business Agent / L2  
> Version: v1.0 design delivery pack | Date: 2026-04-24  
> Basis: `03_srp_smart_accounting_b3_v2.md` + 4月8日–4月20日调研总结  
> Note: 标注“待确认 / 待验证”的内容，需要 FDE、客户业务 Owner 或技术团队继续确认。


## 1. 交付包目的

这套文件用于支持 AG-B3-01 智能会计交付助手的产品定义、设计推进、技术对接、PoC 验收和客户汇报。它不是单纯的 UI 说明，而是一套从业务痛点到产品功能、从用户流程到系统集成、从人工审核到 KPI 衡量的完整设计文档。

产品形态应理解为：**面向月结前端流程的 AI workflow system**，不是会计聊天机器人。

## 2. 推荐阅读顺序

| 顺序 | 文件 | 用途 |
|---|---|---|
| 1 | `01_PRD.md` | 产品目标、范围、用户、功能与验收标准 |
| 2 | `02_PoC_Plan.md` | PoC 范围、阶段、成功标准、前置依赖 |
| 3 | `03_Service_Blueprint.md` | 客户、员工、AI 与系统协作方式 |
| 4 | `04_User_Journey_and_Task_Flow.md` | 支撑低保真图和交互流程设计 |
| 5 | `05_Feature_Breakdown.md` | 功能拆为可设计、可开发、可测试模块 |
| 6 | `06_Wireframe_Design_Spec.md` | 页面结构、组件、状态与交互 |
| 7 | `07_AI_Agent_Workflow.md` | AI Agent 职责边界和编排逻辑 |
| 8 | `08_API_Integration_Spec.md` | 系统如何打通 |
| 9 | `09_Data_Mapping.md` | 邮件、附件、OCR、Xero、催票状态字段 |
| 10 | `10_Decision_Rules_and_Human_Gates.md` | 何时自动、何时人工确认、何时升级 |
| 11 | `11_UAT_Test_Cases.md` | 验收测试 |
| 12 | `12_KPI_Measurement_Plan.md` | PoC 价值衡量 |
| 13 | `13_Risk_Dependency_Log.md` | API、数据、合规、采用风险 |
| 14 | `14_Open_Questions_and_FDE_List.md` | 给 FDE / 客户 / 技术继续确认 |
| 15 | `15_Demo_Script.md` | 客户汇报和产品演示 |

## 3. 文件清单

```text
smart-accounting-agent-design-pack/
├── 00_README.md
├── 01_PRD.md
├── 02_PoC_Plan.md
├── 03_Service_Blueprint.md
├── 04_User_Journey_and_Task_Flow.md
├── 05_Feature_Breakdown.md
├── 06_Wireframe_Design_Spec.md
├── 07_AI_Agent_Workflow.md
├── 08_API_Integration_Spec.md
├── 09_Data_Mapping.md
├── 10_Decision_Rules_and_Human_Gates.md
├── 11_UAT_Test_Cases.md
├── 12_KPI_Measurement_Plan.md
├── 13_Risk_Dependency_Log.md
├── 14_Open_Questions_and_FDE_List.md
└── 15_Demo_Script.md
```

## 4. 设计原则

1. **Workflow-first**：优先解决月结前端流程卡点，而不是展示 AI 对话能力。  
2. **Evidence-first**：每个 AI 判断都能追溯到邮件、附件、OCR、人工确认和 Xero 状态。  
3. **Human-in-the-loop**：会计判断、低置信度结果、金额异常、GST 异常、客户异常状态必须保留人工关卡。  
4. **Exception-ready**：覆盖混乱附件、多页发票、密码文件、低清晰度扫描、缺票、客户延迟回复、Xero 写入失败等异常流。  
5. **PoC 可落地**：第一阶段聚焦 M8 + M9 闭环，不扩展复杂中游会计判断。
