# BANK_LEDGER_MANUAL_REVIEW_TEMPLATE.md

## 目标

这份模板用于定义：哪些银行流水或候选分录必须进入人工复核清单，以及复核清单应该如何组织。

`Iris / Finance Operations Lead` 的目标不是消灭人工复核，而是把人工复核压缩到真正值得人工判断的例外项。

## 使用原则

- 所有待人工复核项必须说明原因
- 待人工复核项必须能追溯到原始流水和候选分录
- 复核结论应可回写到规则库或分类映射中
- 同类问题反复出现时，应优先沉淀成规则，而不是永久靠人工兜底

## 建议人工复核清单字段

| 字段名 | 是否必填 | 说明 |
| --- | --- | --- |
| `review_item_id` | 是 | 复核项唯一 ID |
| `source_file_name` | 是 | 来源文件 |
| `source_row_number` | 是 | 来源行号 |
| `transaction_date` | 是 | 交易日期 |
| `summary` | 是 | 原始摘要 |
| `counterparty_name` | 否 | 对方户名 |
| `net_amount` | 是 | 原始净额 |
| `business_type_candidate` | 否 | 当前候选业务类型 |
| `classification_confidence` | 否 | 当前置信度 |
| `review_trigger_type` | 是 | 触发复核的类型 |
| `review_trigger_reason` | 是 | 触发复核的详细原因 |
| `suggested_accounts` | 否 | 候选科目 |
| `suggested_entry_note` | 否 | 候选分录说明 |
| `review_owner` | 否 | 建议复核人 |
| `review_status` | 是 | `pending` / `reviewed` / `returned` |
| `review_result` | 否 | 人工复核结论 |
| `rule_update_needed` | 是 | 是否建议沉淀为规则 |

## 推荐复核触发类型

建议至少支持以下触发类型：

| 触发类型 | 说明 |
| --- | --- |
| `missing_required_field` | 缺少关键字段 |
| `ambiguous_summary` | 摘要模糊 |
| `personal_counterparty` | 对方为个人，业务性质不明确 |
| `multi_match_conflict` | 命中多个业务规则 |
| `large_amount_exception` | 大额异常 |
| `internal_transfer_uncertain` | 疑似内部转账但无法确认 |
| `refund_or_reversal_complex` | 退款/冲销场景复杂 |
| `account_mapping_missing` | 科目映射缺失 |
| `historical_rule_conflict` | 与历史规则冲突 |
| `investment_related_uncertain` | 投资相关资金流向不明确 |
| `capital_injection_related` | 股东注资或资本金性质待确认 |
| `ambiguous_payment_gateway` | 支付机构备付金类渠道交易用途不明 |
| `salary_batch_without_counterparty` | 工资批量支付但缺少对方明细 |

## 样本驱动重点复核场景

基于真实样本，以下场景建议默认进入人工复核：

- `汇款汇入` + `用途=股东注资`：需要确认是资本金、股东借款还是其他往来
- `代发工资` 但缺少对方户名或工资明细：需要确认工资分摊与薪酬清单
- `银联B2B网关支付` 且对方银行为支付机构备付金集中存管账户：需要确认真实业务用途
- `网上汇款` / `汇款汇出` 与个人户名相关但只有模糊用途：需要确认是否为报销、备用金或其他往来

## 建议复核分级

为了便于优先级处理，建议增加 `review_priority`：

- `P1`：高风险，必须优先处理
- `P2`：中风险，当期应处理
- `P3`：低风险，可合并处理

### 建议 P1 场景

- 大额异常资金收支
- 退款/冲销影响收入确认
- 内部转账金额大且对方账户不明
- 投资相关资金但口径未确认
- 可能影响正式财务结论的关键信息缺失

### 建议 P2 场景

- 个人户名交易性质不明确
- 科目候选不唯一
- 同类业务首次出现
- 股东注资或资本金相关交易
- 工资批量支付但缺少明细

### 建议 P3 场景

- 摘要略模糊但总体方向可判断
- 只需补一个辅助字段即可闭环

## 人工复核结论建议格式

每条复核项建议至少记录：

- 最终业务分类
- 最终候选科目或正式分录方向
- 是否可沉淀为规则
- 结论依据
- 处理人
- 处理时间

## 推荐复核清单输出方式

建议分成两张表：

### A. 待处理清单

用于当期复核：

- 所有 `review_status = pending`
- 按优先级排序

### B. 已处理清单

用于追溯和规则沉淀：

- 所有 `review_status = reviewed`
- 记录最终结论和规则沉淀建议

## 建议输出示例结构

```text
review_item_id: RV-20260416-0032
source_file_name: bank_export_april.xlsx
source_row_number: 128
summary: 报销款
counterparty_name: 张三
net_amount: -1580.00
business_type_candidate: staff_reimbursement
classification_confidence: medium
review_trigger_type: personal_counterparty
review_trigger_reason: 对方为个人，且未匹配到员工名单，需要确认是否属于员工报销
suggested_accounts: 管理费用 / 销售费用 / 其他应收款
review_status: pending
rule_update_needed: true
```

## 复核后建议沉淀的内容

以下情况建议在复核结束后更新规则：

- 某一类关键词稳定对应某种业务分类
- 某个对方主体可以稳定识别为客户/供应商/内部账户
- 某类摘要稳定对应某组候选科目
- 某类例外场景应固定进入人工复核

## 最低通过标准

人工复核清单必须做到：

- 每一项都有明确触发原因
- 每一项都能追溯到原始流水
- 每一项都有当前候选判断
- 每一项都能记录最终复核结论
