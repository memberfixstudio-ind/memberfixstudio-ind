![Rohan Salave — Useful WordPress software](assets/header.svg)

# Rohan Salave — WordPress plugin developer

**WordPress developer: custom plugins, Gutenberg blocks, MemberPress/LearnDash.**

I'm Rohan Salave, the developer behind [MemberFix Studio](https://memberfix.studio/). I build WordPress tools that make everyday work easier: clear interfaces, careful integrations and tests against real WordPress behavior. My open-source projects show the code, the tradeoffs and the release evidence.

[Discuss a WordPress project on LinkedIn](https://www.linkedin.com/in/rohan-salave-362475189/) · [Browse the repositories](https://github.com/memberfixstudio-ind?tab=repositories)

## Open-source WordPress plugins you can install

### Client Brief Desk · WordPress client intake and approvals

**Get the client details you need before the work begins.** A private workspace for project briefs: useful question presets, saved drafts, revision requests and approval of an exact submission. Clients see their own work; staff notes stay private. Conflicting edits preserve the draft instead of silently overwriting it.

[![Client Brief Desk workspace with fictional demo records](https://raw.githubusercontent.com/memberfixstudio-ind/client-brief-desk/main/docs/dashboard.png)](https://github.com/memberfixstudio-ind/client-brief-desk)

[Install v1.0](https://github.com/memberfixstudio-ind/client-brief-desk/releases/latest) · [Source](https://github.com/memberfixstudio-ind/client-brief-desk) · [Engineering case study](case-studies/client-brief-desk.md) · [Tests and limits](https://github.com/memberfixstudio-ind/client-brief-desk/blob/main/docs/VALIDATION.md)

### Access Ledger · investigate failed WooCommerce downloads

**A customer paid. Their download fails. Find the reason before changing their access.** Diagnose orders, scan for problems, preview a verified email correction and keep an audit trail with guarded undo. **v1.1** adds older findings, clear search scope and spreadsheet-safe CSV export.

[![Access Ledger support workspace](https://raw.githubusercontent.com/memberfixstudio-ind/access-ledger/main/docs/dashboard.png)](https://github.com/memberfixstudio-ind/access-ledger)

[Install v1.1](https://github.com/memberfixstudio-ind/access-ledger/releases/latest) · [Source](https://github.com/memberfixstudio-ind/access-ledger) · [Engineering case study](case-studies/access-ledger.md) · [Tests and limits](https://github.com/memberfixstudio-ind/access-ledger/blob/main/docs/VALIDATION.md)

### Focused tools

| Project | Useful for | Built with |
| --- | --- | --- |
| [Command Deck](https://github.com/memberfixstudio-ind/command-deck) | Find admin screens and content with forgiving keyboard search | WordPress REST API · JavaScript |
| [Clear FAQ Block](https://github.com/memberfixstudio-ind/clear-faq-block) | Paste and edit an FAQ; publish native accordions without front-end JavaScript | `block.json` · React · PHP |
| [Member Snapshot](https://github.com/memberfixstudio-ind/member-snapshot) | Show membership plans and course progress in one card | MemberPress · LearnDash · block/shortcode |
| [WordPress Toolbox](https://github.com/memberfixstudio-ind/wordpress-toolbox) | Small, focused WordPress utilities, such as [Notice Tray](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/notice-tray) for tidying admin notices and [Session Watch](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/session-watch) for reviewing and ending user sessions | PHP · WordPress APIs |

## How I approach the work

- **Start with the task:** make the next action clear, including errors, empty states and keyboard use.
- **Protect the data:** check permissions server-side, make changes explicit and preserve history where it matters.
- **Test the outcome:** exercise real WordPress behavior, including failures and concurrent edits.
- **Show the boundaries:** publish install instructions, changelogs, research, tests and known limits with the code.

Open to custom WordPress plugins, Gutenberg blocks, WooCommerce troubleshooting, MemberPress and LearnDash projects.

## What I'm learning

<!-- LEARNING:START -->
- **2026-11-28:** Treat whatever `apply_filters()` returns as untrusted input: any callback can hand back a string, `null` or a negative number, so cast and clamp it at the point of use, e.g. `$days = max( 0, (int) apply_filters( 'my_plugin_days', 14, $row ) );`. I did that for the new `member_snapshot_ending_soon_days` filter in Member Snapshot, which lets a site change how early a plan is flagged "ending soon".
- **2026-11-27:** A `render_block` filter can run more than once for the same block in one request, for example when something runs the content filters again, so side effects like collecting schema data should be idempotent: key the collected entries, e.g. `$items[ md5( wp_json_encode( $entry ) ) ] = $entry;`, and return `array_values( $items )`. Clear FAQ Block now does this, so a repeated render lists each question in its FAQ schema once.
- **2026-11-26:** Listen for `pageshow` and check `event.persisted` when a page can be restored from the browser's back/forward cache: restored pages skip `DOMContentLoaded` and keep their JavaScript state, so a "submitted" flag set to stop double clicks leaves the button locked after Back. I added that reset to Session Watch's sign-out buttons, and passed a function to `.replace( '%s', () => name )` so a `$&` in a display name isn't read as a replacement pattern.
<!-- LEARNING:END -->

[All development notes](NOTES.md)

## This week

<!-- WEEKLY:START -->
This week I shipped [Members Only](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/members-only), a block that shows the blocks inside it only to signed-in or signed-out visitors, chosen roles, MemberPress members or LearnDash students, because WordPress's own block visibility can hide a block but can't tell who is signed in. Clear FAQ Block's paste import no longer trims questions that start with "A-" or "A.", Member Snapshot shows a fallback title for untitled memberships and courses and gained a `member_snapshot_ending_soon_days` filter, Session Watch's buttons unlock again after a Back-button restore, and Command Deck got a CI workflow that checks its PHP and JavaScript syntax. Three of this week's seven notes went into code: the `pageshow` reset in Session Watch, idempotent FAQ schema collection in Clear FAQ Block, and casting filtered values in Member Snapshot (and in Members Only's own filters).
<!-- WEEKLY:END -->

## Also building

[**SahlQuote**](https://sahlquote.com) turns a contractor's bill of quantities into a draft priced quotation in Excel, in English or Arabic, for UAE building-material suppliers.

**Main stack:** WordPress · PHP · JavaScript · React · Gutenberg · WooCommerce · MemberPress · LearnDash

[MemberFix Studio](https://memberfix.studio/) · [LinkedIn](https://www.linkedin.com/in/rohan-salave-362475189/) · [SahlQuote](https://sahlquote.com)
