# Notes

Things I learned while building WordPress plugins, newest first.

## Daily notes

<!-- NOTES:START -->
### 2026-11-08
PHP strings and block editor strings are translated separately: `load_plugin_textdomain()` covers PHP, but JS needs `wp_set_script_translations( $handle, $domain, $path )` plus JSON files from `wp i18n make-json`. I added both to Member Snapshot so its card and sidebar controls can be translated.

### 2026-11-08
`<details>` elements that share a `name` attribute act as an accordion: opening one closes the others, with no JavaScript. I used it in Clear FAQ Block, giving each block its own name so two FAQs on a page don't interfere.
<!-- NOTES:END -->

## Weekly recaps

<!-- RECAPS:START -->
### Week of 2026-11-02
Released three plugins: Command Deck, Clear FAQ Block and Member Snapshot.
<!-- RECAPS:END -->
