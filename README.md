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
- **2026-11-23:** Since WordPress 6.9, `esc_url()` and `esc_url_raw()` prepend `https://` to a schemeless URL when `'https'` is the first entry in `$protocols`, e.g. `esc_url( $url, array( 'https', 'http' ) )`; with the default list they still fall back to `http://`. I haven't needed it in Member Snapshot, whose links all come from `get_permalink()` or filters, but it is the way to handle a bare handle or domain typed into a URL field.
- **2026-11-22:** Setting a block attribute from stale state is easy to get wrong: since WordPress 6.9 the `setAttributes` prop passed to a block's `Edit` component accepts an updater function, so `setAttributes( ( prev ) => ( { items: [ ...prev.items, newItem ] } ) )` always builds on the latest attributes instead of the `items` captured by your closure. I haven't switched Clear FAQ Block's handlers over yet.
- **2026-11-21:** In the Interactivity API, use `data-wp-on-async--click` instead of `data-wp-on--click` when the handler does not need `event.preventDefault()` or `stopPropagation()`: the async version yields to the main thread before running your action, which helps keep Interaction to Next Paint low. If you need the event synchronously, call `yield` after reading it or use `splitTask()` for long work.
<!-- LEARNING:END -->

[All development notes](NOTES.md)

## This week

<!-- WEEKLY:START -->
This week I shipped [Session Watch](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/session-watch), which adds **Users → Signed in** so admins can see every active session with its device, IP address and login time, spot accounts signed in from several IP addresses, and sign out one device, one person or everyone else. Command Deck now ignores Enter while an IME composition is in progress and cancels pending searches when you keep typing, Member Snapshot shows card dates in the site timezone, Notice Tray removes its user meta on uninstall, Clear FAQ Block and Notice Tray gained WordPress.org-format `readme.txt` files, and every toolbox plugin is now linted on PHP 7.4, 8.1 and 8.3. Six of this week's seven notes went into code: the IME guard and `AbortController` in Command Deck, `wp_date()` in Member Snapshot (and Session Watch), `delete_metadata()` on uninstall in Notice Tray, the `readme.txt` fields in Clear FAQ Block, and `wp_admin_notice()` for Session Watch's result messages.
<!-- WEEKLY:END -->

## Also building

[**SahlQuote**](https://sahlquote.com) turns a contractor's bill of quantities into a draft priced quotation in Excel, in English or Arabic, for UAE building-material suppliers.

**Main stack:** WordPress · PHP · JavaScript · React · Gutenberg · WooCommerce · MemberPress · LearnDash

[MemberFix Studio](https://memberfix.studio/) · [LinkedIn](https://www.linkedin.com/in/rohan-salave-362475189/) · [SahlQuote](https://sahlquote.com)
