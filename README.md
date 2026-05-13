# Word-Press-Dev-OPS-Claude-Skill
An LLM skill package for senior-level WordPress development work: plugins, themes, Gutenberg blocks, REST endpoints, WooCommerce integrations, hooks, filters, security review, performance passes, and the usual little fires WordPress throws at you when someone says, “it should only take ten minutes

---

AUTHOR: TABARC-Code

# WordPress Studio Skill

**WordPress Studio** is an LLM skill package for senior-level WordPress development work: plugins, themes, Gutenberg blocks, REST endpoints, WooCommerce integrations, hooks, filters, security review, performance passes, and the usual little fires WordPress throws at you when someone says, “it should only take ten minutes”.

It is designed as a working reference system, not a glossy prompt fragment. The main `SKILL.md` file defines the role, triggers, workflow, security rules, output expectations, and linked-skill behaviour. The supporting Markdown files act as focused reference packs for common development contexts.

This repository is written for GitHub consumption and for people who want the skill to be inspectable before they trust it with production-adjacent code. Which is sensible. Blind trust in tooling is how you inherit a database full of surprises.

---

## What this skill covers

WordPress Studio is aimed at practical implementation and review work across the modern WordPress stack.

| Area | Coverage |
|---|---|
| Plugin architecture | File structure, bootstrapping, activation/deactivation, settings, custom post types, enqueues |
| Theme development | Classic themes, child themes, Full Site Editing, `theme.json`, template hierarchy |
| Gutenberg blocks | `block.json`, static and dynamic blocks, build flow, Interactivity API |
| Hooks and filters | Actions, filters, priorities, accepted arguments, custom hooks, dynamic hook names |
| Security | Sanitisation, escaping, nonces, capabilities, uploads, REST permissions, prepared statements |
| REST API | Controller pattern, route registration, schema, permissions, auth methods, `WP_Error` responses |
| WooCommerce | HPOS-compatible order handling, product APIs, checkout hooks, Store API notes |
| Performance | Transients, object cache, query optimisation, conditional assets, scheduled tasks |
| Documentation | PHPDoc, admin copy, plugin readme structure, human-facing technical writing |

The skill’s general posture is conservative: use WordPress APIs first, escape late, sanitise early, prepare database queries, and do not invent a clever new framework inside a plugin because somebody discovered dependency injection on Tuesday.

---

## Repository contents

Current archive layout:

```text
WP-Developer-CS/
├── SKILL.md
├── README.md
├── Description.md
├── skill-network.md
├── security.md
├── plugin-architecture.md
├── rest-api.md
├── woocommerce.md
├── gutenberg-blocks.md
├── hooks-filters.md
├── performance.md
├── theme-development.md
└── documentation-standards.md
```

### Important path note

`SKILL.md` currently refers to the support files as `references/*.md`, for example `references/security.md` and `references/plugin-architecture.md`.

The archive itself stores those files at the root.

That mismatch should be fixed before release. Either move the support files into a `references/` directory, or update the paths inside `SKILL.md` and `security.md`. The first option is cleaner:

```text
WP-Developer-CS/
├── SKILL.md
├── README.md
├── Description.md
└── references/
    ├── skill-network.md
    ├── security.md
    ├── plugin-architecture.md
    ├── rest-api.md
    ├── woocommerce.md
    ├── gutenberg-blocks.md
    ├── hooks-filters.md
    ├── performance.md
    ├── theme-development.md
    └── documentation-standards.md
```

Tiny detail. Big nuisance. Classic.

---

## Audit summary

Audit date: **13 May 2026**.

Overall verdict: **strong foundation, not release-clean yet**.

The skill has a good spine. It gives the model clear constraints, separates domain references sensibly, and repeatedly reinforces WordPress security behaviour. It also avoids a common failure mode in WordPress code generation: treating WordPress as “generic PHP with a database lying nearby”. That is a point in its favour.

However, a few items need attention before this should be treated as a polished public repo.

| Severity | Finding | Recommended action |
|---|---|---|
| High | Reference path mismatch: `SKILL.md` points to `references/*.md`, but the files are at root. | Move support files into `references/`, or update every path reference. |
| High | Upload-security guidance uses `wp_check_filetype()` where stronger real-type checking is more appropriate. | Prefer `wp_check_filetype_and_ext()` for uploaded files and keep explicit MIME allowlists. |
| High | `security.md` says `wp_delete_file()` validates that a path sits inside uploads. That claim should not be relied on. | Add explicit path validation before deletion and keep deletion restricted to known upload paths. |
| Medium | `security.md` mentions a `wp_rest_nonce()` alias. The safer documented pattern is `wp_create_nonce( 'wp_rest' )`. | Remove the alias claim unless verified against the target WordPress version. |
| Medium | REST permission comments say “never return true”, while public read endpoints may legitimately return `true`. | Reword to: public reads may return `true`; writes must use capability checks. |
| Medium | REST collection examples push prepared response objects into arrays. | Use collection-safe response preparation, or clearly mark the snippet as conceptual rather than drop-in. |
| Medium | Version baseline is useful but aging. WordPress, Gutenberg, WooCommerce, and WPCS move quickly. Quietly, then suddenly loudly. | Add a maintenance note and review against current official docs before major releases. |
| Low | No repository hygiene files yet. | Add `LICENSE`, `CHANGELOG.md`, `CONTRIBUTING.md`, `.editorconfig`, and optional lint configs. |
| Low | Some examples are intentionally abbreviated, but not always labelled as such. | Mark partial patterns as “illustrative” where they omit surrounding class methods or validation. |

