<div align="center">

# 🔍 SecureScan Suite v6.0

[![SecureScan](https://img.shields.io/badge/SecureScan-Suite_v6.0-00d4aa?style=for-the-badge&logo=shield&logoColor=white)](https://sudoninja-noob.github.io/securescan-suite/)
[![Author](https://img.shields.io/badge/author-%40sudoninja-c44dff?style=for-the-badge)](https://github.com/sudoninja-noob)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![HTML](https://img.shields.io/badge/Built_with-HTML_%2F_JS-f5a623?style=for-the-badge&logo=html5&logoColor=white)]()
[![No Backend](https://img.shields.io/badge/No_Backend-100%25_Client--Side-34d399?style=for-the-badge)]()
[![CVE DB](https://img.shields.io/badge/CVE_DB-NVD_%C2%B7_OSV_%C2%B7_GHSA-60a5fa?style=for-the-badge)]()

**A fully client-side security scanning suite for SBOM, SCA, and Firmware analysis.**
Zero installation. Zero backend. Drop a file, get a report.

[🔍 **Launch Tool**](https://sudoninja-noob.github.io/securescan-suite/SecureScan_Suite_V6_0.html) · [🌐 **Landing Page**](https://sudoninja-noob.github.io/securescan-suite/) · [🎬 **Watch Demo**](https://youtu.be/mRZiuCSYBSs) · [🐛 **Report a Bug**](https://github.com/sudoninja-noob/securescan-suite/issues)

</div>

---

## 🎬 Demo

<div align="center">

[![SecureScan Suite Demo](https://img.youtube.com/vi/mRZiuCSYBSs/maxresdefault.jpg)](https://youtu.be/mRZiuCSYBSs)

**▶ [Watch the full demo on YouTube](https://youtu.be/mRZiuCSYBSs)**

</div>

---

## Overview

**SecureScan Suite** is a single-file, browser-based security scanning tool with three integrated scanners:

| Scanner | Purpose |
|---------|---------|
| 📦 **SBOM Scanner** | Parses package manifests → Software Bill of Materials with CVE cross-reference |
| 🔬 **SCA Scanner** | Fingerprints binary executables/installers → identifies embedded libraries + CVEs |
| 📡 **Firmware Scanner** | Extracts all components from firmware images → CVE mapping + SBOM feed |

All scanning happens **entirely in the browser** — no files uploaded, no backend, no installation.

---

## ✨ Features

- ⚡ **Zero-setup** — open the HTML file, start scanning immediately
- 🔒 **100% client-side** — all analysis runs locally; no data leaves your machine
- 🧩 **Three scanners in one** — SBOM, SCA binary, Firmware — each fully isolated
- 📊 **Multi-format export** — HTML, Excel (.xlsx), CSV, JSON, XML, SPDX, CycloneDX per scanner
- 🔗 **Firmware → SBOM pipeline** — one-click feed of firmware components into SBOM scanner
- 🎯 **Policy gate results** — automated PASS/FAIL against configurable security policies
- 📈 **Vulnerability bar charts** — severity distribution per component
- 🪪 **License compliance grid** — permissive vs copyleft vs proprietary classification
- 🔍 **NVD deep links** — every CVE links to `nvd.nist.gov` for full advisory detail
- 🌙 **Professional dark UI** — color-coded scanner identities (teal / cyan / magenta)

---

## 📦 SBOM Scanner — Manifest Analysis

**Supported ecosystems:**

| Ecosystem | Manifest Files |
|-----------|---------------|
| npm / Node.js | `package.json`, `yarn.lock`, `package-lock.json` |
| Python (PyPI) | `requirements.txt`, `Pipfile`, `setup.py` |
| Java (Maven) | `pom.xml`, `build.gradle` |
| Go | `go.mod`, `go.sum` |
| Rust (Cargo) | `Cargo.toml`, `Cargo.lock` |
| Firmware Feed | Auto-loaded from Firmware Scanner |

**Output:** Vulnerabilities tab · License breakdown · CycloneDX 1.5 JSON preview

**Policy gates:** No critical CVEs · No CVSS ≥ 9.0 · No GPL in prod · All components have a fix

---

## 🔬 SCA Scanner — Binary / Installer Analysis

Fingerprints executables and installers against **80+ known software products**.

**Supported file types:** `.exe` `.msi` `.dmg` `.pkg` `.deb` `.rpm` `.apk` `.jar` `.war` `.ear` `.zip` `.tar.gz`

**Output:** Binary identity · Risk score 0–10 · CVE findings with NVD links · Component tags

---

## 📡 Firmware Scanner — Component Extraction

Extracts **21 components** on every scan — ELF binaries, libraries, config files, startup scripts.

**Device detection:** Router · IP Camera · IoT Device · NAS · Network Switch · OTA Package

**All 21 extracted components include:** `linux-kernel` · `busybox` · `openssl` · `dropbear` · `curl` · `wpa_supplicant` · `hostapd` · `uclibc` · `dnsmasq` · `lighttpd` and more

**Flags:** Hardcoded credentials in `/etc/passwd` + `/etc/shadow` · Command injection in startup scripts

---

## 📊 Export Formats

| Format | SBOM Scanner | SCA Scanner | Firmware Scanner |
|--------|:---:|:---:|:---:|
| **HTML Report** | ✅ | ✅ | ✅ |
| **Excel (.xlsx)** | ✅ 3 sheets | ✅ 3 sheets | ✅ 4 sheets |
| **CSV** | ✅ | — | ✅ |
| **JSON** | ✅ | — | ✅ |
| **XML** | — | — | ✅ |
| **SPDX 2.3** | ✅ | — | — |
| **CycloneDX 1.5** | ✅ | — | ✅ SBOM Feed |

---

## 🚀 Usage

### Option 1 — Direct file open
```bash
git clone https://github.com/sudoninja-noob/securescan-suite.git
cd securescan-suite
# Open SecureScan_Suite_V6_0.html in any modern browser
```

### Option 2 — Visit tool
```
https://sudoninja-noob.github.io/securescan-suite/
```

### Scanning a manifest (SBOM)
1. Drop `requirements.txt`, `package.json`, `pom.xml` etc. into the **SBOM Scanner** drop zone
2. Click **Run SBOM Scan**
3. Export in any format from the export bar

### Scanning a binary (SCA)
1. Drop any `.exe`, `.msi`, `.apk`, `.jar` into the **SCA Scanner** drop zone
2. Scan starts automatically — product fingerprinted, CVEs displayed inline

### Scanning firmware
1. Drop any `.bin`, `.img`, `.squashfs`, `.tar.gz` into the **Firmware Scanner** drop zone
2. 21 components extracted, CVEs mapped
3. Click **⟶ Feed to SBOM Scanner** for the full Firmware → SBOM pipeline

---

## 🛠 Tech Stack

| Technology | Purpose |
|-----------|---------|
| **HTML5 / CSS3** | Single-file UI, no frameworks |
| **Vanilla JavaScript (ES2020)** | All scan logic and export functions |
| **SheetJS (xlsx.js)** | Excel workbook generation (CDN) |
| **CycloneDX 1.5** | SBOM output format |
| **SPDX 2.3** | Alternative SBOM output format |

No build step. No npm. No webpack. No frameworks. One HTML file.

---

## 📁 Project Structure

```
securescan-suite/
├── index.html                    ← GitHub Pages landing page
├── SecureScan_Suite_V6_0.html    ← Main tool (single file)
├── README.md                     ← This file
├── LICENSE                       ← MIT License
├── sample-reports/               ← Example exported reports
│   ├── fw-sca-IoTGoat-raspberry-pi2.html
│   ├── sbom-report-AndroidManifest.html
│   └── sca-report-InsecureBankv2.html
└── screenshots/                  ← UI screenshots
```

---

## 📋 Changelog

| Version | Changes |
|---------|---------|
| **v6.0** | Full redesign — 3 isolated scanner cards, all 21 firmware components, 7-format exports |
| **v5.0** | Added Firmware Scanner with SBOM feed integration |
| **v4.0** | Policy gates, bar charts, HTML report matching CAST Highlight format |
| **v3.0** | Excel multi-sheet workbook export |
| **v2.0** | SCA binary scanner with 15+ product fingerprints |
| **v1.0** | Initial SBOM manifest scanner |

---

## 👤 Author

**Sanjay Singh** · `@sudoninja`
Senior Manager, Cyber Security Services — SGS Brightsight · Bengaluru

| | |
|--|--|
| 🐙 GitHub | [@sudoninja-noob](https://github.com/sudoninja-noob) |
| 🦈 SudoShark | [PCAP Security Analyzer](https://sudoninja-noob.github.io/sudoshark/) |
| 🌐 Portfolio | [sudoninja-noob.github.io](https://sudoninja-noob.github.io) |
| 📜 Certs | OSCP · CRTP · CEH · CPTE |
| 🐛 CVEs | 100+ MITRE-assigned |
| 📚 Books | 6 published on Amazon KDP |
| 🔴 Red Team | Synack Red Team operator |

---

## ⚖️ License

MIT License — free to use, modify, and distribute. Attribution appreciated.

---

<div align="center">

🔍 **SecureScan Suite v6.0** · Built by [@sudoninja](https://github.com/sudoninja-noob) · Zero dependencies · 100% client-side

⭐ **Star this repo if it helped you** ⭐

</div>
