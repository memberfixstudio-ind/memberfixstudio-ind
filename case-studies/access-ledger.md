# Access Ledger: explain a failed download before changing access

A WooCommerce customer has paid, but their download does not work. Regenerating permissions can erase useful history and reset access that should have remained limited.

[Source and install](https://github.com/memberfixstudio-ind/access-ledger) · [Research and reviewer votes](https://github.com/memberfixstudio-ind/access-ledger/blob/main/docs/RESEARCH.md) · [Validation](https://github.com/memberfixstudio-ind/access-ledger/blob/main/docs/VALIDATION.md)

![Access Ledger investigation workspace](https://raw.githubusercontent.com/memberfixstudio-ind/access-ledger/main/docs/dashboard.png)

## The workflow

Find an order, read the diagnosis, then preview a narrowly supported correction. The plugin distinguishes issues such as expiry, exhausted allowances, removed permissions and email mismatches. It corrects a verified email mismatch only after an exact confirmation; it records the change and offers guarded undo.

## The engineering decision that matters

Use WooCommerce's order APIs and change the affected permission's identity field without recreating permission records. A transaction, row locks and conditional writes protect the operation. Download counts and logs remain intact. A separate-process test checks concurrent consumption of a download allowance.

The browser test exercises the native download itself: rejected before correction, available after correction, rejected again after undo. That checks the user-visible outcome as well as the database state.

## v1.1: support teams can reach older findings

The original workspace showed only the latest 50 stored findings. The update adds bounded, cursor-based loading of older findings, keeps search and filters explicitly scoped to loaded rows, and rejects stale cursors after a new scan replaces the previous one. CSV and JSON exports include up to 1,000 findings from the latest scan. CSV cells neutralize spreadsheet formula prefixes.

## Evidence and limits

The repository includes real WordPress/WooCommerce integration tests, fault-injection tests, browser tests and concurrency checks, with exact environments in the validation report. HPOS and the legacy order store are both part of its test strategy.

Diagnostics are not a promise that every access problem can be repaired. Corrections deliberately cover a narrow, verifiable case. A production store still needs a backup and staging validation. Screenshots and test records are synthetic; no client data or customer adoption metrics are presented.
