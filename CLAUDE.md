# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML site for 4229 Oakview Pl, Saanich, BC. No build system, framework, or dependencies. Three pages:

- **[index.html](index.html)** — Public introduction page (property overview, photos, map). Has a subtle "Member login" link at the bottom that opens a password modal.
- **[members.html](members.html)** — Members dashboard hub. Gated by auth. Shows section cards linking to private content (rental listing, utility documents, etc.).
- **[rental.html](rental.html)** — Master bedroom rental listing (price, details, video tour, contact). Gated by auth. Nav links back to `members.html`.

## Development

Open any file directly in a browser — no server required. For live-reload use `npx serve .` or VS Code Live Server.

## Auth Flow

- Auth state: `sessionStorage` key `member = '1'`
- Login modal lives on `index.html`. Correct password → SHA-256 verified → set key → redirect to `members.html`.
- `members.html` and `rental.html` each redirect to `index.html` if the key is missing (checked in a `<script>` tag at the top of `<head>`).
- Logout clears the key and returns to `index.html`.
- **Password**: SHA-256 hash stored as `PASSWORD_HASH` in `index.html`. Default password is `oakview2026`. To change: compute a new SHA-256 hash and replace the constant.

## Adding New Sections to the Members Dashboard

Add a new `.portal-card` div inside `.portal-grid` in `members.html`. Use `<a class="portal-card" href="newpage.html">` for active links or `<div class="portal-card coming-soon">` for placeholders. The `.card-icon`, `h3`, `.card-desc`, and `.card-footer` pattern is consistent across all cards.

## Shared Conventions

- **Brand color** — `#c8762b` (orange-brown) for icons, badges, and CTA buttons.
- **CSS sections** — commented with `/* ── NAME ── */` markers in each file.
- **Images** — all local JPEGs/JPGs in the repo root, referenced by filename.
- **Contact email** — `limata@gmail.com` (hardcoded in mailto links in `rental.html`).
