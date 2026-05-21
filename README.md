<p align="center">
  <img alt="archphish Logo" src="https://raw.githubusercontent.com/Arc-Cyber-Arsenal/archphish/main/arcpish.png" height="160" />
  <p align="center">
</p>


# ArchPhish

[![Language](https://img.shields.io/badge/Go-1.20+-00ADD8?logo=go)](https://go.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-windows%20%7C%20linux%20%7C%20macos-lightgrey)](https://github.com/Archsec-Emman/archphish)

**An Advanced Man-in-the-Middle Phishing Framework with 2FA Bypass**  
ArchPhish is a professional-grade penetration testing tool that uses transparent reverse‑proxy techniques to capture login credentials and session cookies, even from websites protected by two‑factor authentication (2FA).

> **⚠️ IMPORTANT DISCLAIMER:** This tool is intended **exclusively for authorised security testing, educational research, and defending your own systems**. Use it only on systems you own or have explicit written permission to test. The author is not responsible for any misuse or damage caused by this software.

---

## 📖 Overview

ArchPhish is designed for red teams and security professionals to assess an organisation's resilience against advanced phishing attacks. By acting as a stealthy reverse proxy, it intercepts traffic between a target and a legitimate website, capturing credentials and session tokens in real time, even when the target site uses two-factor authentication (2FA) or other multi-factor authentication (MFA) mechanisms. It is a cross‑platform, single‑binary tool written in Go, making it easy to deploy in diverse engagement environments.

## ✨ Key Features

- **🔒 Transparent Reverse Proxy** – Sits between the user and the target website, intercepting traffic without triggering TLS certificate warnings (thanks to automated Let's Encrypt integration).
- **🔑 2FA/MFA Bypass** – Captures session cookies **after** the user has completed the multi-factor authentication process, allowing the attacker to hijack the authenticated session.
- **📄 Phishlets** – Uses YAML-based templates to define the behaviour for any target (e.g., Google, Microsoft, GitHub, banking portals). The modular system makes it easy to add new targets or customise existing ones.
- **📡 Live Session View** – Monitor captured credentials, cookies, and traffic in real time via a terminal UI or through a structured JSON API.
- **🎣 Lure System** – Create custom landing pages and configure stealthy redirects to send victims to the legitimate site after their data is captured.
- **⚙️ Cross‑Platform** – A single, statically-linked binary runs on Windows, Linux, and macOS, with no external dependencies.
- **📊 Built-in Analytics** – Tracks engagement metrics such as click-through rates and session durations, useful for campaign reporting.

## 🚀 Quick Start

### Prerequisites
- Go 1.20 or later (only required for building from source)
- Git
- A domain name (for TLS certificate issuance)

### Installation

#### Option 1: Download a Pre-built Binary (Recommended)
Visit the [Releases](https://github.com/Archsec-Emman/archphish/releases) page and download the latest version for your operating system.

#### Option 2: Build from Source
```bash
# Clone the repository
git clone https://github.com/Archsec-Emman/archphish.git
cd archphish

# Build the binary
go build -o archphish .

# (Optional) Install system-wide
sudo cp archphish /usr/local/bin/
```

### Basic Usage
```bash
# Run ArchPhish with a phishlet for a target (e.g., "linkedin")
./archphish -p 443 -phishlet linkedin -domain your-domain.com
```

Once running, ArchPhish will:
1. Obtain a valid TLS certificate for `your-domain.com` via Let's Encrypt.
2. Serve the fake login page defined in the `linkedin` phishlet.
3. Proxy all subsequent requests to the real LinkedIn.
4. Log captured credentials and session cookies to the console and a database.

## 📚 Detailed Usage

### Command-Line Options

| Option | Description | Default |
|--------|-------------|---------|
| `-p` | Port to listen on (usually 443 for HTTPS) | `443` |
| `-phishlet` | Name of the phishlet to use (e.g., `google`, `microsoft`) | Required |
| `-domain` | Your domain name (must be pointed to the server) | Required |
| `-config` | Path to a custom configuration file | `config.yml` |
| `-lure` | Redirect URL after credential capture | None |
| `-verbose` | Enable verbose logging | `false` |
| `-api` | Enable the JSON API on port 8080 | `false` |

### Creating a Custom Phishlet

Phishlets are YAML files stored in the `phishlets/` directory. A basic template looks like this:

```yaml
name: "example"
author: "Your Name"
version: "1.0"

# The target's URL
url: "https://example.com"

# Regex patterns to identify login pages
auth_regex:
  - "login"
  - "signin"

# Credentials extraction rules
credentials:
  username: "input[name='username']"
  password: "input[name='password']"
  # For 2FA tokens
  token: "input[name='totp']"

# Post-capture behaviour
redirect_url: "https://example.com/dashboard"
```

### Live Session Monitoring

With the JSON API enabled (`-api`), you can integrate ArchPhish with other tools or build a custom dashboard:

```bash
# Get all captured sessions
curl http://localhost:8080/api/sessions

# Get details of a specific session
curl http://localhost:8080/api/session/123
```

## 📂 Project Structure

```
archphish/
├── core/               # Core proxy, TLS, and HTTP logic
├── phishlets/          # YAML templates for each target
├── database/           # SQLite/PostgreSQL storage layer
├── log/                # Logging utilities
├── parser/             # HTML parsing and form manipulation
├── redirectors/        # URL redirection handlers
├── vendor/             # Third-party dependencies
├── main.go             # Application entry point
├── go.mod              # Go module definition
├── LICENSE             # MIT License
├── Makefile            # Build automation
└── README.md           # This file
```

## 🛠️ Development & Contribution

We welcome contributions that improve the tool’s robustness, add new phishlets, or enhance documentation. Please follow the standard GitHub flow:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/amazing-feature`).
3. Commit your changes (`git commit -m 'Add some amazing feature'`).
4. Push to the branch (`git push origin feature/amazing-feature`).
5. Open a Pull Request.

**Development Requirements:**
- Go 1.20+
- Make (optional, for using the Makefile)

**Run Tests:**
```bash
go test ./...
```

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

## 📬 Contact & Support

- **GitHub Issues**: [https://github.com/Archsec-Emman/archphish/issues](https://github.com/Archsec-Emman/archphish/issues)
- **Author**: [Archsec-Emman](https://github.com/Archsec-Emman)

---

*If you find ArchPhish useful in your professional security assessments, please consider giving the repository a star.* ⭐
```
