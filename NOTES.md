# Notes

Things I learned while building WordPress plugins, newest first.

## Daily notes

<!-- NOTES:START -->
### 2026-11-13
An approval must refer to the answers actually reviewed. Client Brief Desk combines version checks and a transaction with preserved question-and-answer snapshots. The browser test opens two tabs, rejects the stale save and verifies that its draft survives loading the newer version.

Hook `load_plugin_textdomain()` on `init`, not `plugins_loaded`: since WordPress 6.7, translating a string before `init` triggers a `_load_textdomain_just_in_time` notice. I added it to Command Deck that way, with a `Domain Path` header pointing at `/languages`.

### 2026-11-12
WooCommerce’s permission regeneration can erase download history. Access Ledger instead changes one verified email field inside a transaction, with a conditional write and an audit record. A separate-process test checks that a concurrent download still consumes its allowance correctly.

### 2026-11-11
`php -l` only checks syntax for the PHP version running it, so a plugin that declares `Requires PHP: 7.4` should lint on 7.4 as well as 8.x: newer syntax like `match` or the `?->` nullsafe operator passes on 8.x and fails on 7.4. I added a GitHub Actions matrix (7.4, 8.1, 8.3) to Member Snapshot for exactly this.

### 2026-11-10
Use `WP_HTML_Tag_Processor` instead of regex when you change a block's rendered HTML: `next_tag( 'details' )`, then `set_attribute( 'name', $group )`, then `get_updated_html()`. `set_attribute()` replaces an existing attribute instead of duplicating it, and Clear FAQ Block uses this to give each accordion its own group name.

### 2026-11-09
`esc_url_raw()` is the right sanitizer for a URL you store or hand to JavaScript, and it strips protocols like `javascript:` because they aren't in `wp_allowed_protocols()`. I added it to Command Deck, so actions from its `command_deck_actions` filter can't open a script URL.

### 2026-11-08
PHP strings and block editor strings are translated separately: `load_plugin_textdomain()` covers PHP, but JS needs `wp_set_script_translations( $handle, $domain, $path )` plus JSON files from `wp i18n make-json`. I added both to Member Snapshot so its card and sidebar controls can be translated.

### 2026-11-08
`<details>` elements that share a `name` attribute act as an accordion: opening one closes the others, with no JavaScript. I used it in Clear FAQ Block, giving each block its own name so two FAQs on a page don't interfere.
<!-- NOTES:END -->

## Weekly recaps

<!-- RECAPS:START -->
### Week of 2026-11-09
Released Access Ledger and its v1.1 reporting update, then Client Brief Desk for text-based client intake and review. Added real WordPress integration tests, browser journeys, release ZIPs, changelogs and public engineering case studies. Research documents existing competing tools.

### Week of 2026-11-02
Released three plugins: Command Deck, Clear FAQ Block and Member Snapshot.
<!-- RECAPS:END -->
