# Description

AUTHOR: TABARC-Code

**WordPress Studio** is a senior WordPress development skill for building and reviewing production-grade plugins, themes, Gutenberg blocks, REST API endpoints, WooCommerce features, and Full Site Editing work.

It gives an LLM a WordPress-first operating frame: use core APIs, respect hooks and filters, write secure PHP, keep output escaped, handle input properly, document contracts, and avoid the cheerful little shortcuts that become incident reports later.

The skill is structured around a main `SKILL.md` file plus focused reference documents for security, plugin architecture, REST API work, WooCommerce, Gutenberg blocks, hooks and filters, performance, theme development, documentation standards, and linked-skill behaviour.

## Best used for

- Generating WordPress plugin or theme code patterns.
- Reviewing existing WordPress PHP, JavaScript, or block code.
- Designing custom post types, taxonomies, settings pages, and enqueue flows.
- Creating REST API controllers with permission callbacks and schema-aware parameters.
- Handling WooCommerce order, product, checkout, and HPOS-aware development.
- Building Gutenberg blocks with `block.json`, static saves, dynamic rendering, and modern build tooling.
- Improving WordPress security posture around nonces, capabilities, sanitisation, escaping, uploads, and database queries.
- Producing clearer technical documentation, PHPDoc, admin notices, and readme copy.

## Current audit position

The skill has a strong technical core, but the repository is not quite release-clean.

The main issue is structural: `SKILL.md` refers to supporting files under `references/*.md`, while the uploaded archive stores those files at the repository root. Fix that before treating the repo as ready for public use.

A few technical notes also need revision, especially around upload validation, REST nonce wording, and REST permission callback nuance. Nothing catastrophic. Just the normal sediment that gathers when documentation grows faster than its maintenance routine.

## Tone and posture

This skill favours practical WordPress engineering over abstract cleverness. It is security-conscious, API-led, compatibility-aware, and mildly allergic to magic.

It will not replace tests, static analysis, PHPCS, or a developer reading the code before shipping. That is a feature, not a defect. Tools assist; they do not absolve.

## Suggested repository description

Senior WordPress development skill for secure plugins, themes, Gutenberg blocks, REST endpoints, WooCommerce, HPOS, hooks, filters, performance, and documentation.
