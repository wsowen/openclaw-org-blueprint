# Examples

## Example 1: User asks for a draft workflow

Input:

- "把这份银行流水 Excel 整理成记账分录草稿"

Expected work pattern:

1. inspect workbook structure
2. normalize rows
3. classify business type
4. draft entries
5. output manual review queue

## Example 2: Output summary

```text
Processed rows: 428
High-confidence classifications: 286
Medium-confidence classifications: 91
Low-confidence / unresolved: 51
Manual review items: 64
Top business types:
- sales_receipt: 122
- vendor_payment: 96
- bank_fee: 54
- internal_transfer: 38
Created outputs:
- normalized_ledger.xlsx
- journal_draft_pending_review.xlsx
Main risks:
- 17 personal-counterparty rows need owner confirmation
- 9 internal transfers lack a verified internal account mapping
```

## Example 3: Manual review row

```text
review_item_id: RV-20260416-0032
source_file_name: bank_export_april.xls
source_row_number: 128
summary: 报销款
counterparty_name: 张三
net_amount: -1580.00
business_type_candidate: staff_reimbursement
classification_confidence: medium
review_trigger_type: personal_counterparty
review_trigger_reason: personal name detected but employee match is missing
suggested_accounts: 管理费用 / 销售费用 / 其他应收款
review_status: pending
rule_update_needed: true
```

## Example 4: Sample workbook profile

For a workbook like `info1776258323868.xls`, expect patterns such as:

- row 1 contains totals rather than headers
- row 2 is the true header row
- debit and credit columns are already split as `借方金额(支出)` and `贷方金额(收入)`
- `用途` and `备注` materially improve classification quality
- repeated summaries like `财税库行-税费/社保`, `代发工资`, `网上汇款`, `汇款汇入` should trigger sample-driven rules before generic fallback logic
