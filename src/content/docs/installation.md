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
brew tap russmckendrick/tap
brew install ssl-toolkit
```

To upgrade to the latest version:

```bash
brew upgrade ssl-toolkit
```

## GitHub Releases (Linux / macOS / Windows)

Pre-built binaries are available for all major platforms from the [GitHub Releases](https://github.com/russmckendrick/ssl-toolkit/releases) page.

### Linux / macOS

Download and install using curl:

```bash
# Download the latest release for your platform
curl -sL https://github.com/russmckendrick/ssl-toolkit/releases/latest/download/ssl-toolkit-$(uname -s)-$(uname -m).tar.gz | tar xz

# Move to a directory in your PATH
sudo mv ssl-toolkit /usr/local/bin/
```

### Windows

1. Download the latest `.zip` file from the [releases page](https://github.com/russmckendrick/ssl-toolkit/releases)
2. Extract the executable
3. Add the directory to your system PATH, or move `ssl-toolkit.exe` to a directory already in your PATH

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
