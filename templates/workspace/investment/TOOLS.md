# TOOLS.md - Investment Analysis Workspace Notes

## Primary Inputs

`athena-investment-analyst` 第一阶段重点依赖这些输入类型：

- 股票行情：待登记
- 基金净值与基金资料：待登记
- 指数数据：待登记
- 期货行情与合约信息：待登记
- 研究报告与资讯来源：待登记
- 自建观察名单：待登记

## Required Metadata

后续接入任何投资数据源时，尽量补齐以下信息：

- 数据来源
- 覆盖市场
- 更新时间
- 时间区间
- 是否可作为正式依据
- 是否存在延迟

## Allowed Automation

- 自动整理研究资料
- 自动提取分析框架和观察点
- 自动归纳风险提示与待跟踪事项

## Disallowed Automation

- 自动下单
- 自动给出保本、收益承诺
- 自动用未知时间点的数据输出确定性观点

## Notes

在没有可靠实时行情之前，本工作区更适合做结构化研究辅助，不适合做即时交易决策。
