# Groot installer — download

Download the Groot installer. No login needed.

## Download

```sh
curl -L -o install-groot https://raw.githubusercontent.com/tionghieng/groot-installer-download/main/install-groot-linux-amd64
chmod +x install-groot
./install-groot
```

ARM64 (e.g. Raspberry Pi, ARM servers):

```sh
curl -L -o install-groot https://raw.githubusercontent.com/tionghieng/groot-installer-download/main/install-groot-linux-arm64
chmod +x install-groot
./install-groot
```

Verify the download with the checksums in `SHA256SUMS`:

```sh
sha256sum -c SHA256SUMS
```

## What it does

A terminal wizard that sets up Groot, a Telegram group assistant, on
your Linux machine (Docker only). It asks about your LLM, your
Telegram bot, and optionally a database, then writes its settings to
`~/.groot-installer/` and starts Groot with Docker Compose.

- `./install-groot --help` — show all options
- `./install-groot --dry-run` — walk through without writing anything
- `./install-groot --uninstall` — remove Groot

## Source

The installer source code is **not** in this repo — this repo holds
only the built executables. The source is private.
