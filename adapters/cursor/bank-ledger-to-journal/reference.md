# Reference

This skill is backed by the finance-operation templates already stored in this repository.

## Source Templates

Primary rule files:

- `templates/workspace/financing/workflows/bank-ledger-to-journal/STANDARD_FIELDS.md`
- `templates/workspace/financing/workflows/bank-ledger-to-journal/BUSINESS_CLASSIFICATION.md`
- `templates/workspace/financing/workflows/bank-ledger-to-journal/JOURNAL_DRAFT_TEMPLATE.md`
- `templates/workspace/financing/workflows/bank-ledger-to-journal/MANUAL_REVIEW_TEMPLATE.md`

Supporting finance workspace note:

- `templates/workspace/financing/TOOLS.md`

## How to Use the Templates

### 1. Standard fields template

Use `STANDARD_FIELDS.md` when:

- mapping raw Excel columns into a stable intermediate schema
- deciding required fields
- deciding which missing values trigger manual review

### 2. Business classification template

Use `BUSINESS_CLASSIFICATION.md` when:

- assigning business categories to rows
- deciding confidence levels
- explaining why a row was classified a certain way

### 3. Journal draft template

Use `JOURNAL_DRAFT_TEMPLATE.md` when:

- producing candidate journal entry lines
- separating high-confidence and pending-review outputs
- explaining candidate account choices

### 4. Manual review template

Use `MANUAL_REVIEW_TEMPLATE.md` when:

- building exception queues
- setting review priority
- capturing rule-learning opportunities after review

## Excel Handling Guidance

If an Excel-specific skill like `excel-xlsx` is available, borrow its low-level spreadsheet handling rules:

- use `pandas` for analysis and reshaping
- use `openpyxl` when workbook preservation matters
- protect dates, text IDs, leading zeros, and workbook structure
- do not trust stale cached formulas blindly

This skill does not replace those spreadsheet mechanics. It adds finance-operation workflow on top.

## Recommended Deliverables

Best default deliverables for a bank-ledger task:

1. `normalized_ledger`
2. `business_classification`
3. `journal_draft_high_confidence`
4. `journal_draft_pending_review`
5. `manual_review_queue`
6. `summary`

## Test Workbook Note

If a workbook such as `info1776258323868.xls` is available, use it as a smoke test for:

- field mapping robustness
- `.xls` compatibility
- review-trigger quality
- output sheet structure

If the test workbook cannot be found, proceed with the skill design and ask the user for the exact path before running a live test.
