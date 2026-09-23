---
title: Offline Cold Wallet Tool
description: 
published: true
date: 2026-09-23T13:16:34.638Z
tags: 
editor: markdown
dateCreated: 2026-09-23T13:16:34.638Z
---

# Saito Static Key Generator

> TL;DR: go to the [Saito Offline Wallet Tool](https://saito.io/saito/tools/key-gen/index.html), disconnect from any network and follow the instructions.

The [Saito Offline Wallet Tool](https://saito.io/saito/tools/key-gen/index.html) creates or restores Saito wallet keys locally in your browser. It is intended for preparing cold-storage wallets on a disconnected computer.

The entire tool is contained in one `index.html` file, including its JavaScript, styles, recovery-word list, and QR-code generator. No installation, server, or external libraries are needed to run the downloaded file. The utility does not transmit keys or automatically save them.

![Saito Offline Wallet Tool showing the Generate new and Restore phrase tabs](images/saito-key-generator.png)

## Download and verify the file

**Verify the downloaded file before opening it or entering a recovery phrase.**

Download [index.html](https://saito.io/saito/tools/key-gen/index.html) directly. On Linux or macOS, you can download it from a terminal:

```sh
curl --fail --location --output index.html https://saito.io/saito/tools/key-gen/index.html
```

Use the original HTML file, rather than a browser-generated “complete webpage” or an edited copy: saving or reformatting the contents can change its checksum.

The SHA-256 checksum of `web/saito/tools/key-gen/index.html`, verified against the public download on **23 September 2026**, is:

```text
cfcf677c55b5c74df4e021648de0acb3f14690d21a1fd8ab054fffb94438de67
```

This checksum covers the **entire file**, including the embedded code. It applies to this exact version; any change to the file requires an updated checksum.

In the folder containing the downloaded `index.html`, run the appropriate command:

**Linux**

```sh
sha256sum index.html
```

**macOS**

```sh
shasum -a 256 index.html
```

**Windows PowerShell**

```powershell
Get-FileHash -Algorithm SHA256 .\index.html
```

Compare the complete 64-character hash with the value above. Uppercase and lowercase letters represent the same hash. Every character must match.

Linux users can also check automatically:

```sh
printf '%s\n' 'cfcf677c55b5c74df4e021648de0acb3f14690d21a1fd8ab054fffb94438de67  index.html' | sha256sum --check
```

The expected result is `index.html: OK`.

**If the checksum differs, do not use the file.** Obtain a fresh copy and confirm the published checksum for that version through a trusted Saito source. A matching checksum establishes that the bytes match the published version; its value depends on trusting the source of the expected checksum.

## Generate or restore keys offline

1. Download the file and verify its checksum. If you transfer it to another computer, verify it again there.
2. Use a clean computer and an up-to-date browser without extensions. Disconnect Wi-Fi, Bluetooth, and network cables.
3. Open the verified `index.html` directly in your browser. The address should begin with `file://`.
4. Choose **Generate new → Generate keys**, or **Restore phrase**, enter an existing compatible 24-word recovery phrase, and select **Restore keys**.
5. Use **Reveal secrets** to record the private key and recovery phrase. Check your backup carefully; restoring the phrase should reproduce the same public key.
6. Store the backup securely offline. When finished, select **Clear**, close the browser, and shut down the device.

New wallets use the browser's cryptographic random-number generator to create a 24-word English BIP39 phrase with 256 bits of entropy. The tool produces a Saito public key, a private key, and the recovery phrase, with QR codes for the public and private keys. Secrets are hidden on screen until revealed.

Restoration checks the phrase's words and checksum, then decodes its entropy directly into the 32-byte private key using Saito's recovery convention. A BIP39 phrase from another cryptocurrency wallet should not be assumed to restore the same keys here.

Generation is disabled while the browser reports that it is online, unless **Allow key creation while online** is selected. Leave that override unchecked for cold storage. The status badge reflects the browser's network report; physically disconnect the computer yourself.

The public key can be shared to receive funds. **Anyone with the private key or recovery phrase can control the wallet.** The tool also offers **Print** and **Download PDF** backups; both include the secrets even when they are hidden on screen. Keep those backups offline and account for copies retained in printer queues, downloads, or synced folders.
