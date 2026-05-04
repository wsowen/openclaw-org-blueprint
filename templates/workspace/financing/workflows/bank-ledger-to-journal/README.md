# Bank Ledger To Journal

这个目录承载 `Iris / Finance Operations Lead` 在“银行流水 Excel -> 候选记账分录草稿”这一具体业务上的规则与模板。

它属于 `financing` 板块下的一个具体业务流程，而不是整个板块的通用人格或长期边界文件。

## 适用场景

适用于：

- 银行导出的账户台账 Excel
- 对公账户流水整理
- 从原始流水生成业务归类与候选分录草稿
- 生成人工复核清单

不直接等同于：

- 正式会计凭证
- 正式入账动作
- 最终财务结论

## 文件结构

- `RUN_PROTOCOL.md`：Iris 处理该类任务时的执行协议
- `STANDARD_FIELDS.md`：银行流水标准字段模板
- `BUSINESS_CLASSIFICATION.md`：业务归类规则模板
- `JOURNAL_DRAFT_TEMPLATE.md`：候选分录草稿模板
- `MANUAL_REVIEW_TEMPLATE.md`：人工复核清单模板
- `ENTITY_RULES.md`：已确认主体、稳定规则与待确认事项

## 推荐执行顺序

1. 先按 `RUN_PROTOCOL.md` 明确任务目标、输出包和升级条件
2. 再按 `STANDARD_FIELDS.md` 做字段标准化
3. 结合 `ENTITY_RULES.md` 与 `BUSINESS_CLASSIFICATION.md` 做业务归类
4. 再按 `JOURNAL_DRAFT_TEMPLATE.md` 生成候选分录草稿
5. 最后按 `MANUAL_REVIEW_TEMPLATE.md` 整理人工复核清单

## 设计原则

- 所有结果都必须能追溯到原始流水文件、sheet 和行号
- 不编造业务类型、科目或财务结论
- 分录只输出候选草稿，不直接替代正式入账
- 低置信度与复杂例外项必须进入人工复核流程
- 人工确认结果应优先沉淀回 `ENTITY_RULES.md`
