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
