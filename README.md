# XignAll — Local-First Distributed Electronic Signing

**Prepare · Sign · Verify · Automate** — Desktop and server application for distributed electronic signing workflows. Qualified PAdES signatures, organizational SEAL automation, Telegram remote authorization, and batch document processing — entirely within your own infrastructure, without SaaS dependency.

[![Download](https://img.shields.io/badge/Download-v1.3.1-blue?style=flat-square)](https://github.com/LiviuStoica73/XignAll-releases/releases)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey?style=flat-square)]()
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)]()

---

## What is XignAll?

XignAll is a local-first electronic signing and document workflow platform for organizations that sign between dozens and thousands of PDF documents per day. It automates the full document signing workflow — from raw source files to signed, verified PDFs — entirely on your machines and servers, with no cloud uploads and no external signing platform.

Unlike traditional cloud signing services, XignAll operates locally and supports shared-folder workflow orchestration without mandatory APIs or SaaS infrastructure.

**Core use cases:**
- Notary offices batch-signing deeds and notarial acts
- Cadastral commissions processing land registry document sets
- Public administration dispatching serial signing workflows across multiple officials
- Accounting and audit firms signing financial statements and tax declarations in bulk
- Organizations requiring air-gapped or offline-capable signing infrastructure

Supported on **Windows 10/11**, **macOS** (Apple Silicon + Intel), and **Linux** (Ubuntu 22.04+).

---

## Why XignAll is different

| Traditional SaaS e-sign | XignAll |
|------------------------|---------|
| Cloud dependent | Local-first |
| Per-user subscription | One-time license / per-server license |
| Requires API integration | Works with shared folders |
| Documents leave the organization | Documents stay local |
| Centralized workflow | Distributed workflow |
| Browser-based | Native desktop / server app |
| Limited batch operations | High-volume batch (20–60 docs/min) |
| Vendor lock-in | Self-hosted, air-gapped compatible |

---

## Table of Contents

