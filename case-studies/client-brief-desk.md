# Client Brief Desk: make the brief reviewable

A small service business needs answers before work can begin. Email threads make it hard to tell which answers are final, what is missing, and which revision someone approved.

[Source and install](https://github.com/memberfixstudio-ind/client-brief-desk) · [Research and alternatives](https://github.com/memberfixstudio-ind/client-brief-desk/blob/main/docs/RESEARCH.md) · [Validation](https://github.com/memberfixstudio-ind/client-brief-desk/blob/main/docs/VALIDATION.md)

![Staff workspace with fictional client briefs](https://raw.githubusercontent.com/memberfixstudio-ind/client-brief-desk/main/docs/dashboard.png)

## The workflow

An administrator creates a brief from a service, website or event preset and assigns an existing WordPress account. The client saves incomplete answers and submits when ready. Staff request specific changes or approve that submitted version. The portal shows only briefs assigned to the signed-in client.

## The engineering decision that matters

Approval is a state transition tied to a version, not a checkbox attached to changing text. Submitted answers are read-only. Updates compare the version under a database row lock; the update and its history entry commit in one transaction. Submission and approval events preserve question-and-answer snapshots. If another tab saved first, the interface retains the local draft and shows the newer version for comparison.

Private staff notes are filtered server-side from client reads, history and exports. WordPress's native privacy exporter and eraser include the client's retained briefs and submission history.

## Why this scope

Existing intake and approval products already solve much of this problem. The research names them. This project offers a focused, text-only WordPress workflow with no hosted account, file-storage subsystem or production package dependency. It reuses WordPress authentication and REST protections.

## Evidence and limits

Real WordPress database tests exercise account isolation, state transitions, stale requests, snapshots and rollback when history writes fail. Browser tests exercise the actual staff/client journey, draft conflicts and mobile layout. See the validation report for exact environments and results.

This is an open-source software release with synthetic test evidence. It has no claimed adoption numbers or measured business impact. It does not send reminders, accept uploads or provide legal electronic signatures. Third-party themes, caching setups and a real customer's workflow still require staging validation.
