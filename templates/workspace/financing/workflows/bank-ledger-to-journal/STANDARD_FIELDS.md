# BANK_LEDGER_STANDARD_FIELDS.md

## 目标

这份模板用于把不同银行导出的账户台账 Excel，统一整理成 `Iris / Finance Operations Lead` 可处理的标准流水结构。

目标不是直接记账，而是先把原始流水变成结构一致、可追溯、可继续归类和生成分录草稿的中间表。

## 使用范围

适用于：

- 银行账户台账 Excel
- 对公账户流水导出文件
- 银行交易明细表
- 多银行格式统一整理

不适用于：

- 已经生成好的正式会计凭证
- 缺少日期、金额方向或摘要的严重残缺流水
- 无法确认来源的手工拼接流水

## 标准字段

每一行标准流水至少应包含以下字段：

| 字段名 | 是否必填 | 说明 |
| --- | --- | --- |
| `source_file_name` | 是 | 原始文件名，便于追溯 |
| `source_sheet_name` | 否 | 来源工作表名称 |
| `source_row_number` | 是 | 来源行号，便于审计 |
| `bank_account_name` | 是 | 本方银行账户名称 |
| `bank_account_no` | 否 | 本方银行账号 |
| `bank_name` | 否 | 银行名称 |
| `transaction_date` | 是 | 交易日期，建议来自交易时间的日期部分 |
| `transaction_datetime` | 否 | 完整交易时间 |
| `posting_date` | 否 | 记账日期/入账日期 |
| `transaction_id` | 否 | 唯一流水编号等主流水号 |
| `bank_serial_no` | 否 | 银行流水号 |
| `voucher_no` | 否 | 银行回单号/凭证号 |
| `summary` | 是 | 银行摘要原文 |
| `counterparty_name` | 否 | 对方户名 |
| `counterparty_account_no` | 否 | 对方账号 |
| `counterparty_bank` | 否 | 对方开户行 |
| `currency` | 否 | 币种，默认人民币时也建议保留字段 |
| `debit_amount` | 否 | 借方发生额/支出金额 |
| `credit_amount` | 否 | 贷方发生额/收入金额 |
| `net_amount` | 是 | 统一后的净额，收入为正，支出为负 |
| `balance` | 否 | 交易后余额 |
| `usage` | 否 | 用途字段原文 |
| `remark` | 否 | 原始备注 |
| `channel` | 否 | 网银/柜台/代发/平台等 |
| `raw_direction` | 是 | 原始方向字段值 |
| `normalized_direction` | 是 | 统一方向：`inflow` / `outflow` |
| `is_internal_transfer_candidate` | 是 | 是否疑似内部转账 |
| `business_type_candidate` | 否 | 业务归类候选值 |
| `classification_confidence` | 否 | 归类置信度 |
| `requires_manual_review` | 是 | 是否需人工复核 |
| `manual_review_reason` | 否 | 需人工复核原因 |

## 样本验证：兴业银行导出 `.xls`

基于真实样本 `info1776258323868.xls`，当前已确认以下特征：

- 第 1 行是汇总信息，不是表头
- 第 2 行才是正式表头
- 表头中同时提供 `借方金额(支出)` 和 `贷方金额(收入)`
- 同时存在 `记账日期` 与 `交易时间`
- `用途` 与 `备注` 对业务归类很关键，不能忽略

### 样本字段映射建议

| 原始列名 | 建议标准字段 |
| --- | --- |
| `唯一流水编号` | `transaction_id` |
| `银行流水号` | `bank_serial_no` |
| `账号` | `bank_account_no` |
| `户名` | `bank_account_name` |
| `凭证代号` | `voucher_no` |
| `借方金额(支出)` | `debit_amount` |
| `贷方金额(收入)` | `credit_amount` |
| `账户余额` | `balance` |
| `摘要` | `summary` |
| `对方账号` | `counterparty_account_no` |
| `对方户名` | `counterparty_name` |
| `对方银行` | `counterparty_bank` |
| `记账日期` | `posting_date` |
| `交易时间` | `transaction_datetime` + `transaction_date` |
| `用途` | `usage` |
| `备注` | `remark` |

## 标准化规则

### 1. 金额方向统一

不同银行可能有：

- 收入/支出
- 借方/贷方
- 存入/支取
- 来账/往账

统一后必须转换为：

- `normalized_direction = inflow` 表示流入
- `normalized_direction = outflow` 表示流出
- `net_amount > 0` 表示流入
- `net_amount < 0` 表示流出

### 2. 日期字段统一

如果同时存在交易日期和记账日期：

- `transaction_date` 记录实际交易日期
- `posting_date` 记录银行记账日期

如果只有一个日期字段：

- 优先写入 `transaction_date`
- `posting_date` 留空

### 3. 文本字段保留原文

以下字段尽量保留原始文本，不要在标准化阶段过度改写：

- `summary`
- `counterparty_name`
- `remark`
- `raw_direction`

清洗后的分类判断可以另存，不要覆盖原文。

### 4. 缺失值处理

- 日期缺失：必须人工复核
- 金额缺失或方向无法判断：必须人工复核
- 摘要缺失：必须人工复核
- 对方户名缺失：允许进入下一步，但通常应降低归类置信度

### 5. 样本中的方向计算规则

对于当前样本，建议明确使用：

- `debit_amount > 0` → `normalized_direction = outflow`
- `credit_amount > 0` → `normalized_direction = inflow`
- `net_amount = credit_amount - debit_amount`

### 6. 样本中的表头识别规则

如果文件首行包含“本表总笔数”“本表总收入金额”“本表总支出金额”等汇总文本，应跳过该行，以下一行作为正式表头。

## 建议输出结构

建议标准化结果至少保留三类信息：

### A. 原始追溯信息

- 文件名
- sheet 名
- 行号
- 原始摘要
- 原始方向

### B. 标准化字段

- 统一日期
- 统一金额方向
- 统一净额
- 统一账户信息

### C. 下一步处理字段

- 归类候选
- 置信度
- 是否人工复核
- 人工复核原因

## 建议文件命名

如果输出标准化结果，建议命名为：

- `bank_ledger_normalized.xlsx`
- `bank_ledger_normalized.csv`

如果按期间管理，建议命名为：

- `bank_ledger_normalized_YYYYMM.xlsx`
- `bank_ledger_normalized_accountA_YYYYMM.xlsx`

## 最低通过标准

一批流水要进入下一步“业务归类”和“分录草稿生成”，至少应满足：

- 每行都有来源追溯信息
- 每行都有交易日期
- 每行都有净额和统一方向
- 每行都有摘要原文
- 无法判断的行已明确标记人工复核
