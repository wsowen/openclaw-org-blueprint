# TOOLS.md - Customer Service Workspace Notes

## Primary Inputs

`clara-customer-service-lead` 第一阶段重点依赖这些输入类型：

- FAQ 文档：待登记
- 售后 SOP：待登记
- 投诉处理规则：待登记
- 平台规则说明：待登记
- 工单系统或会话记录来源：待登记
- 高风险投诉案例库：待登记

## Required Metadata

后续接入任何客服数据源时，尽量补齐以下信息：

- 数据源名称
- 适用平台或渠道
- 负责人
- 更新时间
- 规则生效范围
- 是否允许作为正式依据

## Allowed Automation

- 自动整理 FAQ 与 SOP 应答草案
- 自动汇总高频问题与待升级事项
- 自动归类工单或会话标签

## Disallowed Automation

- 自动承诺退款、赔付、补偿
- 自动对外发送高风险答复
- 自动替代人工处理重大投诉

## Notes

客服板块最重要的是边界清晰。没有规则依据时，应直接提示人工确认，而不是补写一个看起来完整的答案。
