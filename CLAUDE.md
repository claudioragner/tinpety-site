# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the static website for **Tinpety** ("a rede social do seu pet" — a social network for pets), an Android app. The site is served via GitHub Pages at **tinpety.com** (see `CNAME`) and exists primarily to host legal/policy pages required by app stores and to verify Android App Links.

There is no build system, package manager, linter, or test suite. The site is plain hand-written HTML — changes are made by editing the HTML files directly and pushing. To preview locally, open a file in a browser or serve the repo root (e.g. `python3 -m http.server`).

## Structure

- `index.html` — marketing home: sticky header with menu (CSS-only hamburger on mobile via `#menu-toggle` checkbox), hero, feature cards, Google Play CTA, footer linking the policy pages. Play Store links point to `https://play.google.com/store/apps/details?id=app.tinpety` (package from `assetlinks.json`). Uses the logo purple `#5c26ff` via CSS variables on `:root`.
- `logomarcahorizontal.png` — horizontal Tinpety logo shown on the landing page.
- `app-icon.png` — app icon as shown on the Play Store (white outline paw from `LogoPata.png` on a purple `#5c26ff` rounded square, 512×512), used as the home hero image.
- `favicon.png` — site favicon (solid purple paw on transparent background), referenced by every page. Extracted from the paw in `logomarcahorizontal.png`; `LogoPata.png` is the white-outline paw art from the Android app icon, the source for `app-icon.png`.
- `parceria-dog.png` — partner logo (DOG • Go To The Moon, links to https://doggotothemoon.io/) shown in the footer's "Parcerias" column, 128×200 with transparent background.
- `privacidade/index.html` — Privacy Policy and Terms of Use (Política de Privacidade e Termos de Uso).
- `seguranca-infantil/index.html` — Child Safety Standards (Padrões de Segurança Infantil).
- `404.html` — not a plain error page: it is the fallback for App Links URLs like `tinpety.com/pet/{petId}`. Its inline script sends Android users to the app via an `intent://` URL (Play Store as fallback) and shows a download button otherwise. Keep its script working when editing it.
- `.well-known/assetlinks.json` — Android App Links verification for package `app.tinpety`. Contains the app's release SHA-256 certificate fingerprints; edit only when adding/rotating signing certificates, and keep it valid JSON.
- `.nojekyll` — disables Jekyll processing on GitHub Pages (required so `.well-known/` is served). Do not delete.
- `CNAME` — custom domain (`tinpety.com`). Do not delete or modify; GitHub Pages needs it.

## Conventions

- All user-facing content is in **Brazilian Portuguese** (`lang="pt-BR"`); keep new content in Portuguese.
- Each page is fully self-contained: inline `<style>` in the `<head>`, no external CSS/JS, no shared assets. When editing one policy page's styles, mirror the change in the other — `privacidade/` and `seguranca-infantil/` intentionally share the same look.
- `index.html`, `privacidade/` and `seguranca-infantil/` share the same header (logo, menu, "Baixar app" button, CSS-only mobile hamburger) and footer (Documentos, Contato, Parcerias, copyright). The markup and CSS are copied into each page, so a change to the menu or footer must be made in all three. On the policy pages the menu marks the current page with `aria-current="page"` and "Recursos" points to `/#recursos`.
- On the policy pages, the document styles are scoped under `main.doc` so they don't leak into the shared header and footer.
- Policy pages' visual identity: primary purple `#6200ea`, heading color `#1a1a2e`, body text `#212121`, `.highlight` boxes in `#f3e5f5`/`#4a148c`, Roboto/Arial font stack, centered max-width layout.
- Pages live in directories as `index.html` (e.g. `/privacidade/`) so URLs are clean, extension-less paths. Follow this pattern for new pages, and link them from `index.html`.
