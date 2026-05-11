<p align="center">
  <img alt="archphish Logo" src="https://raw.githubusercontent.com/Arc-Cyber-Arsenal/archphish/main/arcpish.png" height="160" />
  <p align="center">
</p>

# archphish

**Advanced Man-in-the-Middle Phishing Framework with 2FA Bypass**

archphish is a penetration testing tool that uses transparent reverse‑proxy techniques to capture login credentials and session cookies, even against websites protected by two‑factor authentication. Provided by **Archsec‑Emman**.

> **Disclaimer:** Use only on systems you own or have explicit permission to test. The author is not responsible for any misuse.

---

## Features

- **Transparent proxy** – No TLS warnings with a valid certificate.
- **2FA bypass** – Capture session cookies after full authentication.
- **Phishlets** – YAML‑based templates for any target (Google, Microsoft, etc.).
- **Live session view** – Terminal UI and JSON API.
- **Lure system** – Custom landing pages and redirects.
- **Cross‑platform** – Windows, Linux, macOS (single binary).

---

## Quick Start

```bash
# Clone the repo
git clone https://github.com/Arc-Cyber-Arsenal/archphish.git
cd archphish
go build -o archphish .
./archphish
