---
name: bank-ledger-to-journal
description: Convert bank ledger Excel exports into standardized ledger rows, business classifications, journal entry drafts, and manual review queues for finance operations. Use when working with bank statements, bank ledger spreadsheets, account transaction exports, bookkeeping draft entries, or `.xls`/`.xlsx` bank files.
---
# Bank Ledger To Journal

## When to Use

Use this skill when the user wants to turn a bank ledger, bank statement export, or account transaction spreadsheet into finance-operation outputs such as:

- standardized bank ledger rows
- business classification results
- journal entry drafts
- manual review queues

Typical triggers:

- "银行流水转分录"
- "账户台账整理成记账分录"
- "bank ledger to journal entries"
- "process this `.xls` / `.xlsx` bank export"

## Core Rules

- Treat the source workbook as evidence. Keep file name, sheet name, and row traceability.
- Do not write final accounting conclusions when only a draft is supported.
- Separate four stages clearly: standardize, classify, draft, review.
- Mark uncertainty explicitly instead of guessing.
- Preserve Excel reliability: protect dates, numeric precision, leading zeros, and workbook structure.

## Workflow

Copy this checklist and work through it:

```text
Progress:
- [ ] Step 1: Inspect workbook and identify source sheets
- [ ] Step 2: Normalize rows into the standard ledger schema
- [ ] Step 3: Classify transactions into business types
- [ ] Step 4: Generate journal entry drafts
- [ ] Step 5: Build the manual review queue
- [ ] Step 6: Summarize output files, exceptions, and next actions
```

### Step 1: Inspect workbook

- Identify workbook type: `.xls`, `.xlsx`, `.xlsm`, `.csv`.
- For legacy `.xls` bank exports, `xlrd` is a practical first-read option when the goal is structure inspection.
- Decide tool by job:
  - use `pandas` for reshaping and analysis
  - use `openpyxl` when workbook structure, formulas, styles, or sheet preservation matter
- Record:
  - source file name
  - relevant sheet names
  - likely header row
  - obvious date, direction, amount, and balance columns
- If the workbook is messy, first produce a field-mapping note before changing data.
- Do not assume the first row is the header. Some bank exports put totals or summary text above the real header row.

### Step 2: Normalize rows

Follow the standard schema in [reference.md](reference.md).

Minimum required outputs per row:

- source traceability
- transaction date
- summary
- normalized direction
- net amount
- manual review flag

Rules:

- keep original text fields where possible
- normalize amount direction into `inflow` / `outflow`
- keep identifiers and account-like values as text when precision may be damaged
- if date, direction, amount, or summary is missing, mark the row for manual review

### Step 3: Classify business type

Follow the classification rules in [reference.md](reference.md).

For each row, output:

- `business_type_candidate`
- `classification_confidence`
- `classification_basis`
- `requires_manual_review`
- `manual_review_reason`

Do not force a category when evidence is weak. Use `other_or_unknown` when needed.

### Step 4: Generate journal drafts

Follow the journal draft rules in [reference.md](reference.md).

For each draft line, keep:

- source traceability
- business type
- candidate debit / credit accounts
- amount
- explanation
- review flag

If the company accounting policy is missing, present candidate accounts instead of pretending there is a final answer.

### Step 5: Build the manual review queue

Use the review triggers in [reference.md](reference.md).

Always include:

- review trigger type
- review trigger reason
- candidate business type
- candidate accounts if available
- whether the result should become a future rule

### Step 6: Deliver outputs

Preferred output set:

- normalized ledger table
- business classification table
- journal draft table
- manual review queue
- short summary of unresolved issues

If the user asked for a single workbook, create separate sheets instead of mixing everything into one flat sheet.

## Output Expectations

When reporting back to the user, summarize:

- how many rows were processed
- how many rows classified with high / medium / low confidence
- how many rows need manual review
- which business types appeared most
- whether the workbook was preserved or a new output file was created

## Additional Resources

- Use [reference.md](reference.md) for the rule sources and file mapping.
- Use [examples.md](examples.md) for suggested output shapes.
