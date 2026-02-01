# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Marketing and documentation website for [ssl-toolkit](https://github.com/russmckendrick/ssl-toolkit), a Rust-based SSL/TLS certificate diagnostic CLI tool. Deployed to Cloudflare Pages at https://ssl-toolkit.dev.

## Commands

- **Package manager**: Use `pnpm` (not npm/yarn)
- **Dev server**: `pnpm dev` (serves at localhost:4321)
- **Build**: `pnpm build` (outputs to `dist/`)
- **Preview**: `pnpm preview`

No test suite or linter is configured.

## Tech Stack

- **Astro 5** — static site generator with `output: 'static'`
- **Tailwind CSS v4** — via `@tailwindcss/vite` Vite plugin (NOT `@astrojs/tailwind`, which is Tailwind v3 only)
- **Astro Content Collections** — for markdown-based documentation
- **Cloudflare adapter** — `@astrojs/cloudflare` for Pages deployment
- **TypeScript** — strict config extending `astro/tsconfigs/strict`
- **No UI framework** — pure Astro components with vanilla JS `<script>` blocks

## Architecture

### Landing Page (`/`)

Full-page scroll experience with CSS scroll-snap. Three slides in order:

`SlideHero` → `SlideFeatures` → `SlideCTA`

Plus a fixed `ScrollNav` component for navigation dots.

Components are in `src/components/landing/`:
- **SlideHero.astro** — ASCII banner, tagline, install CTA, and terminal demo with typing animation
- **SlideFeatures.astro** — 6 feature cards with mouse-follow glow effect
- **SlideCTA.astro** — Call-to-action with "Read the Docs" button and footer
- **ScrollNav.astro** — Fixed navigation dots with Intersection Observer tracking and keyboard navigation

### Documentation (`/docs/`)

Multi-page documentation using Astro Content Collections.

**Content location**: `src/content/docs/*.md`

Each doc has frontmatter:
```yaml
---
title: Page Title
description: Brief description
order: 1  # Controls sidebar order
---
```

**Current docs**:
1. Getting Started — Quick intro and first steps
2. Installation — Homebrew, GitHub Releases, From Source
3. Usage Examples — Interactive mode, domain checks, CI/CD
4. CLI Reference — Complete options, commands, exit codes

**Components**:
- `src/layouts/DocsLayout.astro` — Main docs layout with sidebar, breadcrumbs, prev/next navigation
- `src/components/docs/Sidebar.astro` — Navigation sidebar with active state

**Routing**:
- `src/pages/docs/index.astro` — Renders getting-started content
- `src/pages/docs/[...slug].astro` — Dynamic routing for all docs

### Key Design Details

- **Theme**: Tokyo Night Storm palette defined as CSS custom properties in `src/styles/global.css` under `@theme {}` — all colors use `tokyo-*` naming (e.g., `text-tokyo-blue`, `bg-tokyo-bg-dark`)
- **Scroll-snap**: Enabled on `html` for landing page, disabled via `.docs-container` class on docs pages
- **Terminal animation**: Uses `insertAdjacentHTML` with inline styles (Tailwind classes don't work on dynamically created elements). Config in `public/config/terminal-demo.json`
- **Tailwind config**: No `tailwind.config.mjs` — Tailwind v4 uses the `@theme` block in `global.css` for custom tokens
- **Fonts**: JetBrains Mono (Google Fonts) for monospace, Inter for body text
- **Prose styles**: Documentation markdown styling defined in `global.css` under `.docs-content`

## Adding New Documentation

1. Create `src/content/docs/your-page.md` with frontmatter (title, description, order)
2. The page automatically appears in sidebar navigation
3. Build will generate `/docs/your-page/` route

## Content Accuracy

The ssl-toolkit CLI is written in **Rust** (not Go). Installation uses `brew tap russmckendrick/tap` before `brew install ssl-toolkit`, and building from source uses `cargo build --release`. Keep CLI flags, subcommands, and examples aligned with the actual tool in the `ssl-toolkit` sibling repo.
