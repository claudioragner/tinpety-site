# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the static website for **Tinpety** ("a rede social do seu pet" — a social network for pets), an Android app. The site is served via GitHub Pages at **tinpety.com** (see `CNAME`) and exists primarily to host legal/policy pages required by app stores and to verify Android App Links.

There is no build system, package manager, linter, or test suite. The site is plain hand-written HTML — changes are made by editing the HTML files directly and pushing. To preview locally, open a file in a browser or serve the repo root (e.g. `python3 -m http.server`).

## Structure

- `index.html` — minimal landing page linking to the policy pages.
- `logomarcahorizontal.png` — horizontal Tinpety logo shown on the landing page.
- `privacidade/index.html` — Privacy Policy and Terms of Use (Política de Privacidade e Termos de Uso).
- `seguranca-infantil/index.html` — Child Safety Standards (Padrões de Segurança Infantil).
- `404.html` — custom GitHub Pages not-found page linking back to home.
- `.well-known/assetlinks.json` — Android App Links verification for package `app.tinpety`. Contains the app's release SHA-256 certificate fingerprints; edit only when adding/rotating signing certificates, and keep it valid JSON.
- `.nojekyll` — disables Jekyll processing on GitHub Pages (required so `.well-known/` is served). Do not delete.
- `CNAME` — custom domain (`tinpety.com`). Do not delete or modify; GitHub Pages needs it.

## Conventions

- All user-facing content is in **Brazilian Portuguese** (`lang="pt-BR"`); keep new content in Portuguese.
- Each page is fully self-contained: inline `<style>` in the `<head>`, no external CSS/JS, no shared assets. When editing one policy page's styles, mirror the change in the other — `privacidade/` and `seguranca-infantil/` intentionally share the same look.
- Shared visual identity: primary purple `#6200ea`, heading color `#1a1a2e`, body text `#212121`, `.highlight` boxes in `#f3e5f5`/`#4a148c`, Roboto/Arial font stack, centered max-width layout.
- Pages live in directories as `index.html` (e.g. `/privacidade/`) so URLs are clean, extension-less paths. Follow this pattern for new pages, and link them from `index.html`.
