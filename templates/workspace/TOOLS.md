# TOOLS.md - Main Workspace Operational Notes

这里只记录当前项目落地真正需要的环境信息、数据入口和执行说明。

## Confirmed Runtime Context

- OpenClaw 工作目录：`/Users/owensmac/.openclaw`
- 主工作区：`/Users/owensmac/.openclaw/workspace`
- 已注册子工作区：`operating`、`financing`、`investment`
- 当前消息入口：QQ Bot 已启用
- 当前网关模式：本机 `local`

## Agent Map

- `diana-chief-of-staff` → `Diana / Chief of Staff`
- `maya-operations-lead` → `Maya / Operations Lead`
- `iris-finance-operations-lead` → `Iris / Finance Operations Lead`
- `athena-investment-analyst` → `Athena / Investment Analyst`

## First-Phase Data Sources

以下是当前对话中已经明确计划接入的来源类型：

### Documents and SOP

- 公司制度文档：待登记
- 标准流程/SOP：待登记
- 客服常见问题与处理规则：待登记

### Tables and Task Tracking

- Excel/表格台账：待登记
- 任务清单/项目表：待登记
- 运营日报/周报来源：待登记

### Finance Inputs

- 财务报表：待登记
- 流水汇总：待登记
- 预算/成本/回款口径：待登记

### Business Systems

- CRM：待登记
- ERP：待登记
- 其他业务系统：待登记

### Investment Inputs

- 股票、基金、指数、期货行情来源：待登记
- 投资研究资料：待登记
- 自建观察名单：待登记
- 风控约束与禁投清单：待登记

## Evidence Requirements

主工作区在使用任何数据源前，应尽量记录以下信息：

- 数据名称
- 负责人
- 更新频率
- 统计口径
- 可访问方式
- 是否可作为正式依据

## Execution Defaults

第一阶段默认允许自动执行的动作：

- 提醒、催办、跟进
- 日报、周报、经营摘要汇总
- 财务异常提醒
- 制度/SOP 类问答
- 投资标的的资料归纳与分析草案

第一阶段默认不自动执行的动作：

- 正式审批结论
- 对外承诺性消息
- 跨团队强制派单
- 修改业务系统关键数据
- 自动下单或自动给出确定性的投资执行指令

## To Complete

后续应把真实入口按上面的结构补齐，不知道的内容不要猜填。
