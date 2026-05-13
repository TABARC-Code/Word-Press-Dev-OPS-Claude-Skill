---
name: wordpress-studio
description: >
  Expert WordPress development skill for building production-grade themes, plugins, Gutenberg
  blocks, WooCommerce features, REST API endpoints, and Full Site Editing (FSE) solutions.
  Use this skill whenever the user asks about WordPress, WooCommerce, Gutenberg, ACF, hooks,
  filters, custom post types, plugin architecture, block development, WordPress security,
  WordPress performance, WP-CLI, or any custom WordPress PHP/JS implementation.
  Also triggers for: debugging WordPress code, reviewing plugin structure, sanitisation and
  escaping questions, nonce handling, capability checks, database queries via $wpdb, enqueue
  patterns, child themes, template hierarchy, and block patterns.
  Always use this skill when the task involves any WordPress file, function, hook, or
  WooCommerce feature — even if the user frames it as a general PHP or JavaScript question.
triggers:
  - WordPress
  - WooCommerce
  - Gutenberg
  - WordPress plugin
  - WordPress theme
  - custom blocks
  - ACF
  - WordPress REST API
  - hooks and filters
  - WordPress security
  - WordPress performance
  - WP-CLI
  - Full Site Editing
  - FSE
  - block patterns
  - wp_enqueue
  - $wpdb
  - nonce
  - sanitize
  - escape output
  - custom post type
  - taxonomy
  - Git
  - deployment
  - staging
  - local development
  - DDEV
  - accessibility
  - WCAG
  - responsive design
  - ACF
  - get_field
  - Gravity Forms
  - site migration
  - headless WordPress
  - multisite
  - wp-config
role: senior-developer
scope: full-stack-wordpress
output-format: code-with-explanation
version: 1.0.0
author: TABARC-Code / Blackwood Studio
linked-skills:
  - professional-technical-writing
  - skill-creator
  - alchemy-hive
  - boardgame-design-hydra
  - humanizer
---

# WordPress Studio

Senior WordPress development skill. Builds secure, scalable, production-grade WordPress
solutions following WPCS, OWASP, and modern PHP/JS standards. Covers the full development
lifecycle from architecture through deployment.

---

## Skill Network

This skill operates within a bidirectional network. All link contracts, data flows,
and cross-link definitions are defined canonically in `references/skill-network.md`.

The summary below is a quick reference. `references/skill-network.md` is the
authoritative source. If the two ever diverge, skill-network.md takes precedence.

| Linked Skill | Activation Condition |
|---|---|
| `professional-technical-writing` | Any user-facing text, readme, PHPDoc, admin copy |
| `skill-creator` | Building a WordPress-wrapping skill; skill self-audit |
| `alchemy-hive` | Site architecture, CPT slugs, taxonomy design, SEO alignment |
| `boardgame-design-hydra` | Rule/state/scoring logic; game companion plugins |
| `humanizer` | Any generated prose before final output |

Full relationship definitions, data contracts, and cross-links: `references/skill-network.md`.

---

## Core Principles

Apply these before writing a single line of code.

**1. WordPress first.** Use WordPress APIs. Never roll your own when a core function exists.

**2. Security by default.** Every input sanitised. Every output escaped. Every form nonced.
Every capability checked. Every database query prepared. No exceptions, no shortcuts.

**3. Hooks over modification.** Extend through actions and filters. Never modify core files.

**4. Standards compliance.** WPCS (WordPress Coding Standards) throughout. PSR-12 is not
the WordPress standard — know the difference.

**5. i18n from the start.** Every user-facing string wrapped in `__()`, `_e()`, or
equivalent. Text domains registered correctly.

**6. Backward compatibility awareness.** Target WordPress 6.4+, PHP 8.1+. Note when a
feature requires a higher minimum.

**7. Document contracts.** Every function gets a PHPDoc block. Every hook documents its
arguments. Every filter documents its expected return type.

---

## Workflow

### Phase 1 — Analyse

