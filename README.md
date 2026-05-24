# Lastleaf

Lastleaf is a standalone, browser-based recovery decryptor for notes encrypted with the [Meld Encrypt](https://github.com/meld-cp/obsidian-encrypt) Obsidian plugin.

It is designed as an emergency escape hatch: if the original plugin disappears, breaks, or is unavailable on a future machine, you can still decrypt your own notes as long as you remember the password.

## Features

- Decrypts Meld Encrypt whole-note JSON files.
- Decrypts inline encrypted fragments.
- Supports the known v0, v1, and v2 Meld Encrypt formats.
- Runs entirely in the browser with the Web Crypto API.
- Has no build step, package manager, backend, analytics, or telemetry.
- Can be saved and used offline by opening `index.html`.

## Usage

Open `index.html` in a modern browser.

You can either select an encrypted note file or paste encrypted Meld Encrypt content directly into the page. Enter the password used by Meld Encrypt, then decrypt the note or inline fragment.

Passwords and ciphertext are processed locally in the browser. The application does not send data to a server.

## Supported Formats

| Format | Meld Encrypt marker | Notes |
| --- | --- | --- |
| v0 | `%%🔐 ... %%` | Earliest inline encryption format. |
| v1 | `%%🔐α ... %%` or file `version: "1.0"` | Legacy CryptoHelper format. |
| v2 | `%%🔐β ... %%` or file `version: "2.0"` | CryptoHelper2304 format and current default at the time this tool was written. |

Whole-note encrypted files are JSON objects containing `version`, `hint`, and `encodedData`.

## Security Model

Lastleaf is a recovery tool, not a password recovery service.

It can help when:

- the Meld Encrypt plugin is no longer maintained;
- Obsidian plugin compatibility changes;
- you are setting up a new machine without the original plugin environment;
- you need an auditable offline decryptor for your own encrypted notes.

It cannot help when:

- the password is forgotten;
- a future Meld Encrypt version changes the encryption format;
- the local copy of this tool has been tampered with.

Before trusting a downloaded copy with real notes, inspect `index.html` directly. The decryptor logic is contained in the page source.

## Local Development

There is no development toolchain required.

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

For local testing, open `index.html` directly or serve the directory with any static file server.

## Deployment

This repository is suitable for static hosting. The included `_headers` file is intended for Cloudflare Pages.

## Attribution

Lastleaf is an independent third-party tool. It is not affiliated with or endorsed by the Meld Encrypt project.

The decryption behavior is based on the public Meld Encrypt implementation in [`meld-cp/obsidian-encrypt`](https://github.com/meld-cp/obsidian-encrypt).

## License

MIT