- [Desktop Edition](#desktop-edition)
  - [Document Preparation (Pipeline)](#document-preparation-pipeline)
  - [Digital Signing](#digital-signing)
  - [Multi-Signer Serial Workflow](#multi-signer-serial-workflow)
  - [Signature Verification](#signature-verification)
  - [PDF Tools](#pdf-tools)
  - [Signature & Stamp Extractor](#signature--stamp-extractor)
- [Server Edition](#server-edition--folder-watch--seal--telegram)
  - [Folder Watch — Automatic signing](#folder-watch--automatic-signing)
  - [Telegram Bot — Remote signing](#telegram-bot--remote-signing)
  - [Organizational SEAL](#organizational-seal)
- [Certificates & Hardware Tokens](#certificates--hardware-tokens)
- [Use Cases](#use-cases)
- [Requirements](#requirements)
- [Download](#download)
- [FAQ](#faq)

---

## Desktop Edition

### Document Preparation (Pipeline)

The **Prepare** tab processes source documents in bulk before signing.

**Supported input formats:**
`.doc`, `.docx`, `.odt`, `.rtf`, `.txt`, `.html`, `.xlsx`, `.xls`, `.ods`, `.csv`

**Pipeline steps (each independently enabled/disabled):**

| Step | Description |
|------|-------------|
| **1. Convert to DOCX** | Converts source files to `.docx` via LibreOffice or MS Word |
| **2. Append DOCX page** | Appends a `.docx` page (e.g. signer list) to each document |
| **3. Convert to PDF** | Converts `.docx` to final PDF |
| **4. Append PDF page** | Appends a `.pdf` page to existing PDFs |
| **5. Delete text from marker** | Removes all content from a specified text marker onward (bulk) |
| **6. Trim last N pages (DOCX)** | Removes the last N pages from each `.docx` |
| **7. Trim last N pages (PDF)** | Removes the last N pages from each PDF |

All steps run in parallel with configurable worker threads. A run report is generated after each execution. Already-processed files are skipped on re-run.

---

### Digital Signing

The **Sign** tab applies visible digital signatures to entire folders of PDFs.

**Signature capabilities:**
- **Batch signing** — sign an entire folder (or recursive subfolders) in one operation
- **20–60 documents per minute** depending on hardware and file size
- **Precise coordinate placement** — drag-and-drop on live PDF preview, saved per signer profile
- **Visible signature appearance**: signer name, reason, location, date, logo image
- **Multiple signer profiles** — switch between profiles in one click
- **Page range selection** — sign all pages, even/odd pages only, or a custom range (e.g. `1,3,5–8`)
- **Incremental signing** — signs documents that already have existing signatures without invalidating them
- **TSA timestamp support** — embeds a trusted timestamp from any RFC 3161 server (e.g. DigiCert)
- **Configurable appearance** — border width, which fields to display, logo position and scale

**Signature format:**
- **PAdES** (PDF Advanced Electronic Signatures) — eIDAS-compliant, accepted across all EU member states
- **QES-ready** — supports qualified electronic signatures when used with a qualified certificate on a hardware token

---

### Multi-Signer Serial Workflow

The **Workflow** tab orchestrates a signing chain across multiple signers.

- Define an **ordered list of signers** — each with their own profile
- Each signer receives an **email notification** when it is their turn
- Signer opens XignAll, signs the batch, and the next signer is automatically notified
- **Absentee handling** — skip a signer and continue the chain
- **SEAL at end of chain** — apply an organizational SEAL signature to certify the final signed document
- **Signature table replacement** — insert a marker line in the document; XignAll removes and rebuilds the entire signature table in all documents of the batch automatically
- **Shared-folder workflow transport** — workflow state synchronized through shared packages stored alongside the document batch; no server or API required

---

### Signature Verification

The **Verify** tab inspects digital signatures in any PDF.

- Shows: signer name, reason, location, timestamp, certificate issuer, certificate validity
- Detects whether the document was modified after signing
- Works on any PAdES-signed PDF, regardless of which software was used to sign it

---

### PDF Tools

Nine built-in PDF processing tools, all working on batches of files.

| Tool | Description |
|------|-------------|
| **Merge** | Combine multiple PDFs into one |
| **Split** | Split a PDF by page ranges or into individual pages |
| **Rotate** | Rotate pages (90°, 180°, 270°) — all pages or specific page numbers |
| **Watermark** | Add text or image watermark to all pages |
| **Anonymize** | Auto-redact sensitive data using regex patterns |
| **Extract Text** | Extract all text content from PDFs to `.txt` files |
| **Extract Images** | Extract all embedded images from PDFs |
| **Edit Metadata** | View and edit PDF metadata (title, author, subject, keywords, producer) |
| **Encrypt / Decrypt** | Password-protect PDFs with AES-128 encryption, or remove protection |

**Anonymization patterns (built-in):**
Automatically detects and redacts: email addresses, IBAN numbers, phone numbers, Romanian CNP (personal ID), passport numbers, bank card numbers. Supports adding custom regex patterns. International and Romanian patterns included.

---

### Signature & Stamp Extractor

The **Tools** tab includes an image processing utility for creating electronic signature logos.

- **Input**: any photo of a handwritten signature or ink stamp (JPG, PNG, BMP, TIFF)
- **Process**: removes the background automatically → outputs a transparent PNG
- **Output**: ready-to-use as the logo image in a digital signature profile
- Runs entirely offline — no external service required

---

## Server Edition — Folder Watch + SEAL + Telegram

The **Server Edition** adds automated, unattended signing via folder monitoring and Telegram remote authorization. It is designed for organizations that need a local signing infrastructure operating continuously without user interaction.

Server Edition is not a separate product — it is XignAll with additional capabilities unlocked by a server license. Documents never leave your infrastructure.

### Folder Watch — Automatic signing

XignAll monitors a configured root folder (`/SEAL/`) and its first-level subfolders. When a new file appears in any subfolder, it is processed automatically:

```
/SEAL/
├── Economic/
│   ├── invoice1.docx       ← drop file here
│   ├── invoice1.pdf        ← XignAll converts to PDF
│   └── Signed/
│       └── invoice1_signed.pdf
├── Legal/
│   └── Signed/
│       └── contract_signed.pdf
└── HR/
```

**How it works:**
1. File appears in `/SEAL/[department]/`
2. If not already a PDF, the file is **automatically converted** (DOCX, XLSX, ODT, RTF, TXT, JPG, PNG, BMP, TIFF, GIF, WEBP supported)
3. The PDF is **signed** — with the configured SEAL profile or a qualified certificate from a hardware token
4. The signed file is moved to `[department]/Signed/`
5. Files that fail are moved to `[department]/Failed/` with an error log entry

**Signing with SEAL vs. individual certificate:**
Folder Watch can sign using the organizational SEAL (eSEAL) or a qualified certificate from a hardware token. The organizational SEAL is issued to a legal entity — any employee authorized by the network administrator can trigger it, which is fully compliant with the eIDAS regulation. Using an individual qualified certificate is technically supported; however, a qualified certificate is personally bound to its holder, and whether delegated use is appropriate remains the sole responsibility of the certificate owner.

**Additional features:**
- Department-isolated signing queues — each subfolder is independent
- Optional Telegram approval before signing (admin receives notification, replies `/approve` or `/reject`)
- Compatible with shared network drives, NAS, and cloud-synced folders (Google Drive, OneDrive)
- No API, no cloud dependency, no integration required

---

### Telegram Bot — Remote signing

Authorized users send any supported file to the bot via Telegram. XignAll converts it to PDF if needed and signs it with the configured SEAL or certificate. The signed PDF is returned in the same chat — typically within seconds.

```
User sends:  photo_from_phone.jpg   [photo from phone camera]
Bot replies: Converting JPG → PDF...
Bot replies: ✅ Signing with SEAL...
Bot replies: photo_from_phone_signed.pdf   [signed PDF]

User sends:  contract.pdf   [existing PDF]
Bot replies: ✅ Signing with SEAL...
Bot replies: contract_signed.pdf   [signed PDF]
```

**Supported input via Telegram:**

| Type | Formats |
|------|---------|
| Office documents | `.docx`, `.doc`, `.odt`, `.rtf`, `.txt`, `.xlsx`, `.xls`, `.ods`, `.csv` |
| Images / Photos | `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.gif`, `.webp` |
| Phone camera | Supported — Telegram sends as compressed JPG, converted to PDF before signing |
| PDF | Signed directly, no conversion |

**Access control:**
- Whitelist-based: only pre-authorized Telegram user IDs can use the bot
- Bot silently ignores all messages from unauthorized users
- Admin commands: `/status`, `/users`, `/log`

**Signing responsibility:**
The bot signs using the organizational SEAL or a configured qualified certificate. The organizational SEAL is a legal entity credential — any authorized employee can trigger it (eIDAS-compliant). Delegating a personal qualified certificate to a shared bot is technically supported; compliance with applicable regulations is the responsibility of the certificate holder.

---

### Organizational SEAL

An **organizational SEAL** (eSEAL) is the electronic equivalent of a company stamp — applied by the legal entity, not by an individual. Under the eIDAS regulation, a qualified eSEAL has full legal force across all EU member states.

In XignAll, the SEAL is applied at the end of a signing workflow, after all individual signers have completed their signatures — certifying that the document is final and authentic.

**Signing workflow order:**
```
① Signer 1  (individual qualified certificate)
② Signer 2  (individual qualified certificate)
③ Signer N  (individual qualified certificate)
④ Organizational SEAL  ← applied last
```

**Configuration:**
- PKCS#12 (.p12) certificate or hardware PKCS#11 token
- PIN entered once — all documents sealed automatically in the session
- Wrong-PIN detection stops processing to prevent token lockout
- Any employee authorized by the network administrator can trigger the SEAL

---

## Feature comparison: Free · PRO · Server Edition

| Feature | Free | PRO | Server |
|---------|------|-----|--------|
| Single file signing | ✅ | ✅ | ✅ |
| PKCS#12 + PKCS#11 hardware token | ✅ | ✅ | ✅ |
| Single signer profile | ✅ | ✅ | ✅ |
| PDF Merge + Split | ✅ | ✅ | ✅ |
| Signature verification | ✅ | ✅ | ✅ |
| Aria AI chatbot | ✅ | ✅ | ✅ |
| macOS + Windows + Linux | ✅ | ✅ | ✅ |
| Bulk folder signing (unlimited) | ❌ | ✅ | ✅ |
| Unlimited signer profiles | ❌ | ✅ | ✅ |
| Serial multi-signer workflow | ❌ | ✅ | ✅ |
| All 9 PDF Tools + Utilities | ❌ | ✅ | ✅ |
| TSA timestamp (RFC 3161) | ❌ | ✅ | ✅ |
| Up to 3 device activations | ❌ | ✅ | ✅ |
| Folder Watch — automatic SEAL signing | ❌ | ❌ | ✅ |
| Telegram remote signing authorization | ❌ | ❌ | ✅ |
| Runs as background service | ❌ | ❌ | ✅ |
| Signing log + audit report (PDF) | ❌ | ❌ | ✅ |
| Department-isolated signing queues | ❌ | ❌ | ✅ |
| Per-organization license | ❌ | ❌ | ✅ |
| Internal .p12 certificate issuance | ❌ | ❌ | ⏳ in development |

---

## Certificates & Hardware Tokens

### PKCS#12 (software certificates)
- Supports `.p12` and `.pfx` certificate files
- PIN entered once per session, never stored on disk
- Certificate details displayed before signing: subject, issuer, validity, qualified status

### PKCS#11 (hardware USB tokens)
- Compatible with: eToken (SafeNet/Thales), SafeNet iKey, Gemalto, and any PKCS#11-compliant device
- Auto-detection of installed token drivers on Windows, macOS, Linux
- Token identified by **serial number** — stable across reboots and USB reconnects
- PIN entered once per session

### TSA (Trusted Timestamp Authority)
- Optional RFC 3161 timestamp embedded in each signature
- Compatible with DigiCert, GlobalSign, and any RFC 3161-compliant TSA server

---

## Use Cases

### Notary offices
Batch-sign entire files of deeds and notarial acts. Each document receives a visible PAdES signature with the notary's name, stamp logo, and embedded timestamp — in parallel, 20–60 documents per minute.

### Cadastral commissions
Process land registry batches: convert from `.docx` to PDF, append the official seal page, sign with the commission's qualified certificate on a hardware token, all in one automated pipeline run.

### Public administration
Dispatch documents for serial signing across multiple officials. Each official is notified by email, signs their batch, and the chain continues automatically. The final document is certified with an organizational SEAL.

### Accounting and audit firms
Sign financial statements, tax declarations, and audit reports in bulk. PKCS#12 certificates supported for firms without hardware tokens.

### Air-gapped environments
XignAll runs fully offline. No internet connection is required for signing. License validation includes a 30-day offline grace period, making it suitable for classified or isolated environments.

### Shared-folder distributed workflows
Multiple signers across different machines sign the same document batch using a shared folder (network drive, NAS, or cloud-synced folder). No server, no API, no internet required between signers.

---

## Requirements

### Runtime (end users)
- **LibreOffice** — required for document conversion (Pipeline steps 1 and 3)
  - Download: [libreoffice.org](https://www.libreoffice.org/download/download-libreoffice/)
- For PKCS#11 tokens: the token driver/middleware for your device

### Build from source
- Python 3.12
- `pip install -r requirements.txt`
- Platform build scripts: `build_mac.sh`, `build_linux.sh`, `build_win.ps1`

---

## Download

Pre-built binaries available in the [Releases](https://github.com/LiviuStoica73/XignAll-releases/releases) repository.

| Platform | File |
|----------|------|
| Windows 10/11 | `XignAll-1.3.1-win.msi` |
| macOS (Universal) | `XignAll-1.3.1-mac.dmg` |
| Linux x86_64 | `XignAll-1.3.1-linux-x86_64.tar.gz` |

A **free edition** with no time limit is available on all three platforms.

---

## Languages

Application UI and website available in: Romanian, English, French, German, Italian, Hungarian, Polish, Ukrainian, Bulgarian, Slovenian.

---

## FAQ

**Does XignAll upload my documents to a server?**
No. All processing happens locally on your machine. Documents never leave your environment. The only network call is license validation — documents, certificates, and signing keys are never transmitted.

**Does XignAll require cloud infrastructure or internet to sign?**
No. XignAll is designed as a local-first signing platform. Signing works entirely offline. License validation includes a 30-day offline grace period, making XignAll suitable for restricted or air-gapped environments.

**What is the difference between Desktop and Server Edition?**
Desktop Edition is optimized for interactive bulk signing workflows — one session, one operator.
Server Edition adds:
- Folder Watch automation (unattended signing on file arrival)
- Telegram remote signing authorization (sign from phone, no VPN)
- Organizational SEAL automation
- Department-isolated signing queues
- Signing log and audit report export

**Can signing workflows be distributed across multiple users without API integration?**
Yes. XignAll synchronizes workflow state through shared workflow packages stored alongside the document batch — using a shared folder (network drive, NAS, or cloud-synced folder). No API, no server, no internet required between signers.

**Does XignAll support organizational electronic seals (eSEAL)?**
Yes. XignAll supports qualified electronic seal application (eIDAS-compliant) at the end of distributed signing workflows. The SEAL is applied after all individual signers complete, certifying the document is final and authentic. Any employee authorized by the network administrator can trigger the SEAL — no individual certificate required.

**Can XignAll operate in isolated or air-gapped environments?**
Yes. XignAll runs fully offline. No internet connection is required for signing or document processing. The 30-day offline grace period for license validation makes it suitable for classified or restricted environments.

**What signature format does XignAll produce?**
PAdES (PDF Advanced Electronic Signatures), compliant with the eIDAS regulation. Accepted by courts, public institutions, and notary offices across all EU member states.

**Can I sign documents that already have signatures from other signers?**
Yes. XignAll uses incremental PDF updates, which preserves all existing signatures when adding a new one.

**Can I use a hardware USB token (eToken, SafeNet)?**
Yes. XignAll supports any PKCS#11-compliant hardware token. The token is identified by serial number for stability across reboots.

**What is the SEAL in Server Edition?**
SEAL refers to an organizational electronic seal — a signature applied by the organization itself (not an individual), typically at the end of a signing workflow to certify the document is complete and authentic. In the eIDAS framework this corresponds to a qualified Electronic Seal (eSEAL). Any employee authorized by the network administrator can trigger it — this is fully eIDAS-compliant.

**Can the Telegram bot sign photos taken on a phone?**
Yes. Send a photo directly from your phone camera to the bot. XignAll converts it to PDF and returns a signed document within seconds.

**Is there a macOS Apple Silicon build?**
Yes. The macOS DMG is a universal binary supporting both Apple Silicon and Intel.

---

## License

Proprietary software. All rights reserved.
© 2026 Liviu Stoica — [xignall.io](https://xignall.io) — contact@xignall.io