- Identify WordPress version, PHP version, active theme/plugin context
- Check whether WooCommerce, ACF, or other major plugins are in scope
- Identify existing hooks, post types, taxonomies already registered
- Note constraints: multisite, hosting environment, existing architecture
- Identify deployment target: local dev, staging, or production
- Confirm accessibility requirements: WCAG 2.1 AA is the professional baseline

### Phase 2 — Architect

- Plan file structure before writing code (see `references/plugin-architecture.md`)
- Design hook strategy: which actions/filters to use or register
- Define data flow: how data enters, is stored, is retrieved, is output
- Identify security surface: all inputs, all outputs, all capability gates

### Phase 3 — Implement

- Build to WPCS
- Security layer first: nonces, sanitisation, escaping, capability checks
- Database layer: `$wpdb->prepare()` always, never raw queries
- Enqueue layer: all scripts/styles via `wp_enqueue_scripts` or `admin_enqueue_scripts`
- Hook layer: priorities explicit, unhookable by downstream developers
- Front-end layer: mobile-first CSS, semantic HTML5, correct image sizing with alt text
- Accessibility layer: keyboard nav, ARIA only where semantic HTML is insufficient,
  colour contrast, form labels (see `references/accessibility.md`)

### Phase 4 — Optimise

- Transients for expensive queries
- Object cache where available
- Conditional asset loading (only enqueue where needed)
- Query optimisation: avoid `query_posts()`, use `WP_Query` correctly

### Phase 5 — Document and Test

**Documentation:**
- PHPDoc on all functions and classes
- Inline comments for non-obvious logic only (explain why, not what)
- Compatibility notes for version-specific features
- If documentation is user-facing: apply `professional-technical-writing` standards
  (see `references/documentation-standards.md`)

**Testing:**
- Manual: activate/deactivate without errors; test with WP_DEBUG enabled
- Compatibility: test on minimum WordPress version declared in plugin header
- Multisite: test on a multisite install if the plugin declares network support
- WooCommerce: if HPOS-compatible, test with HPOS both enabled and disabled
- Security: run PHPCS with WordPress-Extra and Security ruleset before shipping
- Browser: test admin UI in Chrome and Firefox; check for JS console errors
- PHP version: test on the minimum PHP version declared in plugin header
- Unit: PHPUnit with WP_Mock for isolated logic tests — prioritise security
  functions and business logic, not boilerplate getter/setter functions

---

## Reference Guide

Load these references based on task context. Do not load all at once.

| Reference | Load When |
|---|---|
| `references/plugin-architecture.md` | Building or auditing a plugin from scratch |
| `references/theme-development.md` | Theme files, template hierarchy, child themes, FSE |
| `references/gutenberg-blocks.md` | Block dev, block.json, Interactivity API, dynamic blocks |
| `references/hooks-filters.md` | Registering or using actions/filters, hook priorities |
| `references/security.md` | Any security question, code review, capability checks |
| `references/woocommerce.md` | WooCommerce hooks, HPOS, product/order API, payment gateways |
| `references/rest-api.md` | Custom endpoints, authentication, schema design |
| `references/performance.md` | Caching, query optimisation, asset optimisation |
| `references/documentation-standards.md` | User-facing strings, readme files, inline docs |
| `references/git-workflow.md` | Git setup, local dev, CI/CD deployment, site migration |
| `references/accessibility.md` | WCAG 2.1 AA, ARIA, keyboard nav, accessible blocks |
| `references/frontend.md` | Responsive CSS, SCSS, JS ES6+, ACF, Gravity Forms |
| `references/skill-network.md` | Full bidirectional link specifications |

---

## Security Checklist

Run this mentally before finalising any code output.

- [ ] All superglobal values (`$_GET`, `$_POST`, `$_REQUEST`, `$_COOKIE`) passed through `wp_unslash()` then the narrowest appropriate sanitisation function
- [ ] All output escaped with `esc_html()`, `esc_attr()`, `esc_url()`, `esc_js()`, `wp_kses()`
- [ ] Forms include a nonce field (`wp_nonce_field()`)
- [ ] AJAX handlers verify nonce (`check_ajax_referer()` or `wp_verify_nonce()`)
- [ ] REST endpoints include permission callback
- [ ] All database queries that include variable data use `$wpdb->prepare()` (static queries with no user input do not require it)
- [ ] File operations check `ABSPATH` is defined
- [ ] Uploads handled through `wp_handle_upload()`
- [ ] Capability checks before any admin action (`current_user_can()`)
- [ ] No raw PHP short tags
- [ ] No `extract()` calls
- [ ] No `eval()`
- [ ] Direct file access blocked (`defined('ABSPATH') || exit;`)

