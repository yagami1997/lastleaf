# Lastleaf

> When the original tool is gone, you can still open your own notes.

Lastleaf is a small, standalone recovery decryptor for notes encrypted with the [Meld Encrypt](https://github.com/meld-cp/obsidian-encrypt) Obsidian plugin.

It is a single-page web tool. Open `index.html`, paste or select encrypted content, enter the password, and recover the plaintext locally in your browser. There is no server, account, package manager, build step, analytics, or telemetry.

Created in Los Angeles on **May 23, 2026 at 8:51 PM PDT**.

## Note

Encryption is an act of trust in the future. We encrypt because some things should remain private, but privacy should not turn into accidental loss just because a plugin is abandoned, a platform changes, or an old development environment disappears.

Lastleaf exists for that narrow but important case: you still have the encrypted notes, you still know the password, but the original tool is no longer conveniently available. The goal is not to replace Meld Encrypt or weaken its model. The goal is to preserve access to your own writing through a quiet, auditable, offline artifact that can survive longer than any one app, maintainer, or hosting account.

This project is intentionally plain. Its value comes from being easy to inspect, easy to save, and easy to run years later.

## What It Supports

Lastleaf decrypts the known Meld Encrypt formats:

| Format | Marker | Notes |
| --- | --- | --- |
| v0 | `%%🔐 ... %%` | Earliest inline encryption format. |
| v1 | `%%🔐α ... %%` or `version: "1.0"` | Legacy CryptoHelper format. |
| v2 | `%%🔐β ... %%` or `version: "2.0"` | CryptoHelper2304 format and the current default when this tool was written. |

Whole-note encrypted files are JSON objects containing `version`, `hint`, and `encodedData`.

## How To Use

Open `index.html` in a modern browser.

You can decrypt either:

- a whole encrypted note file;
- a pasted Meld Encrypt JSON payload;
- an inline encrypted fragment.

All cryptographic work happens through the browser's Web Crypto API. Passwords and ciphertext remain on the local page.

## Security Boundaries

Lastleaf can help when:

- the Meld Encrypt plugin is unavailable;
- Obsidian plugin compatibility changes;
- you are recovering notes on a new machine;
- you want an offline, auditable decryptor for your own archive.

Lastleaf cannot help when:

- the password has been forgotten;
- a future Meld Encrypt version introduces a new encryption format;
- the copy of `index.html` you are using has been modified maliciously.

Before using a downloaded copy with real notes, inspect `index.html` directly. The decryption logic is part of the page source.

## Project Structure

```text
lastleaf/
├── index.html
├── favicon.svg
├── favicon-32.png
├── favicon-180.png
├── lastleaf.zip
├── _headers
└── README.md
```

There is no required development setup. Open the HTML file directly, or serve the directory with any static file server.

## Deployment

This repository is suitable for static hosting. The included `_headers` file is intended for Cloudflare Pages.

## Attribution

Lastleaf is an independent third-party tool. It is not affiliated with or endorsed by the Meld Encrypt project.

The decryption behavior is based on the public Meld Encrypt implementation in [`meld-cp/obsidian-encrypt`](https://github.com/meld-cp/obsidian-encrypt).

## License

MIT
