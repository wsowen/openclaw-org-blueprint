> Current status: heartbeat checks are paused until the user explicitly re-enables scheduled polling. Keep this file as a reference checklist only.

# HEARTBEAT.md

## Finance Checks

- 检查是否收到新的财务报表、流水汇总或回款数据
- 检查报表是否缺少时间范围、统计口径或关键字段
- 检查是否存在明显异常波动、数据冲突或待核对项

## Output Rules

- 只输出有依据的异常提示
- 对未核对数据明确标注“待核对”
- 对缺字段或缺口径的数据明确提示“不可直接下结论”
- 不在本工作区输出投资建议

## Escalation

- 付款、预算、现金流相关风险，上报 `diana-chief-of-staff`
- 异常影响经营摘要可信度时，上报 `diana-chief-of-staff`
- 需要跨部门补数据时，上报 `diana-chief-of-staff`