---

## MUST DO

- Follow WordPress Coding Standards throughout
- Sanitise every user input with the narrowest appropriate function
- Escape every output at the point of output
- Use prepared statements for every database query
- Implement proper capability checks
- Enqueue scripts and styles through WordPress APIs only
- Use hooks for extension points — never hardcode logic that should be filterable
- Write translatable strings with correct text domains
- Register custom tables with `dbDelta()` on activation
- Test across multiple WordPress versions before shipping
- Use Git for all custom code — never deploy from local directly to production
- Meet WCAG 2.1 AA as the accessibility baseline unless the brief explicitly states otherwise
- Confirm site loads correctly on mobile viewport before shipping

## MUST NOT DO

- Modify WordPress core files
- Use PHP short open tags (`<?`) — note: `<?=` (short echo) is always available in PHP 7+ and is acceptable in template files only; prefer full tags in plugin PHP files
- Trust any user-supplied input without sanitisation
- Output any data without escaping
- Hardcode table names without `$wpdb->prefix`
- Skip capability checks in admin-facing functions
- Write raw SQL without `$wpdb->prepare()`
- Bundle libraries already provided by WordPress
- Allow arbitrary file uploads without type checking
- Skip internationalisation strings
- Use `query_posts()` — always use `WP_Query` or `get_posts()`
- Call `wp_head()` or `wp_footer()` directly in plugin code (use hooks)
- Leave `WP_DEBUG_DISPLAY` enabled in any environment serving real users
- Commit `wp-config.php`, `vendor/`, `node_modules/`, or `wp-content/uploads/` to Git
- Run `wp search-replace` without `--precise` when migrating serialised data
- Deploy directly from local to production — always go through staging

---

## Error Handling

WordPress has its own error handling conventions. PHP exceptions are not the default.

**WP_Error** is the standard WordPress error object. Use it for all error states in
functions that can fail: REST API callbacks, data processing, any function called
from multiple contexts.

| Context | On error, use |
|---|---|
| REST API callback | Return `WP_Error` with status code in data array |
| AJAX handler | `wp_send_json_error()` then `wp_die()` |
| Admin page action | `wp_die()` for fatal; `add_settings_error()` for recoverable |
| Background process / cron | `error_log()` to a non-web-accessible path; never `wp_die()` |
| Public-facing function | Return `false` or `null`; caller checks return value |
| Database write failure | Check `$wpdb->last_error`; return `WP_Error` |

Never throw uncaught exceptions inside WordPress hooks. An uncaught exception in an
`add_action` callback kills the entire page load. Catch and convert to `WP_Error` or log.

```php
// External API call — safe pattern
function my_plugin_fetch_data( string $url ): array|WP_Error {
    $response = wp_remote_get( esc_url_raw( $url ), [ 'timeout' => 10 ] );

    if ( is_wp_error( $response ) ) {
        return $response;
    }

    $code = wp_remote_retrieve_response_code( $response );
    if ( 200 !== $code ) {
        return new WP_Error(
            'api_error',
            sprintf( __( 'API returned status %d.', 'my-plugin' ), $code ),
            [ 'status' => $code ]
        );
    }

    $body = json_decode( wp_remote_retrieve_body( $response ), true );
    if ( null === $body ) {
        return new WP_Error( 'parse_error', __( 'Could not parse API response.', 'my-plugin' ) );
    }

    return $body;
}

// Caller always checks
$data = my_plugin_fetch_data( $url );
if ( is_wp_error( $data ) ) {
    error_log( 'my-plugin: ' . $data->get_error_message() );
    return;
}
```

---

## Output Templates

Every implementation response must include:

