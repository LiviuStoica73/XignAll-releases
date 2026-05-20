# XignAll — Batch Digital PDF Signing in Your Environment

**Prepare · Sign · Verify · Automate** — Desktop application for batch digital PDF signing with precise coordinate placement. Documents never leave your machine.

[![Download](https://img.shields.io/badge/Download-v1.3.1-blue?style=flat-square)](https://github.com/LiviuStoica73/XignAll-releases/releases)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey?style=flat-square)]()
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)]()

---

## What is XignAll?

XignAll is a desktop application for organizations that sign between dozens and thousands of PDF documents per day. It automates the full document signing workflow — from raw source files to signed, verified PDFs — entirely on your machine, with no cloud uploads and no external signing platform.

Supported on **Windows 10/11**, **macOS** (Apple Silicon + Intel), and **Linux** (Ubuntu 22.04+).

---

## Table of Contents

- [Document Preparation (Pipeline)](#document-preparation-pipeline)
- [Digital Signing](#digital-signing)
- [Multi-Signer Serial Workflow](#multi-signer-serial-workflow)
- [Signature Verification](#signature-verification)
- [PDF Tools](#pdf-tools)
- [Signature & Stamp Extractor](#signature--stamp-extractor)
- [Server Edition — Folder Watch + SEAL](#server-edition--folder-watch--seal)
- [Telegram Bot — Remote Signing](#telegram-bot--remote-signing)
- [Certificates & Hardware Tokens](#certificates--hardware-tokens)
- [Use Cases](#use-cases)
- [Requirements](#requirements)
- [Download](#download)
- [FAQ](#faq)

---

## Document Preparation (Pipeline)

The **Prepare** tab processes source documents in bulk before signing.

### Supported input formats
`.doc`, `.docx`, `.odt`, `.rtf`, `.txt`, `.html`, `.xlsx`, `.xls`, `.ods`, `.csv`

### Pipeline steps (each independently enabled/disabled)

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

## Digital Signing

The **Sign** tab applies visible digital signatures to entire folders of PDFs.

### Signature capabilities
- **Batch signing** — sign an entire folder (or recursive subfolders) in one operation
- **20–60 documents per minute** depending on hardware and file size
- **Precise coordinate placement** — drag-and-drop on live PDF preview, saved per signer profile
- **Visible signature appearance**: signer name, reason, location, date, logo image
- **Multiple signer profiles** — switch between profiles in one click
- **Page range selection** — sign all pages, even/odd pages only, or a custom range (e.g. `1,3,5–8`)
- **Incremental signing** — signs documents that already have existing signatures without invalidating them
- **TSA timestamp support** — embeds a trusted timestamp from any RFC 3161 server (e.g. DigiCert)
- **Configurable appearance** — border width, which fields to display, logo position and scale

### Signature format
- **PAdES** (PDF Advanced Electronic Signatures) — eIDAS-compliant, accepted across all EU member states
- **QES-ready** — supports qualified electronic signatures when used with a qualified certificate on a hardware token

---

## Multi-Signer Serial Workflow

The **Workflow** tab orchestrates a signing chain across multiple signers.

- Define an **ordered list of signers** — each with their own profile
- Each signer receives an **email notification** when it is their turn
- Signer opens XignAll, signs the batch, and the next signer is automatically notified
- **Absentee handling** — skip a signer and continue the chain
- **SEAL at end of chain** — apply an organizational SEAL signature to certify the final signed document
- **Signature table replacement** — insert a marker line in the document; XignAll removes and rebuilds the entire signature table in all documents of the batch automatically

---

## Signature Verification

The **Verify** tab inspects digital signatures in any PDF.

- Shows: signer name, reason, location, timestamp, certificate issuer, certificate validity
- Detects whether the document was modified after signing
- Works on any PAdES-signed PDF, regardless of which software was used to sign it

---

## PDF Tools

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

### Anonymization patterns (built-in)
Automatically detects and redacts: email addresses, IBAN numbers, phone numbers, Romanian CNP (personal ID), passport numbers, bank card numbers. Supports adding custom regex patterns. International and Romanian patterns included.

---

## Signature & Stamp Extractor

The **Tools** tab includes an image processing utility for creating electronic signature logos.

- **Input**: any photo of a handwritten signature or ink stamp (JPG, PNG, BMP, TIFF)
- **Process**: removes the background automatically → outputs a transparent PNG
- **Output**: ready-to-use as the logo image in a digital signature profile
- Runs entirely offline — no external service required

This allows organizations to embed a scanned handwritten signature or official rubber stamp image directly inside the visible digital signature, as a transparent PNG layer.

---

## Server Edition — Folder Watch + SEAL

The **Server Edition** adds automated, unattended signing via folder monitoring.

### How it works

XignAll monitors a configured root folder (`/SEAL/`) and its **first-level subfolders**. When a new file appears in any subfolder:

1. If not already a PDF, the file is **automatically converted to PDF**
2. The PDF is **signed with the configured SEAL profile**
3. The signed file is moved to `[subfolder]/Signed/`
4. Files that fail processing are moved to `[subfolder]/Failed/` with an error log entry

### Supported input formats (auto-converted before signing)
`.docx`, `.doc`, `.odt`, `.rtf`, `.txt`, `.xlsx`, `.xls`, `.ods`, `.csv`, `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.gif`, `.webp`

### SEAL configuration
- Dedicated SEAL signer profile (PKCS#12 or PKCS#11 hardware token)
- PIN/password stored encrypted — entered once and secured at rest
- **Wrong PIN detection**: watch stops automatically to prevent token lockout
- Atomic PDF output write — no partial files on crash
- Path traversal protection on all file operations

### Combined workflow (internal signers + SEAL)
- Internal signers (from Workflow tab) sign in sequence first
- SEAL is applied last, certifying the fully-signed final document

---

## Telegram Bot — Remote Signing

The **Server → Telegram** panel runs a Telegram bot that receives documents and signs them with SEAL automatically.

### What it does

Authorized users send any supported file (document, spreadsheet, or photo) to the bot via Telegram. XignAll converts it to PDF if needed and signs it with the configured SEAL profile. The signed PDF is sent back to the user in the same chat — typically within seconds.

### Supported input (via Telegram)

| Type | Formats |
|------|---------|
| Office documents | `.docx`, `.doc`, `.odt`, `.rtf`, `.txt`, `.xlsx`, `.xls`, `.ods`, `.csv` |
| Images / Photos | `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.gif`, `.webp` |
| Phone camera | Supported — Telegram sends as compressed JPG |
| PDF | Signed directly, no conversion |

### Access control
- **Whitelist-based**: only pre-authorized Telegram user IDs can use the bot
- Admin commands: `/status`, `/users`, `/log`
- Multi-instance conflict detection: prevents duplicate bots running simultaneously

### Example use case
A notary photographs a document with their phone and sends it to the bot. Within seconds they receive a SEAL-signed PDF — without opening a computer, without accessing a shared drive, and without any document leaving the organization's server.

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
No. All processing happens locally on your machine. Documents never leave your environment.

**What signature format does XignAll produce?**
PAdES (PDF Advanced Electronic Signatures), compliant with the eIDAS regulation. Accepted by courts, public institutions, and notary offices across all EU member states.

**Can I sign documents that already have signatures from other signers?**
Yes. XignAll uses incremental PDF updates, which preserves all existing signatures when adding a new one.

**Does it work on air-gapped (offline) computers?**
Yes. No internet connection is required for signing. The license includes a 30-day offline grace period.

**Can I use a hardware USB token (eToken, SafeNet)?**
Yes. XignAll supports any PKCS#11-compliant hardware token. The token is identified by serial number for stability across reboots.

**What is the SEAL in Server Edition?**
SEAL refers to an organizational electronic seal — a signature applied by the organization itself (not an individual), typically at the end of a signing workflow to certify the document is complete and authentic. In the eIDAS framework this corresponds to an Electronic Seal (eSeal).

**Can the Telegram bot sign photos taken on a phone?**
Yes. Send a photo directly from your phone camera to the bot. XignAll converts it to PDF and returns a SEAL-signed document within seconds.

**Is there a macOS Apple Silicon build?**
Yes. The macOS DMG is a universal binary supporting both Apple Silicon and Intel.

---

## License

Proprietary software. All rights reserved.
© 2026 Liviu Stoica — [xignall.io](https://xignall.io) — contact@xignall.io
