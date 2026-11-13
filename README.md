## Hi, I'm Rohan 👋

**WordPress developer: custom plugins, Gutenberg blocks, MemberPress/LearnDash.**

I build WordPress tools that make difficult work easier: clear interfaces, careful integrations and tests that exercise real WordPress behavior.

### Featured project: Access Ledger for WooCommerce

**A customer paid. Their download fails. Find the reason before resetting their access.**

[Access Ledger](https://github.com/memberfixstudio-ind/access-ledger) gives store teams an order investigation screen, resumable scans and dated findings. It separates expired or exhausted access from mismatches, previews verified email corrections, and keeps an audit trail with guarded undo.

[![Access Ledger support workspace](https://raw.githubusercontent.com/memberfixstudio-ind/access-ledger/main/docs/dashboard.png)](https://github.com/memberfixstudio-ind/access-ledger)

Built with WooCommerce order APIs, HPOS support and transactional writes that preserve download counts and logs. Real WordPress/MySQL tests cover stale previews, refunds, revoked permissions, authorization and concurrent download consumption; a browser test exercises the actual file download before correction, after correction and after undo.

[Install the plugin](https://github.com/memberfixstudio-ind/access-ledger/releases/latest) · [Read the code](https://github.com/memberfixstudio-ind/access-ledger) · [Research and reviewer votes](https://github.com/memberfixstudio-ind/access-ledger/blob/main/docs/RESEARCH.md) · [Test evidence and limits](https://github.com/memberfixstudio-ind/access-ledger/blob/main/docs/VALIDATION.md)

### More WordPress plugins

| Plugin | What it does |
| --- | --- |
| [**Command Deck**](https://github.com/memberfixstudio-ind/command-deck) | Press ⌘K anywhere in wp-admin to jump to any screen, post, page or user. Forgiving search, recent items, keyboard first. |
| [**Clear FAQ Block**](https://github.com/memberfixstudio-ind/clear-faq-block) | A Gutenberg FAQ block (`block.json` + React). Paste a whole FAQ at once. No front-end JavaScript, FAQ schema built in. |
| [**Member Snapshot**](https://github.com/memberfixstudio-ind/member-snapshot) | One card that shows members their MemberPress plans, renewal dates and LearnDash course progress. Block or shortcode. |

More focused tools: **[WordPress Toolbox](https://github.com/memberfixstudio-ind/wordpress-toolbox)**

### What I work on

- **Custom plugins:** admin tools, integrations and features built the WordPress way
- **Gutenberg blocks:** custom blocks with clean editor UIs and light front-end output
- **MemberPress and LearnDash:** membership sites, member dashboards, setup and fixes
- **AI setups:** chat assistants, document extraction and workflow automation

### What I'm learning

<!-- LEARNING:START -->
- **2026-11-13:** Hook `load_plugin_textdomain()` on `init`, not `plugins_loaded`: since WordPress 6.7, translating a string before `init` triggers a `_load_textdomain_just_in_time` notice. I added it to Command Deck that way, with a `Domain Path` header pointing at `/languages`.
- **2026-11-12:** WooCommerce’s permission regeneration can erase download history. Access Ledger instead changes one verified email field inside a transaction, with a conditional write and an audit record. A separate-process test checks that a concurrent download still consumes its allowance correctly.
- **2026-11-11:** `php -l` only checks syntax for the PHP version running it, so a plugin that declares `Requires PHP: 7.4` should lint on 7.4 as well as 8.x: newer syntax like `match` or the `?->` nullsafe operator passes on 8.x and fails on 7.4. I added a GitHub Actions matrix (7.4, 8.1, 8.3) to Member Snapshot for exactly this.
<!-- LEARNING:END -->

[All notes](NOTES.md)

### This week

<!-- WEEKLY:START -->
Built Access Ledger for WooCommerce after three independent reviewers compared the product directions and voted for download-access diagnostics. The release includes a support dashboard, guarded email corrections, integration tests and real-download browser checks. Earlier projects: Command Deck, Clear FAQ Block and Member Snapshot.
<!-- WEEKLY:END -->

### Also building

**[SahlQuote](https://sahlquote.com)** turns a contractor's bill of quantities (PDF) into a draft priced quotation in Excel, in English or Arabic. It's built for UAE building-material suppliers.

### Tools

![WordPress](https://img.shields.io/badge/WordPress-21759B?style=flat&logo=wordpress&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat&logo=php&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![Figma](https://img.shields.io/badge/Figma-F24E1E?style=flat&logo=figma&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-D97757?style=flat&logo=claude&logoColor=white)

### Get in touch

- LinkedIn: [linkedin.com/in/rohan-salave-362475189](https://www.linkedin.com/in/rohan-salave-362475189/)
- Website: [sahlquote.com](https://sahlquote.com)

I'm open to WordPress, MemberPress and LearnDash projects.
