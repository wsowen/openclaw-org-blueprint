# TOOLS.md - Finance Operations Workspace Notes

## Primary Inputs

`iris-finance-operations-lead` 第一阶段重点依赖这些输入类型：

- 财务报表：待登记
- 流水汇总：待登记
- 回款台账：待登记
- 成本/费用台账：待登记
- 预算数据：待登记
- 与 CRM/ERP 相关的财务模块：待登记

## Required Metadata

后续接入任何财务数据源时，尽量补齐以下信息：

- 报表名称
- 时间范围
- 统计口径
- 提供人/维护人
- 更新时间
- 是否已核对

## Allowed Automation

- 自动整理财务输入
- 自动提示明显异常、缺项和冲突
- 自动为经营汇总提取已确认的数据点

## Disallowed Automation

- 自动生成正式财务结论
- 自动执行付款、审批、报销、记账
- 自动用估算值补齐缺失指标
- 自动输出投资建议或资产配置建议

## Notes

任何缺少时间范围、统计口径或来源说明的数据，都只能作为待核对信息，不能直接进入正式经营摘要。

## Bank Ledger to Journal Workflow

围绕“银行账户台账 Excel -> 记账分录草稿”这一业务，当前模板已收纳到：

- `workflows/bank-ledger-to-journal/README.md`
- `workflows/bank-ledger-to-journal/RUN_PROTOCOL.md`
- `workflows/bank-ledger-to-journal/STANDARD_FIELDS.md`
- `workflows/bank-ledger-to-journal/BUSINESS_CLASSIFICATION.md`
- `workflows/bank-ledger-to-journal/JOURNAL_DRAFT_TEMPLATE.md`
- `workflows/bank-ledger-to-journal/MANUAL_REVIEW_TEMPLATE.md`
- `workflows/bank-ledger-to-journal/ENTITY_RULES.md`

建议顺序：

1. 先按 `RUN_PROTOCOL.md` 明确本次任务范围和输出要求
2. 再做字段标准化
3. 再做业务归类
4. 再生成候选分录草稿
5. 最后处理人工复核清单并回写规则

这些模板用于生成草稿和复核材料，不直接替代正式入账。

## Working Memory For Bank Ledger Tasks

`iris-finance-operations-lead` 在处理银行流水任务时，应默认遵守以下额外约束：

- 先看 `ENTITY_RULES.md`，优先使用已确认主体和规则映射
- 对 `other_or_unknown`、资本性质、工资缺明细、支付通道类交易默认保守处理
- 结果中必须明确区分“高置信候选分录”和“待人工复核候选分录”
- 人工确认后，应回写规则，而不是只修当前一次输出
