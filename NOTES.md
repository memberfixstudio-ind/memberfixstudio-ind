# Notes

Things I learned while building WordPress plugins, newest first.

## Daily notes

<!-- NOTES:START -->
### 2026-11-28
Treat whatever `apply_filters()` returns as untrusted input: any callback can hand back a string, `null` or a negative number, so cast and clamp it at the point of use, e.g. `$days = max( 0, (int) apply_filters( 'my_plugin_days', 14, $row ) );`. I did that for the new `member_snapshot_ending_soon_days` filter in Member Snapshot, which lets a site change how early a plan is flagged "ending soon".

### 2026-11-27
A `render_block` filter can run more than once for the same block in one request, for example when something runs the content filters again, so side effects like collecting schema data should be idempotent: key the collected entries, e.g. `$items[ md5( wp_json_encode( $entry ) ) ] = $entry;`, and return `array_values( $items )`. Clear FAQ Block now does this, so a repeated render lists each question in its FAQ schema once.

### 2026-11-26
Listen for `pageshow` and check `event.persisted` when a page can be restored from the browser's back/forward cache: restored pages skip `DOMContentLoaded` and keep their JavaScript state, so a "submitted" flag set to stop double clicks leaves the button locked after Back. I added that reset to Session Watch's sign-out buttons, and passed a function to `.replace( '%s', () => name )` so a `$&` in a display name isn't read as a replacement pattern.

### 2026-11-25
`add_query_arg()` does not URL-encode the values you pass it, so encode each one yourself with `rawurlencode()`, e.g. `add_query_arg( 'redirect', rawurlencode( $back ), $url )`; an unencoded `&` or `#` in a return address will otherwise split or truncate the query string. Only the existing query string of the URL you pass in is re-encoded. Notice Tray's toggle link already does this for its return address.

### 2026-11-24
To print inline JavaScript from PHP, use `wp_print_inline_script_tag( $js, array( 'id' => 'my-data' ) )` (since WordPress 5.7) instead of echoing a `<script>` tag: it runs the attributes through the `wp_inline_script_attributes` filter, so a CSP plugin can add a nonce. Command Deck still echoes its data tag by hand with `wp_json_encode()` and `JSON_HEX_TAG`, so that is a change I could make there.

### 2026-11-23
Since WordPress 6.9, `esc_url()` and `esc_url_raw()` prepend `https://` to a schemeless URL when `'https'` is the first entry in `$protocols`, e.g. `esc_url( $url, array( 'https', 'http' ) )`; with the default list they still fall back to `http://`. I haven't needed it in Member Snapshot, whose links all come from `get_permalink()` or filters, but it is the way to handle a bare handle or domain typed into a URL field.

### 2026-11-22
Setting a block attribute from stale state is easy to get wrong: since WordPress 6.9 the `setAttributes` prop passed to a block's `Edit` component accepts an updater function, so `setAttributes( ( prev ) => ( { items: [ ...prev.items, newItem ] } ) )` always builds on the latest attributes instead of the `items` captured by your closure. I haven't switched Clear FAQ Block's handlers over yet.

### 2026-11-21
In the Interactivity API, use `data-wp-on-async--click` instead of `data-wp-on--click` when the handler does not need `event.preventDefault()` or `stopPropagation()`: the async version yields to the main thread before running your action, which helps keep Interaction to Next Paint low. If you need the event synchronously, call `yield` after reading it or use `splitTask()` for long work.

### 2026-11-20
Since WordPress 6.4, render admin notices with `wp_admin_notice( $message, array( 'type' => 'warning', 'dismissible' => true ) )` instead of hand-written `<div class="notice">` markup: core builds the classes for you, and other code can adjust every notice through the `wp_admin_notice_args` and `wp_admin_notice_markup` filters. That consistent `.notice notice-{type}` markup is also what tools like Notice Tray rely on when they sort notices by severity.

### 2026-11-19
Pass an `AbortController` signal to `wp.apiFetch( { path, signal } )` and call `controller.abort()` when the query changes, then ignore the `AbortError` in your catch handler: a debounced live search can otherwise show a slow response for an older query under the newer one. I added this to Command Deck, which now cancels pending searches when you keep typing or close the palette.