1. Plugin or theme file header with correct WPCS-standard DocBlock
2. All functions namespaced or prefixed to avoid collisions
3. Security layer visible and commented
4. Hook registrations with explicit priority and argument count
5. Brief explanation of WordPress-specific patterns used and why

**Hook registration — always declare priority and accepted argument count:**

```php
// add_action( hook, callback, priority, accepted_args )
add_action( 'save_post_my_item', [ $this, 'handle_save' ], 10, 3 );

// add_filter( hook, callback, priority, accepted_args )
add_filter( 'the_content', [ $this, 'filter_content' ], 20, 1 );
```

**Gutenberg block output format — blocks have a distinct structure:**

When the task involves block development, the output format is:

1. `block.json` — metadata, attributes, supports, file references
2. `index.js` — editor registration and edit component
3. `render.php` (dynamic) or `save.js` (static) — frontend output
4. PHP registration function hooked to `init`
5. Brief explanation of static vs dynamic choice and why

Never produce a block as a PHP shortcode equivalent. Blocks are registered through
the block API. See `references/gutenberg-blocks.md` for full patterns.

---

## Extended Scope

Headless WordPress, multisite architecture, and debugging tools are covered in
`references/git-workflow.md` (debugging constants, deploy patterns) and inline
below as orientation summaries. Full patterns for REST/GraphQL are in
`references/rest-api.md`.

**Headless orientation:** WordPress as content backend; REST API or WPGraphQL
serves a decoupled frontend (Next.js, Nuxt.js, SvelteKit). This skill covers
the WordPress/API side. Authentication: Application Passwords or JWT plugin.
CORS headers must be configured for the frontend domain.

**Multisite orientation:** `is_multisite()` guards network logic.
Use `get_site_option()` / `update_site_option()` for network-wide settings.
Use `switch_to_blog( $id )` + `restore_current_blog()` for per-site operations.
Never hardcode `$wpdb->prefix` — use `$wpdb->get_blog_prefix()` for multisite tables.

**Debugging tools:** `WP_DEBUG` + `WP_DEBUG_LOG` (path outside web root) in dev.
Query Monitor plugin (dev only — remove before deploy). Xdebug for step-through.
`error_log( print_r( $var, true ) )` for quick dumps. Never `WP_DEBUG_DISPLAY`
in any environment serving real users. See `references/git-workflow.md`.

---

## Linked Skill Activation Rules

These rules define when this skill hands off to or pulls from a linked skill.

**> professional-technical-writing**
Activates when generating: readme files, plugin description copy, user-facing admin notices,
inline documentation for public APIs, or any instructional text outside the codebase.
This skill provides: function signatures, parameter types, return values, code structure.
That skill provides back: sentence clarity rules, reader-perspective framing, layout standards.

**> skill-creator**
Activates when: building a new Claude skill that wraps WordPress functionality, or when
auditing this skill's own structure for improvement.
This skill provides: domain-specific implementation patterns, YAML trigger vocabulary,
WordPress context definitions.
That skill provides back: eval loop methodology, description optimisation, link architecture.

**> alchemy-hive**
Activates when: the WordPress work involves content strategy, page role assignment, SEO
intent matching, or site architecture that needs to align with a search ecology.
This skill provides: post type structure, REST endpoint design, URL architecture, taxonomy
relationships.
That skill provides back: Scout/Follower/Memory/Outlier page role assignments, hidden intent
mapping, costly signal identification for content design.

**> boardgame-design-hydra**
Activates when: the plugin handles rule systems, branching logic, state management,
scoring, or structured decision trees. Also activates for: game companion plugins,
digital scorecard tools, campaign tracker plugins, card or deck management systems,
play record tools, tournament bracket systems, or any plugin where the data models
map to game entities (players, scores, turns, phases, outcomes).
This skill provides: custom post type schemas, data modelling patterns, hook-based
event systems, state machine design.
That skill provides back: mechanic balance logic, branching rule clarity, player-state
tracking patterns adaptable to WordPress user/session data.

**> humanizer**
Activates when: code comments, readme text, admin notices, or any generated prose will be
read by end users or clients.
This skill provides: raw generated text for review.
That skill provides back: cleaned copy with AI writing patterns removed, natural prose
alternatives, em-dash reduction.

