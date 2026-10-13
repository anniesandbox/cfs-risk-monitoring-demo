# CFS Risk Monitoring — Flow Review Plan

## Objective

Compare two Power Automate cloud flow implementations for the simulated CFS financial control `CFS-FIN-001 — Duplicate Payment & Transaction Anomaly`.

## Flow A — Messy Version

Planned flow name: `CFS-FIN-001 - Transaction Check - Messy`

Characteristics:
- Retrieves transactions from SharePoint.
- Checks whether transaction amount exceeds RM10,000.
- Logs results to the Monitoring Results SharePoint list.
- Does not properly validate missing invoice numbers or invalid amounts.
- Does not detect duplicate transactions.
- Uses a static RunID rather than a unique ID for each execution.
- Has limited error handling.

## Flow B — Robust Version

Planned flow name: `CFS-FIN-001 - Transaction Check - Clean`

Intended improvements:
- Generates a unique RunID for each execution.
- Validates missing invoice numbers.
- Flags amounts less than or equal to RM0.
- Flags transactions above RM10,000.
- Detects potential duplicates using VendorID, InvoiceNumber and Amount.
- Logs results to SharePoint with ControlCode, MonitoringStepID, TransactionID and RunID.
- Uses TRY, CATCH and FINALLY scopes with Configure run after for error handling.

## Simulated Business Rules

1. Duplicate: same VendorID, InvoiceNumber and Amount across different TransactionIDs.
2. High value: Amount greater than RM10,000.
3. Missing invoice: InvoiceNumber is blank.
4. Invalid amount: Amount is less than or equal to RM0.

These rules are for sandbox learning only and are not confirmed production CFS policy.

## Review Questions

1. What are the design weaknesses of Flow A?
2. Does Flow B correctly implement every business rule?
3. Are there edge cases or logical errors in the duplicate detection?
4. Is the TRY/CATCH/FINALLY pattern configured correctly?
5. Are SharePoint results sufficient for auditability and troubleshooting?
6. What should be improved before considering a production deployment?

Important: Do not claim to have inspected either flow's actual implementation until its exported definition is available in the repository.
