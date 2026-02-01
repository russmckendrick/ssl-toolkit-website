# ssl-toolkit Website

Marketing and documentation website for [ssl-toolkit](https://github.com/russmckendrick/ssl-toolkit), a Rust-based SSL/TLS certificate diagnostic CLI tool.

**Live site:** https://ssl-toolkit.dev

## Features

- **Full-page scroll landing page** with smooth CSS scroll-snap transitions
- **Interactive terminal demo** showcasing ssl-toolkit in action
- **Multi-page documentation** with sidebar navigation
- **Tokyo Night Storm theme** with custom animations and effects

## Tech Stack

- [Astro 5](https://astro.build) — static site generator
- [Tailwind CSS v4](https://tailwindcss.com) — utility-first styling
- [Cloudflare Pages](https://pages.cloudflare.com) — deployment platform
- TypeScript — type-safe components

## Getting Started

### Prerequisites

- Node.js 18+
- pnpm

### Installation

```bash
# Clone the repository
git clone https://github.com/russmckendrick/ssl-toolkit-website.git
cd ssl-toolkit-website

# Install dependencies
pnpm install
```

### Development

```bash
# Start dev server at localhost:4321
pnpm dev
```

### Build

```bash
# Build for production
pnpm build

# Preview production build
pnpm preview
```

## Project Structure

```
src/
├── components/
│   ├── landing/           # Landing page slides
│   │   ├── SlideHero.astro
│   │   ├── SlideFeatures.astro
│   │   ├── SlideCTA.astro
│   │   └── ScrollNav.astro
│   └── docs/              # Documentation components
│       └── Sidebar.astro
├── content/
│   ├── config.ts          # Content collection schema
│   └── docs/              # Markdown documentation
│       ├── getting-started.md
│       ├── installation.md
│       ├── usage.md
│       └── cli-reference.md
├── layouts/
│   ├── Layout.astro       # Base layout
│   └── DocsLayout.astro   # Documentation layout
├── pages/
│   ├── index.astro        # Landing page
│   └── docs/
│       ├── index.astro    # Docs home
│       └── [...slug].astro # Dynamic docs pages
├── styles/
│   └── global.css         # Tailwind + custom styles
└── public/
    └── config/
        └── terminal-demo.json
```

## Styling

The site uses the **Tokyo Night Storm** color palette defined in `src/styles/global.css`:

| Token | Color | Usage |
|-------|-------|-------|
| `tokyo-bg` | `#24283b` | Main background |
| `tokyo-bg-dark` | `#1a1b26` | Darker surfaces |
| `tokyo-text` | `#c0caf5` | Primary text |
| `tokyo-blue` | `#7aa2f7` | Links, accents |
| `tokyo-purple` | `#bb9af7` | Branding, highlights |
| `tokyo-green` | `#9ece6a` | Success states |
| `tokyo-red` | `#f7768e` | Error states |
| `tokyo-cyan` | `#7dcfff` | Secondary accents |
| `tokyo-orange` | `#e0af68` | Warnings |

## Adding Documentation

To add a new documentation page:

1. Create a markdown file in `src/content/docs/`:

```markdown
---
title: Your Page Title
description: A brief description of the page.
order: 5
---

# Your Page Title

Content goes here...
```

2. The page will automatically appear in the sidebar navigation, ordered by the `order` field.

## Deployment

The site deploys automatically to Cloudflare Pages on push to the `main` branch.

## License

MIT License — see the main [ssl-toolkit](https://github.com/russmckendrick/ssl-toolkit) repository for details.
