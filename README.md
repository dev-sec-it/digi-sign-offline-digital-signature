# DigiSigner by DEV SEC IT

Enterprise PAdES Digital Signature Certificate (DSC) Signer, Hardware Token Bridge, and Document Certification Suite for Microsoft Windows and Chromium Browsers.

- **Publisher:** DEV SEC IT
- **Website:** https://in.devsecit.com
- **Support Email:** support@devsecit.com
- **Phone:** +91 8101 979855
- **Headquarters:** N.S. Colony, Raiganj, Uttar Dinajpur, West Bengal 733134, India

---

## Package Contents (`deploy/`)

- `DigiSigner-Setup-v1.0.0.exe` — Multi-step Windows Setup Installer (NSIS). Installs the DigiSigner desktop application and automatically registers the Chrome, Microsoft Edge, Brave, and Chromium Native Messaging Host.
- `DigiSigner-Extension-v1.0.0.crx` — Signed/packaged Chromium Browser Extension (`CRX3`). Uses the local hardware bridge installed by `DigiSigner-Setup-v1.0.0.exe`.
- `README.md` — End-user installation, extension deployment, and PAdES signing guide.

---

## 1. Windows Installation (Multi-Step Setup)

Run **`DigiSigner-Setup-v1.0.0.exe`** and complete the installation wizard:

1. **Welcome** — Overview of DigiSigner by DEV SEC IT.
2. **License Agreement** — Review and accept the DEV SEC IT End-User Software License Agreement.
3. **Install Scope** — Choose *Current User* (`HKCU`) or *All Users* (`HKLM`).
4. **Destination Folder** — Select installation directory.
5. **Install & Bridge Registration** — Installs files cleanly and automatically executes `digiSigner.exe --register-host` so the browser extension communicates silently with your USB DSC token.
6. **Finish** — Launch DigiSigner directly from the installer or Start Menu (`DEV SEC IT -> DigiSigner`).

---

## 2. Installing & Sharing the Browser Extension (`.crx`)

Share **`DigiSigner-Extension-v1.0.0.crx`** together with **`DigiSigner-Setup-v1.0.0.exe`**.

1. Install **`DigiSigner-Setup-v1.0.0.exe`** on the Windows workstation first so the hardware DSC native bridge (`com.devsecit.digisigner`) is registered.
2. Open Chrome or Edge:
   - **Enterprise / Policy deployment:** Configure `ExtensionInstallForcelist` / `ExtensionInstallSources` referencing `DigiSigner-Extension-v1.0.0.crx`.
   - **Manual installation:** Open `chrome://extensions` or `edge://extensions`, turn on **Developer mode**, and drag `DigiSigner-Extension-v1.0.0.crx` onto the Extensions page (or install via organization policy if external `.crx` prompts are restricted by Chrome).
3. Click the **DigiSigner** toolbar icon. Chrome wakes the registered background bridge silently and detects plugged-in USB DSC tokens automatically.

---

## 3. Document Certification & Multi-Sign Modes

DigiSigner applies compliant PAdES CAdES-detached SHA-256 signatures with Windows CryptoAPI / CNG hardware PIN prompts:

- **Final Seal (`DocMDP P=1`, Multi-Sign OFF):** Certifies the document and applies `/Lock << /Type /SigFieldLock /Action /All >>`. Any edit, form change, or subsequent signature invalidates the seal.
- **Multi-Sign (`DocMDP P=2`, Multi-Sign ON):** Certifies the document against any content modifications while permitting sequential co-signers. When subsequent signers sign the PDF in DigiSigner, existing `/AcroForm` signature fields, page `/Annots`, and `/Perms` certification entries are preserved so all earlier signatures remain valid.

---

## 4. Supported Hardware Tokens & PIN Security

- Compatible with Windows CryptoAPI / CNG minidrivers, including **HyperPKI (HYP2003)**, **Feitian ePass2003**, **Watchdata PROXKey**, and **mToken**.
- Private key cryptographic operations occur strictly inside your hardware USB token. The token vendor's native Windows PIN dialog prompts for authentication; DigiSigner never reads, logs, or stores your PIN.

---

Copyright (c) 2026 DEV SEC IT. All rights reserved.

