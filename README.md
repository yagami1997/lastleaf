# Lastleaf

**An offline recovery toolkit for Meld Encrypt notes.**

Lastleaf is a small, standalone decryptor for notes encrypted with the [Meld Encrypt](https://github.com/meld-cp/obsidian-encrypt) Obsidian plugin. It is built for one purpose: helping you open your own encrypted notes when the original plugin is no longer close at hand.

Open `index.html`, provide the encrypted note or inline fragment, enter the password, and recover the plaintext locally in your browser.

No server. No account. No build step. No telemetry.

Created in Los Angeles on **May 23, 2026 at 8:51 PM PDT**.

## What It Does

- Decrypts Meld Encrypt whole-note JSON files.
- Decrypts inline encrypted fragments.
- Supports the known v0, v1, and v2 Meld Encrypt formats.
- Runs locally through the browser's Web Crypto API.
- Works as a static file and can be saved for offline use.

## Supported Formats

| Format | Marker | Notes |
| --- | --- | --- |
| v0 | `%%🔐 ... %%` | Earliest inline encryption format. |
| v1 | `%%🔐α ... %%` or `version: "1.0"` | Legacy CryptoHelper format. |
| v2 | `%%🔐β ... %%` or `version: "2.0"` | CryptoHelper2304 format and the current default when this tool was written. |

Whole-note encrypted files are JSON objects containing `version`, `hint`, and `encodedData`.

## Usage

Open `index.html` in a modern browser.

You can decrypt:

- a whole encrypted note file;
- a pasted Meld Encrypt JSON payload;
- an inline encrypted fragment.

Passwords and ciphertext stay on the local page. The application does not send your data anywhere.

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

## Note

Encryption is a promise made to a future self: the contents should stay private, but they should not become unreachable simply because a tool disappeared.

Lastleaf exists for that narrow space between privacy and loss. It does not try to replace Meld Encrypt, weaken its assumptions, or recover forgotten passwords. It only preserves the path back to notes you already own, encrypted with a password you still remember.

That is why this project is deliberately plain. A recovery tool should be easy to read, easy to save, and boring enough to survive years of changing platforms.

## Project Structure

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

There is no required development setup. Open the HTML file directly, or serve the directory with any static file server.

## Deployment

This repository is suitable for static hosting. The included `_headers` file is intended for Cloudflare Pages.

## Attribution

Lastleaf is an independent third-party tool. It is not affiliated with or endorsed by the Meld Encrypt project.

The decryption behavior is based on the public Meld Encrypt implementation in [`meld-cp/obsidian-encrypt`](https://github.com/meld-cp/obsidian-encrypt).

## License

MIT