---

## Feedback Loops

This skill improves through structured feedback. The mechanism is explicit.

**Positive signal inputs — update the relevant reference file's "proven patterns" section:**
- Code passes security review without revision
- Hook architecture survives client modification without breakage
- Documentation rated clear by a non-technical reader without re-explanation

**Negative signal inputs — identify the failure category and act:**

| Failure | Action |
|---|---|
| Security flaw in output | Add the specific vulnerability as a named anti-pattern in `security.md` |
| Hook registered without unhook path | Add to MUST NOT DO list; add example in `hooks-filters.md` |
| Documentation requires re-explanation | Review the documentation-standards.md rule that should have caught it |
| PHP deprecation warning | Update the Knowledge Baseline version note; add to MUST NOT DO |
| HPOS-incompatible order query output | Add specific query to MUST NOT DO; update `woocommerce.md` |
| Missing ABSPATH check in output | Security checklist item reinforced; add to session review |
| Accessibility failure (missing alt, label, keyboard nav) | Add specific pattern to `accessibility.md` anti-patterns |
| wp-config.php or credentials included in Git guidance | Review `git-workflow.md` — this is a critical security failure |
| CSS not mobile-first or responsive breakpoints wrong | Review `frontend.md` breakpoint patterns |

**Session review process:**
After any session that produces a negative signal, re-read the relevant reference file
before the next session begins. The skill does not self-update automatically — the review
is manual and deliberate. Passive improvement does not happen; this process must be
explicitly triggered by a negative signal.

**Author review cadence:** TABARC-Code reviews the skill network after every ten
sessions or after any critical security flaw, whichever comes first.

---

## Knowledge Baseline

WordPress 6.4+, PHP 8.1+, Gutenberg block API (apiVersion 3), WooCommerce 8.x+,
ACF 6.x, REST API v2, WP-CLI 2.x, block.json v3, Interactivity API (WP 6.5+),
Full Site Editing, theme.json v3, block patterns, widget deprecation, WPCS 3.x,
PHPStan Level 6+ compatibility, OWASP Top 10 WordPress mapping, transients API,
object cache, `WP_Query`, `WP_User_Query`, `WP_Term_Query`, `$wpdb`, `wp_options`,
custom database tables via `dbDelta()`, Action Scheduler (WC-bundled).

**Critical version notes:**

WooCommerce 8.2+ — HPOS (custom order tables) is active by default. Direct
`get_post_meta()` on order IDs breaks. Always use `wc_get_order()` and the
Orders API. See `references/woocommerce.md`.

WooCommerce 8.3+ — Cart and Checkout blocks replace legacy shortcodes as default.
Classic checkout hooks (`woocommerce_before_checkout_form` etc.) do not fire in
block checkout. Block checkout integration requires the Store API.

WordPress 6.5+ — Interactivity API is stable for production use. Replaces bespoke
JavaScript in interactive blocks.

FSE vs classic themes — these are not interchangeable. FSE block themes use
`templates/*.html`, `parts/*.html`, and `theme.json`. Classic themes use PHP
template files and `functions.php`. Child theme patterns differ. Always confirm
which is in use before writing template or theme code.

PHP 8.1+ — Fibers, enums, readonly properties, intersection types, and `never`
return type are available. Use them. `mixed` type hint is valid. `null` in union
types is preferred over `?Type` for clarity in complex signatures.

WCAG 2.1 Level AA, ARIA, semantic HTML5, responsive CSS (mobile-first), CSS custom
properties, SCSS, ES6+ JavaScript, Git (branch strategy, .gitignore, deploy workflow),
GitHub Actions, WP-CLI (search-replace, db export/import, core verify-checksums),
local dev environments (DDEV, Lando, Local), staging/production workflow, site
migration (serialised data handling), ACF 6.x (get_field, have_rows, ACF blocks),
Gravity Forms hooks, Query Monitor, WP_DEBUG constants, file permissions,
headless WordPress orientation (REST/GraphQL backend, Next.js/Nuxt.js front end),
WordPress Multisite (is_multisite, network options, network-activated plugins).

Author: TABARC-Code / Blackwood Studio
