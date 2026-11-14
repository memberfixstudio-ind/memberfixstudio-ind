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
| [WordPress Toolbox](https://github.com/memberfixstudio-ind/wordpress-toolbox) | Small, focused WordPress utilities | PHP · WordPress APIs |

## How I approach the work

- **Start with the task:** make the next action clear, including errors, empty states and keyboard use.
- **Protect the data:** check permissions server-side, make changes explicit and preserve history where it matters.
- **Test the outcome:** exercise real WordPress behavior, including failures and concurrent edits.
- **Show the boundaries:** publish install instructions, changelogs, research, tests and known limits with the code.

Open to custom WordPress plugins, Gutenberg blocks, WooCommerce troubleshooting, MemberPress and LearnDash projects.

## What I'm learning

<!-- LEARNING:START -->
- **2026-11-14:** Since WordPress 6.8, `wp_register_block_types_from_metadata_collection( __DIR__ . '/build', __DIR__ . '/build/blocks-manifest.php' )` registers every block from one cached manifest instead of reading each `block.json` from disk; `wp-scripts build --blocks-manifest` generates the file, and 6.7 sites can fall back to `wp_register_block_metadata_collection()`. It matters most for plugins that ship many blocks.
- **2026-11-13:** An approval must refer to the answers actually reviewed. Client Brief Desk combines version checks and a transaction with preserved submission snapshots; a stale tab keeps its draft for comparison.
- **2026-11-13:** Hook `load_plugin_textdomain()` on `init`, not `plugins_loaded`: since WordPress 6.7, translating a string before `init` triggers a `_load_textdomain_just_in_time` notice. I added it to Command Deck that way, with a `Domain Path` header pointing at `/languages`.
<!-- LEARNING:END -->

[All development notes](NOTES.md)

## This week

<!-- WEEKLY:START -->
This week I shipped [Notice Tray](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/notice-tray), a small plugin that moves the pile of plugin and theme notices off the top of every wp-admin screen into a tray in the admin bar, while errors and "Settings saved" messages stay on the page. Command Deck now validates actions from its filter and loads its translations on `init`, Clear FAQ Block and Member Snapshot load their PHP and block editor translations, and both gained CI workflows that lint the PHP (Member Snapshot on 7.4, 8.1 and 8.3). Three of this week's notes went straight into code: `esc_url_raw()` for filtered URLs and `load_plugin_textdomain()` on `init` in Command Deck, and the multi-version PHP lint matrix in Member Snapshot.
<!-- WEEKLY:END -->

## Also building

[**SahlQuote**](https://sahlquote.com) turns a contractor's bill of quantities into a draft priced quotation in Excel, in English or Arabic, for UAE building-material suppliers.

**Main stack:** WordPress · PHP · JavaScript · React · Gutenberg · WooCommerce · MemberPress · LearnDash

[MemberFix Studio](https://memberfix.studio/) · [LinkedIn](https://www.linkedin.com/in/rohan-salave-362475189/) · [SahlQuote](https://sahlquote.com)
