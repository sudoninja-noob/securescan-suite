# SecureScan Suite

<div align="center">

![SecureScan Suite](https://img.shields.io/badge/SecureScan-Suite_v6.0-00d4aa?style=for-the-badge&logo=shield&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)
![HTML](https://img.shields.io/badge/Built_with-HTML_%2F_JS-f5a623?style=for-the-badge&logo=html5&logoColor=white)
![No Backend](https://img.shields.io/badge/No_Backend-100%25_Client--Side-34d399?style=for-the-badge)
![CVE Database](https://img.shields.io/badge/CVE_DB-NVD_%C2%B7_OSV_%C2%B7_GHSA-60a5fa?style=for-the-badge)

**A fully client-side security scanning suite for SBOM, SCA, and Firmware analysis.**  
Zero installation. Zero backend. Drop a file, get a report.

[🔍 Live Demo](#) · [📖 Documentation](#usage) · [🐛 Report a Bug](https://github.com/sudoninja-noob/securescan-suite/issues) · [💡 Request a Feature](https://github.com/sudoninja-noob/securescan-suite/issues)

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Scanners](#scanners)
  - [SBOM Scanner](#1-sbom-scanner--manifest-analysis)
  - [SCA Scanner](#2-sca-scanner--binary--installer-analysis)
  - [Firmware Scanner](#3-firmware-scanner--component-extraction)
- [Supported File Types](#supported-file-types)
- [Export Formats](#export-formats)
- [SBOM Feed Integration](#sbom-feed-integration-firmware--sbom)
- [CVE Databases](#cve-databases)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Author](#author)
- [License](#license)

---

## Overview

**SecureScan Suite** is a single-file, browser-based security scanning tool that provides three integrated scanners in one interface:

| Scanner | Purpose |
|---------|---------|
| **SBOM Scanner** | Parses package manifests and generates a Software Bill of Materials with CVE cross-reference |
| **SCA Scanner** | Fingerprints binary executables and installers to identify embedded libraries and known vulnerabilities |
| **Firmware Scanner** | Extracts all components from firmware images, maps CVEs, flags misconfigurations, and generates a SBOM feed |

All scanning happens **entirely in the browser** — no files are uploaded to any server, no backend required, no installation needed.

---

## Features

- ⚡ **Zero-setup** — open the HTML file, start scanning immediately
- 🔒 **100% client-side** — all analysis runs locally in your browser; no data leaves your machine
- 🧩 **Three scanners in one** — SBOM, SCA binary, and Firmware, each with isolated output panels
- 📊 **Multi-format export** — HTML, Excel (.xlsx), CSV, JSON, XML, SPDX, CycloneDX per scanner
- 🔗 **Firmware → SBOM pipeline** — one-click feed of extracted firmware components into the SBOM scanner
- 🎯 **Policy gate results** — automated pass/fail checks against configurable security policies
- 📈 **Vulnerability bar charts** — visual distribution of CVEs by component and severity
- 🪪 **License compliance grid** — permissive vs copyleft vs proprietary classification
- 🔍 **NVD deep links** — every CVE links directly to `nvd.nist.gov` for full advisory detail
- 🌙 **Dark UI** — professional dark theme with color-coded scanner identities

---

## Scanners

### 1. SBOM Scanner — Manifest Analysis

Accepts package manifest files and produces a full **Software Bill of Materials** with vulnerability cross-reference.

**Supported ecosystems:**

| Ecosystem | Manifest Files |
|-----------|---------------|
| **npm / Node.js** | `package.json`, `yarn.lock`, `package-lock.json` |
| **Python (PyPI)** | `requirements.txt`, `Pipfile`, `setup.py` |
| **Java (Maven)** | `pom.xml`, `build.gradle` |
| **Go** | `go.mod`, `go.sum` |
| **Rust (Cargo)** | `Cargo.toml`, `Cargo.lock` |
| **Firmware Feed** | Auto-loaded from Firmware Scanner |

**Output tabs:**
- **Vulnerabilities** — filterable/searchable CVE table with severity, CVSS score, fix version
- **Licenses** — bar chart breakdown of license types with review flags
- **SBOM Output** — CycloneDX 1.5 JSON preview with syntax highlighting

**Policy gates checked:**
- No critical CVEs in direct dependencies
- No CVEs with CVSS ≥ 9.0
- No GPL/unknown licenses in production
- All components have a fix available

---

### 2. SCA Scanner — Binary / Installer Analysis

Fingerprints executables and installers against a database of **80+ known software products** to identify embedded third-party libraries and associated CVEs.

**Matched software includes:**

| Category | Products |
|----------|---------|
| Network Tools | Wireshark, Nmap |
| Archive Managers | WinRAR, 7-Zip |
| SSH Clients | PuTTY, WinSCP |
| Runtimes | Python, Node.js |
| Browsers | Firefox, Chrome |
| Media | VLC |
| Conferencing | Zoom |
| Office | LibreOffice |
| Databases | MySQL |
| Crypto | OpenSSL |
| Java Apps | `.jar`, `.war`, `.ear` |
| Android | `.apk` |

**Output includes:**
- Binary identity metadata (product, vendor, category, file size, type)
- Risk score (0–10) with visual bar
- Expandable CVE findings with NVD links
- Detected third-party component tags with versions and licenses
- Policy gate results

---

### 3. Firmware Scanner — Component Extraction

Performs deep component extraction from firmware images, simulating extraction of:

- ELF binaries (`/bin`, `/sbin`, `/usr/sbin`)
- Shared libraries (`/usr/lib`, `/lib`)
- Package manager databases (opkg / dpkg / apk)
- Configuration files (`/etc/passwd`, `/etc/shadow`)
- Startup scripts (`/etc/init.d/`)

**All 21 components extracted on every scan:**

| Component | Type | Notable CVEs |
|-----------|------|-------------|
| `linux-kernel` | kernel | CVE-2023-35788 (High) |
| `busybox` | binary | CVE-2022-48174 (Critical) |
| `openssl` | library | CVE-2023-0286 (High) |
| `dropbear` | binary | CVE-2023-48795 (Medium) |
| `curl` | library | CVE-2023-38545 (Critical) |
| `wpa_supplicant` | binary | CVE-2022-23304 (Critical) |
| `hostapd` | binary | CVE-2022-23303 (Critical) |
| `uclibc` | library | CVE-2022-29503 (Critical) |
| `dnsmasq` | binary | CVE-2023-28450 (High) |
| `lighttpd` | binary | CVE-2022-41556 (High) |
| `fwupd` | binary | CVE-2020-10759 (Medium) |
| `zlib`, `sqlite3`, `libpcap` | library | — |
| `iptables`, `udhcpc`, `opkg`, `mtd-utils` | binary/package | — |
| `/etc/passwd`, `/etc/shadow` | config | Hardcoded credential flags |
| `init.sh` | script | Command injection risk |

**Firmware device type detection:**

| Filename pattern | Detected as |
|------------------|------------|
| `router`, `openwrt`, `dd-wrt` | Router / Access Point |
| `camera`, `hikvision`, `dahua` | IP Camera |
| `iot`, `esp`, `rtos` | IoT Device |
| `nas`, `synology`, `qnap` | NAS Device |
| `switch`, `cisco`, `netgear` | Network Switch |
| `update`, `ota` | OTA Update Package |
| *(any other)* | Embedded Linux Firmware |

---

## Supported File Types

### SBOM Scanner
```
.json  .txt  .toml  .xml  .lock  .sum  .yaml  .yml  .gradle
```

### SCA Scanner
```
.exe  .msi  .dmg  .pkg  .deb  .rpm  .apk  .appx
.zip  .tar  .gz   .xz   .7z   .bin  .run  .sh
.jar  .war  .ear
```

### Firmware Scanner
```
.bin  .img  .squashfs  .ext4  .cramfs  .jffs2  .ubifs
.tar  .gz   .xz        .bz2   .zip     .hex    .ihex
.elf  .axf  .rom       .fw    .update  .ota    .pak
```

---

## Export Formats

Each scanner exports independently. No output from one scanner appears in another scanner's report.

| Format | SBOM Scanner | SCA Scanner | Firmware Scanner |
|--------|:---:|:---:|:---:|
| **HTML Report** | ✅ | ✅ | ✅ |
| **Excel (.xlsx)** | ✅ | ✅ | ✅ (4 sheets) |
| **CSV** | ✅ | — | ✅ |
| **JSON** | ✅ | — | ✅ |
| **XML** | — | — | ✅ |
| **SPDX 2.3** | ✅ | — | — |
| **CycloneDX 1.5** | ✅ | — | ✅ (SBOM Feed sheet) |
| **PDF** | ✅ (print) | — | — |

### Excel sheet structure

**SBOM Excel workbook:**
1. `Overview` — scan metadata and summary statistics
2. `Vulnerabilities` — full CVE table
3. `Licenses` — license type breakdown

**SCA Excel workbook:**
1. `Overview` — binary identity and risk summary
2. `CVE Findings` — all CVEs with NVD links
3. `Components` — detected third-party libraries

**Firmware Excel workbook:**
1. `Overview` — firmware identity and risk summary
2. `Component Inventory` — all 21 extracted components
3. `CVE Findings` — all CVEs with binary paths and NVD links
4. `SBOM Feed` — CycloneDX-format component list for import

---

## SBOM Feed Integration (Firmware → SBOM)

The Firmware Scanner includes a **"⟶ Feed to SBOM Scanner"** button that:

1. Converts all extracted firmware components into a synthetic manifest file (`fw-<name>-components.txt`)
2. Auto-loads it into the SBOM Scanner file list
3. Highlights the SBOM Scanner drop zone and shows a feed notice
4. Enables the "Run SBOM Scan" button — ready to scan immediately

This creates a complete **Firmware → Component Extraction → SBOM Generation** pipeline in a single workflow.

---

## CVE Databases

SecureScan Suite cross-references vulnerabilities against:

| Source | Type | Coverage |
|--------|------|---------|
| **NVD** (National Vulnerability Database) | US Government | CVSS scores, CWE mapping |
| **OSV** (Open Source Vulnerabilities) | Google | Package-level advisories |
| **GHSA** (GitHub Advisory Database) | GitHub | Ecosystem-specific advisories |

Every CVE displayed includes a direct deep link to `https://nvd.nist.gov/vuln/detail/<CVE-ID>` for full advisory detail.

---

## Usage

### Option 1 — Direct file open
```bash
git clone https://github.com/sudoninja-noob/securescan-suite.git
cd securescan-suite
open sbom-scanner_V7.html        # macOS
xdg-open sbom-scanner_V7.html    # Linux
start sbom-scanner_V7.html       # Windows
```

### Option 2 — GitHub Pages
Visit the live hosted version at:
```
https://sudoninja-noob.github.io/securescan-suite/
```

### Scanning a manifest (SBOM)
1. Drop your `requirements.txt`, `package.json`, `pom.xml`, etc. into the **SBOM Scanner** drop zone
2. Click **Run SBOM Scan**
3. Results appear immediately below the button — vulnerabilities, licenses, CycloneDX output
4. Export in any format from the export bar

### Scanning a binary (SCA)
1. Drop any `.exe`, `.msi`, `.apk`, `.jar`, etc. into the **SCA Scanner** drop zone
2. Scan starts automatically — no button needed
3. Product is fingerprinted, CVEs and components displayed inline
4. Export HTML report or Excel from the export bar

### Scanning firmware
1. Drop any `.bin`, `.img`, `.squashfs`, `.tar.gz`, etc. into the **Firmware Scanner** drop zone
2. Scan runs with simulated extraction steps (3.8s)
3. All 21 firmware components appear across 4 tabs: Components, CVE Findings, Architecture, SBOM Feed
4. Click **⟶ Feed to SBOM Scanner** to push components into the SBOM scanner
5. Export HTML, Excel, CSV, JSON, or XML

---

## Screenshots

> *(Add screenshots here after first GitHub publish)*

```
screenshots/
├── sbom-scanner.png
├── sca-scanner.png
├── firmware-scanner.png
└── export-reports.png
```

---


## 🎥 Product Walkthrough

<p align="center">
  <a href="https://youtu.be/mRZiuCSYBSs?si=4amXYW1Jl-QmeC5X">
    <img src="https://img.youtube.com/vi/YOUR_VIDEO_ID/maxresdefault.jpg" 
         alt="SecureScan Suite – SBOM | SCA | Firmware Security Scanner Demo" 
         width="80%" />
  </a>
</p>

<p align="center">
👉 Click the image above to watch the full demo on YouTube
</p>

---

## ⚡ What is SecureScan Suite?

A fully **client-side security scanning suite** for:
- 📦 SBOM (Software Bill of Materials)
- 🧪 SCA (Binary / Installer analysis)
- 📡 Firmware vulnerability extraction

✔ Zero backend  
✔ No installation  
✔ Runs entirely in browser  

## Tech Stack

| Technology | Purpose |
|------------|---------|
| **HTML5 / CSS3** | Single-file UI, no frameworks |
| **Vanilla JavaScript (ES2020)** | All scan logic, export functions |
| **SheetJS (xlsx.js)** | Excel workbook generation (CDN) |
| **IBM Plex Mono / Inter** | Typography (Google Fonts CDN) |
| **CycloneDX 1.5** | SBOM output format |
| **SPDX 2.3** | Alternative SBOM output format |

No build step. No npm. No webpack. No frameworks. One HTML file.

---

## Project Structure

```
securescan-suite/
│
├── sbom-scanner_V7.html      # Main application (single file)
│
├── README.md                  # This file
│
├── sample-reports/            # Example exported reports
│   ├── sbom-report-sample.html
│   └── sca-report-sample.html
│
└── screenshots/               # UI screenshots for README
```

---

## Changelog

| Version | Changes |
|---------|---------|
| **v6.0 (V7)** | Full redesign — 3 isolated scanner cards, fixed SBOM result placement, all 21 firmware components, OpenSSL only where relevant, 5-format exports per scanner |
| **v5.0** | Added Firmware Scanner with SBOM feed integration, dual HTML+XLSX SCA export |
| **v4.0** | Improved HTML report design matching CAST Highlight format, policy gates, bar charts |
| **v3.0** | Excel (.xlsx) export with multi-sheet workbooks |
| **v2.0** | SCA binary scanner with 15+ product fingerprints |
| **v1.0** | Initial SBOM manifest scanner |

---

## Author

**Sanjay** — [@sudoninja](https://sudoninja-noob.github.io/)

- 🔐 OSCP · CRTP · CPTE · CEH certified
- 📚 Published author of 6 cybersecurity books
- 🔴 Synack Red Team operator
- 🏗️ Security architect specializing in application security, penetration testing, and compliance

---

## License

```
MIT License

Copyright (c) 2026 @sudoninja

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

<div align="center">

Built with ❤️ by [@sudoninja](https://sudoninja-noob.github.io/) · For the security community

⭐ **Star this repo if it helped you** ⭐

</div>
