---
title: CLI Reference
description: Complete reference for all ssl-toolkit options, commands, and exit codes.
order: 4
---

# CLI Reference

Complete reference for all ssl-toolkit command-line options and commands.

## Synopsis

```bash
ssl-toolkit [OPTIONS]
ssl-toolkit [OPTIONS] -d <DOMAIN>
ssl-toolkit cert <SUBCOMMAND>
```

## Global Options

| Flag | Value | Description |
|------|-------|-------------|
| `-d, --domain` | `<domain>` | Target domain to analyze |
| `-i, --ip` | `<address>` | Override IP address for connection |
| `-p, --port` | `<port>` | Target port (default: 443) |
| `--non-interactive` | | Run all checks without prompts |
| `-q, --quiet` | | Only output the security grade |
| `--json` | | Output results in JSON format |
| `-o, --output` | `<file>` | Export HTML report to file |
| `-v, --verbose` | | Show detailed check information |
| `--skip-whois` | | Skip WHOIS lookup |
| `--timeout` | `<seconds>` | Connection timeout (default: 10) |
| `--config` | `<file>` | Custom configuration file path |
| `-h, --help` | | Print help information |
| `-V, --version` | | Print version information |

## Certificate Commands

The `cert` subcommand provides operations for working with local certificate files.

### cert info

Display certificate details from PEM files.

```bash
ssl-toolkit cert info <FILES...>
```

**Arguments:**

- `<FILES...>` — One or more PEM certificate files to inspect

**Example:**

```bash
ssl-toolkit cert info server.pem intermediate.pem
```

### cert verify

Verify certificate and key pairs or validate certificate chains.

```bash
ssl-toolkit cert verify [OPTIONS]
```

**Options:**

| Flag | Value | Description |
|------|-------|-------------|
| `--cert` | `<file>` | Certificate file to verify |
| `--key` | `<file>` | Private key file to match against certificate |
| `--chain` | `<file>` | Certificate chain file to validate |
| `--hostname` | `<domain>` | Hostname to validate certificate against |

**Examples:**

Verify certificate and key match:

```bash
ssl-toolkit cert verify --cert server.pem --key server.key
```

Validate certificate chain for hostname:

```bash
ssl-toolkit cert verify --chain fullchain.pem --hostname example.com
```

### cert convert

Convert certificates between formats.

```bash
ssl-toolkit cert convert <FILE> --to <FORMAT> [OPTIONS]
```

**Arguments:**

- `<FILE>` — Source certificate file

**Options:**

| Flag | Value | Description |
|------|-------|-------------|
| `--to` | `<format>` | Target format: `pem`, `der`, or `p12` |
| `-o, --output` | `<file>` | Output file path |
| `--cert` | `<file>` | Certificate file (for P12 creation) |
| `--key` | `<file>` | Private key file (for P12 creation) |

**Examples:**

Convert PEM to DER:

```bash
ssl-toolkit cert convert cert.pem --to der -o cert.der
```

Create PKCS#12 bundle:

```bash
ssl-toolkit cert convert --to p12 --cert cert.pem --key key.pem -o bundle.p12
```

## Exit Codes

ssl-toolkit uses meaningful exit codes for scripting and CI/CD integration:

| Code | Status | Description |
|------|--------|-------------|
| **0** | Success | All checks passed, certificate is valid and secure |
| **1** | Warning | Certificate expiring soon (< 30 days) or minor issues detected |
| **2** | Failure | Certificate expired, connection failed, or critical security issue |

### Using Exit Codes

In shell scripts:

```bash
ssl-toolkit -d example.com --quiet
case $? in
  0) echo "Certificate OK" ;;
  1) echo "Certificate expiring soon" ;;
  2) echo "Certificate has critical issues" ;;
esac
```

In CI/CD pipelines:

```yaml
# GitHub Actions example
- name: Check SSL Certificate
  run: ssl-toolkit -d ${{ env.DOMAIN }} --quiet
  continue-on-error: false
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `SSL_TOOLKIT_CONFIG` | Path to default configuration file |
| `NO_COLOR` | Disable colored output when set |

## Configuration File

ssl-toolkit can be configured via a TOML file. Default locations:

- `~/.config/ssl-toolkit/config.toml` (Linux/macOS)
- `%APPDATA%\ssl-toolkit\config.toml` (Windows)

Example configuration:

```toml
[defaults]
timeout = 15
skip_whois = false
verbose = false

[dns]
providers = ["google", "cloudflare", "opendns"]

[output]
format = "text"  # or "json"
```

## See Also

- [Getting Started](/docs/getting-started) — Quick introduction and first steps
- [Installation](/docs/installation) — Detailed installation instructions
- [Usage Examples](/docs/usage) — Common use cases and patterns
