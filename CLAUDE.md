# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Marketing/docs website for [ssl-toolkit](https://github.com/russmckendrick/ssl-toolkit), a Rust-based SSL/TLS certificate diagnostic CLI tool. Single-page static site deployed to Cloudflare Pages at https://ssl-toolkit.dev.

## Commands

- **Package manager**: Use `pnpm` (not npm/yarn)
- **Dev server**: `pnpm dev` (serves at localhost:4321)
- **Build**: `pnpm build` (outputs to `dist/`)
- **Preview**: `pnpm preview`

No test suite or linter is configured.

## Tech Stack

- **Astro 5** — static site generator, no SSR (`output: 'static'`)
- **Tailwind CSS v4** — via `@tailwindcss/vite` Vite plugin (NOT `@astrojs/tailwind`, which is Tailwind v3 only)
- **Cloudflare adapter** — `@astrojs/cloudflare` for Pages deployment
- **TypeScript** — strict config extending `astro/tsconfigs/strict`
- **No UI framework** — pure Astro components with vanilla JS `<script>` blocks

## Architecture

Single-page site (`src/pages/index.astro`) that imports section components in order:

`Hero` → `Terminal` → `Features` → `Installation` → `Usage` → `CliReference` → `Footer`

Each component is a self-contained `.astro` file in `src/components/` with its own `<script>` tag for client-side interactivity (copy buttons, tab switching, terminal animation).

### Key Design Details

- **Theme**: Tokyo Night Storm palette defined as CSS custom properties in `src/styles/global.css` under `@theme {}` — all colors use `tokyo-*` naming (e.g., `text-tokyo-blue`, `bg-tokyo-bg-dark`)
- **Terminal component** (`Terminal.astro`): Has a typing animation that cycles through 3 demo scenarios using `insertAdjacentHTML` with inline styles (Tailwind classes don't work on dynamically created elements)
- **Tailwind config**: No `tailwind.config.mjs` — Tailwind v4 uses the `@theme` block in `global.css` for custom tokens
- **Fonts**: JetBrains Mono (Google Fonts) for monospace, system sans-serif for body

## Content Accuracy

The ssl-toolkit CLI is written in **Rust** (not Go). Installation uses `brew tap russmckendrick/tap` before `brew install ssl-toolkit`, and building from source uses `cargo build --release`. Keep CLI flags, subcommands, and examples aligned with the actual tool in the `ssl-toolkit` sibling repo.
