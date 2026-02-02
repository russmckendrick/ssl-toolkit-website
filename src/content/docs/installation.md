---
title: Installation
description: Install ssl-toolkit on macOS, Linux, or Windows using Homebrew, pre-built binaries, or from source.
order: 2
---

# Installation

ssl-toolkit is available for macOS, Linux, and Windows. Choose the installation method that works best for your system.

## Homebrew (macOS)

The recommended way to install on macOS is via Homebrew:

```bash
brew install russmckendrick/tap/ssl-toolkit
```

To upgrade to the latest version:

```bash
brew upgrade ssl-toolkit
```

## GitHub Releases (Linux / Windows)

Pre-built binaries are available for all major platforms from the [GitHub Releases](https://github.com/russmckendrick/ssl-toolkit/releases) page.

### Linux

Download and install using curl:

```bash
ARCH=$(uname -m | sed 's/x86_64/amd64/;s/aarch64/arm64/')
curl -sL "https://github.com/russmckendrick/ssl-toolkit/releases/latest/download/ssl-toolkit-linux-${ARCH}" -o ssl-toolkit
chmod +x ssl-toolkit
sudo mv ssl-toolkit /usr/local/bin/
```

### Windows

Download using Powershell

```pwshell
Invoke-WebRequest -Uri "https://github.com/russmckendrick/ssl-toolkit/releases/latest/download/ssl-toolkit-windows-amd64.exe" -OutFile "ssl-toolkit.exe"
```

You can then move ssl-toolkit.exe to a directory in your PATH, or run it directly from the download location.

## From Source (Rust)

If you have Rust installed, you can build ssl-toolkit from source:

```bash
# Clone the repository
git clone https://github.com/russmckendrick/ssl-toolkit.git

# Navigate to the project directory
cd ssl-toolkit

# Build the release binary
cargo build --release

# Install to your Cargo bin directory
cargo install --path .
```

### Requirements

- Rust 1.70 or later
- OpenSSL development libraries (on Linux: `libssl-dev` or `openssl-devel`)

## Verifying Installation

After installation, verify ssl-toolkit is working:

```bash
ssl-toolkit --version
```

You should see output like:

```
ssl-toolkit 0.1.0
```

## Updating

### Homebrew

```bash
brew upgrade ssl-toolkit
```

### From Source

```bash
cd ssl-toolkit
git pull
cargo build --release
cargo install --path . --force
```

## Uninstalling

### Homebrew

```bash
brew uninstall ssl-toolkit
```

### Manual Installation

Remove the binary from where you installed it:

```bash
sudo rm /usr/local/bin/ssl-toolkit
```

### Cargo

```bash
cargo uninstall ssl-toolkit
```
