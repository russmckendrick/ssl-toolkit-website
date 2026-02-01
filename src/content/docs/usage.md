---
title: Usage Examples
description: Common use cases and command patterns for ssl-toolkit.
order: 3
---

# Usage Examples

This page covers common use cases and command patterns for ssl-toolkit.

## Interactive Mode

Launch ssl-toolkit without arguments for an interactive experience:

```bash
ssl-toolkit
```

Or specify a domain to get prompted for which checks to run:

```bash
ssl-toolkit -d example.com
```

The interactive menu includes options for:

- DNS Resolution
- TLS Connection analysis
- Certificate Details
- WHOIS Lookup
- Security Grade
- And more

Use arrow keys to navigate and Enter to select.

## Domain Checks

### Full Domain Analysis

Run all checks on a domain without prompts:

```bash
ssl-toolkit -d github.com --non-interactive
```

### Quick Grade Only

Get just the security grade with minimal output:

```bash
ssl-toolkit -d example.com --quiet
```

### Custom Port

Check a service running on a non-standard port:

```bash
ssl-toolkit -d example.com -p 8443
```

### Override IP Address

Useful for testing a specific server or before DNS propagation:

```bash
ssl-toolkit -d example.com -i 192.168.1.100
```

### Skip WHOIS Lookup

WHOIS lookups can be slow due to rate limiting. Skip them when not needed:

```bash
ssl-toolkit -d example.com --non-interactive --skip-whois
```

### Verbose Output

Get detailed information about each check:

```bash
ssl-toolkit -d example.com --non-interactive --verbose
```

## Certificate Operations

### View Certificate Details

Inspect a local PEM certificate file:

```bash
ssl-toolkit cert info cert.pem
```

View multiple certificates at once:

```bash
ssl-toolkit cert info cert.pem intermediate.pem root.pem
```

### Verify Certificate and Key Pair

Check that a certificate and private key match:

```bash
ssl-toolkit cert verify --cert cert.pem --key key.pem
```

### Validate Certificate Chain

Verify a certificate chain is valid for a hostname:

```bash
ssl-toolkit cert verify --chain chain.pem --hostname example.com
```

### Convert Certificate Formats

Convert PEM to DER:

```bash
ssl-toolkit cert convert cert.pem --to der -o cert.der
```

Convert PEM to PKCS#12 (PFX):

```bash
ssl-toolkit cert convert --to p12 --cert cert.pem --key key.pem
```

## CI/CD Integration

### JSON Output

Get structured JSON output for parsing in scripts:

```bash
ssl-toolkit -d example.com --non-interactive --json
```

Example JSON structure:

```json
{
  "domain": "example.com",
  "grade": "A+",
  "score": 100,
  "certificate": {
    "subject": "CN=example.com",
    "issuer": "...",
    "valid_from": "2024-01-01T00:00:00Z",
    "valid_until": "2025-01-01T00:00:00Z"
  },
  "checks": [...]
}
```

### HTML Reports

Generate a standalone HTML report:

```bash
ssl-toolkit -d example.com --non-interactive -o report.html
```

The report includes embedded styles and can be viewed in any browser.

### Exit Codes in Scripts

Use exit codes to integrate with CI/CD pipelines:

```bash
ssl-toolkit -d example.com --quiet && echo "SSL OK" || echo "SSL FAIL"
```

Exit codes:

| Code | Meaning |
|------|---------|
| 0 | Success — all checks passed |
| 1 | Warning — certificate expiring soon or minor issues |
| 2 | Failure — certificate expired, connection failed, or critical error |

### Timeout Configuration

Set a custom connection timeout (default is 10 seconds):

```bash
ssl-toolkit -d example.com --timeout 30
```

## Advanced Usage

### Custom Configuration File

Use a custom configuration file:

```bash
ssl-toolkit -d example.com --config /path/to/config.toml
```

### Multiple Domain Checks

Check multiple domains in a script:

```bash
for domain in example.com github.com google.com; do
  echo "Checking $domain..."
  ssl-toolkit -d "$domain" --quiet
done
```

### Certificate Expiry Monitoring

Create a simple monitoring script:

```bash
#!/bin/bash
DOMAINS="example.com github.com"

for domain in $DOMAINS; do
  result=$(ssl-toolkit -d "$domain" --quiet 2>&1)
  exit_code=$?
  
  if [ $exit_code -eq 0 ]; then
    echo "✓ $domain: $result"
  elif [ $exit_code -eq 1 ]; then
    echo "⚠ $domain: $result (warning)"
  else
    echo "✗ $domain: FAILED"
  fi
done
```
