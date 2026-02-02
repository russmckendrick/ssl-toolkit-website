---
title: Getting Started
description: Quick introduction to ssl-toolkit and how to get up and running in seconds.
order: 1
---

# Getting Started

**ssl-toolkit** is a comprehensive SSL/TLS certificate diagnostic tool written in Rust. It provides everything you need to analyze, verify, and troubleshoot SSL/TLS certificates from the command line.

## What ssl-toolkit Does

- **DNS Resolution** — Multi-provider lookups (Google, Cloudflare, OpenDNS) with DNSSEC validation
- **TLS Analysis** — Protocol version detection, cipher suite analysis, and handshake inspection
- **Certificate Operations** — Inspect, verify, and convert certificates between formats
- **WHOIS Lookup** — Domain registration details and expiration monitoring
- **Security Grading** — Automated A+ through F grading based on industry best practices
- **Reports & Export** — HTML reports, JSON output, and iCal expiry reminders

## Quick Install

The fastest way to install ssl-toolkit is via Homebrew:

```bash
brew install russmckendrick/tap/ssl-toolkit
```

For other installation methods, see the [Installation](/docs/installation) page.

## Your First Check

Once installed, run a quick domain check:

```bash
ssl-toolkit -d github.com --non-interactive
```

This runs all available checks on the domain and displays a comprehensive report including:

- DNS resolution from multiple providers
- TLS handshake details and cipher suites
- Certificate chain validation
- WHOIS registration information
- Overall security grade

## Interactive Mode

For a more guided experience, launch ssl-toolkit without any arguments:

```bash
ssl-toolkit
```

You'll be presented with an interactive menu where you can:

1. Check a domain
2. Inspect certificate file(s)
3. Verify certificate & key pairs
4. Convert certificate formats

Use the arrow keys to navigate and Enter to select.

## Next Steps

- [Installation](/docs/installation) — Detailed installation instructions for all platforms
- [Usage Examples](/docs/usage) — Common use cases and command patterns
- [CLI Reference](/docs/cli-reference) — Complete reference for all options and commands
