<p align="center">
  <img alt="archphish Logo" src="https://i.ibb.co/s9J5QK30/Gemini-Generated-Image-skxiy0skxiy0skxi.png" height="160" />
  <p align="center">
    <img alt="archphish Title" src="https://i.ibb.co/s9J5QK30/Gemini-Generated-Image-skxiy0skxiy0skxi.png" height="60" />
  </p>
</p>

# archphish

**Advanced Man-in-the-Middle Phishing Framework with 2FA Bypass**

archphish is a penetration testing tool that uses transparent reverse‑proxy techniques to capture login credentials and session cookies, even against websites protected by two‑factor authentication. It is a rebranded fork of the original evilginx2, maintained by **Archsec‑Emman**.

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
