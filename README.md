## Hi, I'm Rohan 👋

**WordPress developer: custom plugins, Gutenberg blocks, MemberPress/LearnDash.**

I build WordPress tools that are easy to use and look good: plugins and blocks that work the moment they're activated, with no settings page to learn.

### WordPress plugins

| Plugin | What it does |
| --- | --- |
| [**Command Deck**](https://github.com/memberfixstudio-ind/command-deck) | Press ⌘K anywhere in wp-admin to jump to any screen, post, page or user. Forgiving search, recent items, keyboard first. |
| [**Clear FAQ Block**](https://github.com/memberfixstudio-ind/clear-faq-block) | A Gutenberg FAQ block (`block.json` + React). Paste a whole FAQ at once. No front-end JavaScript, FAQ schema built in. |
| [**Member Snapshot**](https://github.com/memberfixstudio-ind/member-snapshot) | One card that shows members their MemberPress plans, renewal dates and LearnDash course progress. Block or shortcode. |

More small plugins, one a week: **[WordPress Toolbox](https://github.com/memberfixstudio-ind/wordpress-toolbox)**

### What I work on

- **Custom plugins:** admin tools, integrations and features built the WordPress way
- **Gutenberg blocks:** custom blocks with clean editor UIs and light front-end output
- **MemberPress and LearnDash:** membership sites, member dashboards, setup and fixes
- **AI setups:** chat assistants, document extraction and workflow automation

### What I'm learning

<!-- LEARNING:START -->
- **2026-11-09:** `esc_url_raw()` is the right sanitizer for a URL you store or hand to JavaScript, and it strips protocols like `javascript:` because they aren't in `wp_allowed_protocols()`. I added it to Command Deck, so actions from its `command_deck_actions` filter can't open a script URL.
- **2026-11-08:** PHP strings and block editor strings are translated separately: `load_plugin_textdomain()` covers PHP, but JS needs `wp_set_script_translations( $handle, $domain, $path )` plus JSON files from `wp i18n make-json`. I added both to Member Snapshot so its card and sidebar controls can be translated.
- **2026-11-08:** `<details>` elements that share a `name` attribute act as an accordion: opening one closes the others, with no JavaScript. I used it in Clear FAQ Block, giving each block its own name so two FAQs on a page don't interfere.
<!-- LEARNING:END -->

[All notes](NOTES.md)

### This week

<!-- WEEKLY:START -->
Released three plugins: Command Deck, Clear FAQ Block and Member Snapshot.
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
