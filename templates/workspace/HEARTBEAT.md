> Current status: heartbeat checks are paused until the user explicitly re-enables scheduled polling. Keep this file as a reference checklist only.

# HEARTBEAT.md

# 主工作区心跳只做“低风险、可追溯、能带来管理价值”的检查。
# 如果缺少数据源或依据不足，应直接记录“无法判断”，不要编造结论。

## Daily Checks

- 检查是否有待处理的关键任务、超期事项和未闭环提醒
- 检查是否收到新的运营日报、周报或经营相关汇总材料
- 检查是否存在需要上报管理层的跨团队卡点

## Finance Checks

- 在有财务报表或流水汇总输入时，检查是否存在明显异常、缺项或口径不一致
- 如果财务数据来源不足，只提示“待补数据”，不要输出推测性的财务判断

## Investment Checks

- 在有行情和研究输入时，检查是否有需要重点关注的市场变化或风险提示
- 如果缺少最新行情或来源不足，只标记“待补行情”，不要输出硬性投资结论

## Customer Service Checks

- 在有客服会话、工单或投诉输入时，检查是否存在高优先级待响应事项
- 对超出 FAQ 或 SOP 的情况，默认标记为需人工确认或升级

## Knowledge Checks

- 优先使用已确认的制度文档和 SOP 回答问题
- 当知识库缺失时，提示“当前无依据，需补充制度或 SOP”

## Escalation

- 任务连续超期且无人响应时，提醒升级
- 财务数据冲突或异常影响经营判断时，提醒升级
- 涉及审批、付款、承诺、重大投诉时，默认提醒人工确认
- 投资分析缺少关键市场数据或超出已知风控边界时，默认提醒人工确认
- 客服投诉、赔付、升级争议超出已知规则时，默认提醒人工确认
