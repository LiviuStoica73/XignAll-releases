# XignAll

**XignAll** is a desktop application for bulk PDF digital signing with precise coordinate-based placement, document preparation, and signature verification — 100% offline, no server, no cloud.

> **v1.1.0** — macOS · Windows · Linux · RO / EN / FR / DE

---

## Download v1.1.0

| Platform | File | Requirements |
|----------|------|--------------|
| macOS | `XignAll-1.1.0-mac.dmg` | macOS 12+ (Intel + Apple Silicon) |
| Windows | `XignAll-1.1.0-win.msi` | Windows 10/11 (x64) |
| Linux | `XignAll-1.1.0-linux-x86_64.tar.gz` | Ubuntu 22.04+ / Debian 12+ (x86_64) |

→ [**All releases**](https://github.com/LiviuStoica73/XignAll-releases/releases)

---

## Features

- Bulk folder signing — unlimited documents
- PKCS#12 (.p12 / .pfx) and PKCS#11 hardware token signing (USB eToken, YubiKey)
- Precise visual signature placement on coordinates
- Serial signing workflow — multiple signers in sequence
- Document preparation: DOCX / ODT / XLSX → PDF via LibreOffice
- Signature verification with trust chain details
- PAdES-compliant signatures (B-level)
- TSA timestamp configuration
- PDF Tools: merge, split, remove pages, append pages
- Utilities: stamp extraction, handwritten signature extraction, selective ZIP
- Multi-language interface: Romanian / English / French / German
- Cross-platform: signing profiles work identically on macOS, Windows and Linux
- Local processing — no cloud, no telemetry, no internet required

---

## Pricing

### FREE — €0 forever

| Feature | |
|---------|-|
| PDF document preparation (Steps 1–5) | ✓ |
| Single file signing with coordinates | ✓ |
| PKCS#12 (.p12 / .pfx) signing | ✓ |
| Qualified certificate signing (PKCS#11 hardware token) | ✓ |
| TSA timestamp configuration | ✓ |
| Multiple signer profiles | ✓ |
| PDF Merge + Split | ✓ |
| Signature verification | ✓ |
| RO / EN / FR / DE interface | ✓ |
| macOS + Windows + Linux | ✓ |

### PRO

| Billing | Price |
|---------|-------|
| Monthly | €10 / month + VAT |
| **Annual** | **€89 / year + VAT** *(save 26% vs monthly)* |
| Perpetual | €169 one-time + VAT |

**Everything in Free, plus:**
- Full document preparation pipeline (all steps including remove last pages + append pages)
- Bulk folder signing — unlimited documents
- Unlimited signer profiles
- Serial signing workflow
- TSA timestamp configuration
- All 9 PDF Tools
- Utilities: stamp & handwritten signature extraction, selective ZIP
- Three simultaneous activations: macOS + Windows + Linux
- ChatBot / Email support

### Server Edition

| Billing | Price |
|---------|-------|
| Monthly | €50 / month + VAT |
| **Annual** | **€499 / year + VAT** *(save 17% vs monthly)* |
| Perpetual | €799 one-time + VAT |

**Everything in Pro, plus:**
- Issues internal .p12 certificates for signers
- Signs with qualified digital seal (SEAL) on file arrival
- Runs as background service
- macOS (launchd) / Linux (systemd) / Windows (NSSM)
- Signing log + audit report (PDF)
- Per-organization license
- Local processing — no cloud
- ChatBot / Email support

→ [**Buy license — xignall.io**](https://xignall.io)

---

## Installation

**macOS:** Open the `.dmg`, drag `XignAll.app` to Applications, launch from Applications (not from the DMG).

**Windows:** Run the `.msi` installer. License file is stored in `%APPDATA%\XignAll\`.

**Linux:**
```bash
tar -xzf XignAll-1.1.0-linux-x86_64.tar.gz
cd XignAll
./XignAll
```

---

## License

Commercial software — see [xignall.io](https://xignall.io) for full terms.

© 2026 Liviu Stoica — liviustoica73@gmail.com