---

## Strengths

The skill is most useful because it keeps repeating the right boring things.

That is not an insult. Most production WordPress failures come from ignored boring things: unslashed superglobals, missing capability checks, raw meta queries over swollen datasets, checkout customisations that die the moment block checkout appears, or plugin files with all the architectural discipline of a drawer full of cables.

Particular strengths:

- **Security posture is visible.** The skill foregrounds sanitisation, escaping, nonces, capabilities, and prepared statements.
- **WordPress-native architecture is respected.** Hooks, APIs, activation routines, and enqueue patterns are treated as first-class structures.
- **WooCommerce HPOS is included.** This matters. Legacy order-meta habits are still shambling around in old snippets like something from a low-budget horror film.
- **The reference split is sensible.** Each domain has its own file, so the model does not need to inhale the entire instruction stack for every job.
- **Documentation is not an afterthought.** The skill makes room for PHPDoc, readme structure, admin notices, and end-user copy.

---

## Known limitations

This is a development-assistance skill. It is not a security scanner, a substitute for testing, or a priesthood-approved guarantee that generated code is safe because it contains the word “nonce”.

Use it with a normal engineering workflow:

1. Generate or review the pattern.
2. Run PHPCS with WordPress rulesets.
3. Run static analysis where practical.
4. Test on the declared minimum WordPress and PHP versions.
5. Test with `WP_DEBUG` enabled.
6. Test WooCommerce customisations with HPOS and block checkout where relevant.
7. Read the code like it was written by someone who had not slept. Sometimes it was.

---

## Recommended quality gates

For a public GitHub repo, add a lightweight tooling layer:

```bash
composer require --dev wp-coding-standards/wpcs phpcompatibility/phpcompatibility-wp
```

Suggested checks:

```bash
vendor/bin/phpcs --standard=WordPress .
vendor/bin/phpcs --standard=PHPCompatibilityWP --runtime-set testVersion 8.1- .
```

For Markdown quality, add your preferred linter rather than arguing about bullet spacing in pull requests. Nobody wins that war.

---

## Suggested release checklist

Before tagging `1.0.0`, do the following:

- [ ] Fix the `references/` path mismatch.
- [ ] Re-check all version claims against current WordPress, Gutenberg, WooCommerce, and WPCS documentation.
- [ ] Replace upload-validation guidance with a stricter `wp_check_filetype_and_ext()` pattern.
- [ ] Remove or verify the `wp_rest_nonce()` alias claim.
- [ ] Clarify REST permission callback rules for public reads versus writes.
- [ ] Mark abbreviated examples as partial patterns where needed.
- [ ] Add `LICENSE`.
- [ ] Add `CHANGELOG.md`.
- [ ] Add `CONTRIBUTING.md` if external contributions are wanted.
- [ ] Decide whether linked skills are public dependencies, private concepts, or optional context.

---

## How to use the skill

Use `SKILL.md` as the primary instruction file.

Load additional references only when relevant:

```text
Plugin build or audit       -> plugin-architecture.md
Security review             -> security.md
REST endpoint work          -> rest-api.md
WooCommerce work            -> woocommerce.md
Block development           -> gutenberg-blocks.md
Theme work                  -> theme-development.md
Performance review          -> performance.md
Hook/filter design          -> hooks-filters.md
Documentation output        -> documentation-standards.md
Skill network behaviour     -> skill-network.md
```

The intent is progressive disclosure. A model should not need the WooCommerce payment-gateway notes when it is answering a question about `body_class`. Humans should not either.

---

## Maintenance notes

This repo should be reviewed whenever one of these changes:

- A major WordPress release lands.
- WooCommerce changes checkout, Store API, or HPOS behaviour.
- Gutenberg promotes an experimental API to stable, or removes one.
- WordPress Coding Standards updates its PHP syntax or sniff behaviour.
- A security note in the skill is found to be incomplete, overconfident, or wrong.

The last one is not failure. It is maintenance. Failure is leaving the wrong thing in place because the Markdown looked tidy.

---

## Naming

**WordPress Studio** is the skill name defined in `SKILL.md`.

The uploaded archive name, `WP-Developer-CS`, reads like an internal working title. That is fine for a zip file, but the public GitHub repository would be clearer as one of:

- `wordpress-studio-skill`
- `wp-developer-skill`
- `wordpress-development-skill`

Use the boring name if discoverability matters. Use the poetic one if the repo is part of a wider studio system. There is no universal law here, only search boxes.

---

## Licence

No licence file was included in the uploaded archive.

Add one before publishing. Without a licence, people can read the repo but do not have clear permission to use, modify, or redistribute it. GitHub is full of repos that forgot this. Do not join the pile.

