<div align="center">

# 🍂 Lastleaf

**An offline recovery toolkit for Meld Encrypt notes**

When the original tool is gone, your notes should not be gone with it.

</div>

---

Lastleaf is a standalone, single-page decryptor for notes encrypted with the [Meld Encrypt](https://github.com/meld-cp/obsidian-encrypt) Obsidian plugin.

It exists for a narrow recovery case: you still have the encrypted notes, you still remember the password, but the original plugin or environment is no longer available. Open `index.html`, provide the encrypted content, enter the password, and recover the plaintext locally in your browser.

No server. No account. No build step. No telemetry.

Created in Los Angeles on **May 23, 2026 at 8:51 PM PDT**.

## ✦ Overview

| Property | Detail |
| --- | --- |
| 🧭 Runtime | Browser only |
| 🔐 Crypto API | Web Crypto API |
| 🌿 Network requirement | None after the page is loaded |
| 🧱 Build system | None |
| 📄 Primary file | `index.html` |
| 🗂️ Supported content | Whole-note JSON and inline fragments |

## 🚪 Usage

Open `index.html` in a modern browser.

You can decrypt:

- a whole encrypted note file;
- a pasted Meld Encrypt JSON payload;
- an inline encrypted fragment.

Passwords and ciphertext stay on the local page. Lastleaf does not upload, log, or transmit your data.

## 🔐 Supported Formats

| Format | Marker | Notes |
| --- | --- | --- |
| v0 | `%%🔐 ... %%` | Earliest inline encryption format. |
| v1 | `%%🔐α ... %%` or `version: "1.0"` | Legacy CryptoHelper format. |
| v2 | `%%🔐β ... %%` or `version: "2.0"` | CryptoHelper2304 format and the current default when this tool was written. |

Whole-note encrypted files are JSON objects containing `version`, `hint`, and `encodedData`.

## 🪶 Design Philosophy

Lastleaf is designed to be boring in the best sense of the word.

**Local first.** Recovery should not depend on an account, a server, or a third-party API. The page can be opened from disk and used offline.

**Auditable by inspection.** The implementation lives in `index.html`. A future user should be able to open the file, read the source, and understand what is being run.

**Small enough to preserve.** A recovery tool should be easy to copy into a private archive, a repository, or a long-term backup without carrying a toolchain with it.

**Respectful of the original model.** Lastleaf does not recover forgotten passwords and does not weaken Meld Encrypt. It only preserves access for the person who already has both the ciphertext and the password.

## 📝 Note

Encryption is a promise made across time. It protects a private present, but it also asks the future to remember enough context to open what was sealed.

Software does not always keep that promise for us. Plugins disappear, APIs drift, platforms change shape, and old machines become hard to recreate. Lastleaf is a small answer to that fragility: keep the recovery path simple enough that it can survive without ceremony.

The point is not to distrust tools. The point is to avoid confusing a tool with ownership. If the notes are yours, the password is yours, and the ciphertext is yours, the ability to return to them should remain yours as well.

## 🛡️ Security Boundaries

Lastleaf can help when:

- the Meld Encrypt plugin is unavailable;
- Obsidian plugin compatibility changes;
- you are recovering notes on a new machine;
- you want an offline, auditable decryptor for your own archive.

Lastleaf cannot help when:

- the password has been forgotten;
- a future Meld Encrypt version introduces a new encryption format;
- the local copy of `index.html` has been modified maliciously.

Before using a downloaded copy with real notes, inspect `index.html` directly. The decryption logic is part of the page source.

## 🚀 Deployment Guide

Lastleaf is a static site. It can be deployed anywhere that serves plain files.

### ☁️ Cloudflare Pages

Use a normal Pages project, not a Worker Git deployment.

| Setting | Value |
| --- | --- |
| Framework preset | `None` |
| Build command | Leave empty |
| Build output directory | `/` |
| Root directory | `/` |

The included `_headers` file is intended for Cloudflare Pages. No `wrangler.jsonc` file is required.

### 🌐 Static Hosts

For any other static host, serve the repository root. The only required runtime file is `index.html`; the favicon assets and `lastleaf.zip` are optional supporting files.

### 💾 Local Use

Open `index.html` directly, or serve the directory with any static file server:

```sh
python3 -m http.server
```

## 🧩 Project Structure

```text
lastleaf/
├── index.html
├── favicon.svg
├── favicon-32.png
├── favicon-180.png
├── lastleaf.zip
├── _headers
├── LICENSE
└── README.md
```

## 🙏 Attribution

Lastleaf is an independent third-party tool. It is not affiliated with or endorsed by the Meld Encrypt project.

The decryption behavior is based on the public Meld Encrypt implementation in [`meld-cp/obsidian-encrypt`](https://github.com/meld-cp/obsidian-encrypt).

## 📜 License

Released under the [MIT License](LICENSE).

---

<div align="center">

Lastleaf is made for future access, quiet recovery, and ownership that survives its tools.

<em>Seek truth from facts.</em>

</div>