### 2026-11-18
Format a real Unix timestamp with `wp_date( $format, $timestamp )`, not `date_i18n()`: `wp_date()` converts to the site's timezone, while `date_i18n()` expects a timestamp that already has the offset added, so a UTC expiry can show a day early or late. I switched Member Snapshot's renewal, end and "member since" dates to `wp_date()`.

### 2026-11-17
A WordPress.org `readme.txt` is parsed separately from the plugin header, so keep its short description under 150 characters and set `Stable tag` to a real version number (matching the `Version:` header) rather than `trunk`. I added a `readme.txt` to Clear FAQ Block with those fields checked.

### 2026-11-16
When a plugin stores per-user settings, add an `uninstall.php` that calls `delete_metadata( 'user', 0, $meta_key, '', true )`: the last argument deletes that key for every user in one query instead of looping over users. I added it to Notice Tray so its saved "tray off" choice does not outlive the plugin.

### 2026-11-15
`KeyboardEvent.isComposing` (plus `keyCode === 229` for Safari) tells you an IME is mid-composition, so a keydown handler should return early or Enter will fire your action while someone is still confirming a Japanese or Chinese word. I added that guard to Command Deck's result list.

### 2026-11-14
Since WordPress 6.8, `wp_register_block_types_from_metadata_collection( __DIR__ . '/build', __DIR__ . '/build/blocks-manifest.php' )` registers every block from one cached manifest instead of reading each `block.json` from disk; `wp-scripts build --blocks-manifest` generates the file, and 6.7 sites can fall back to `wp_register_block_metadata_collection()`. It matters most for plugins that ship many blocks.

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
### Week of 2026-11-23
This week I shipped [Members Only](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/members-only), a block that shows the blocks inside it only to signed-in or signed-out visitors, chosen roles, MemberPress members or LearnDash students, because WordPress's own block visibility can hide a block but can't tell who is signed in. Clear FAQ Block's paste import no longer trims questions that start with "A-" or "A.", Member Snapshot shows a fallback title for untitled memberships and courses and gained a `member_snapshot_ending_soon_days` filter, Session Watch's buttons unlock again after a Back-button restore, and Command Deck got a CI workflow that checks its PHP and JavaScript syntax. Three of this week's seven notes went into code: the `pageshow` reset in Session Watch, idempotent FAQ schema collection in Clear FAQ Block, and casting filtered values in Member Snapshot (and in Members Only's own filters).

### Week of 2026-11-16
This week I shipped [Session Watch](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/session-watch), which adds **Users → Signed in** so admins can see every active session with its device, IP address and login time, spot accounts signed in from several IP addresses, and sign out one device, one person or everyone else. Command Deck now ignores Enter while an IME composition is in progress and cancels pending searches when you keep typing, Member Snapshot shows card dates in the site timezone, Notice Tray removes its user meta on uninstall, Clear FAQ Block and Notice Tray gained WordPress.org-format `readme.txt` files, and every toolbox plugin is now linted on PHP 7.4, 8.1 and 8.3. Six of this week's seven notes went into code: the IME guard and `AbortController` in Command Deck, `wp_date()` in Member Snapshot (and Session Watch), `delete_metadata()` on uninstall in Notice Tray, the `readme.txt` fields in Clear FAQ Block, and `wp_admin_notice()` for Session Watch's result messages.

### Week of 2026-11-09
This week I shipped [Notice Tray](https://github.com/memberfixstudio-ind/wordpress-toolbox/tree/main/notice-tray), a small plugin that moves the pile of plugin and theme notices off the top of every wp-admin screen into a tray in the admin bar, while errors and "Settings saved" messages stay on the page. Command Deck now validates actions from its filter and loads its translations on `init`, Clear FAQ Block and Member Snapshot load their PHP and block editor translations, and both gained CI workflows that lint the PHP (Member Snapshot on 7.4, 8.1 and 8.3). Three of this week's notes went straight into code: `esc_url_raw()` for filtered URLs and `load_plugin_textdomain()` on `init` in Command Deck, and the multi-version PHP lint matrix in Member Snapshot.

### Week of 2026-11-09
Released Access Ledger and its v1.1 reporting update, then Client Brief Desk for text-based client intake and review. Added real WordPress integration tests, browser journeys, release ZIPs, changelogs and public engineering case studies. Research documents existing competing tools.

### Week of 2026-11-02
Released three plugins: Command Deck, Clear FAQ Block and Member Snapshot.
<!-- RECAPS:END -->
