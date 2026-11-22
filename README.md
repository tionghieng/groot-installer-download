# Groot — Telegram group assistant

**Groot** (GROup bOT) is a personalised Telegram assistant that lives
in your groups and helps everyone in them. It runs on your own
machine, in Docker, 24/7, and can use any LLM — OpenAI, Anthropic,
Google Gemini, DeepSeek, a local Ollama model, or any OpenAI-compatible
custom model.

You talk to it in Telegram: in a 1:1 chat with the bot, or by
@mentioning it in a group. It only replies in groups when mentioned
(or when you use `/ask`), so it never spams your chats.

To run it, download the installer below and run it once — it asks a
few questions (your LLM, your Telegram bot), writes the settings,
and starts Groot in Docker. If you'd rather not use the terminal,
download the launcher (`install-groot.desktop`) instead and
double-click it: it opens a terminal and runs the installer for you.

## What Groot does

- **Chat** — ask questions, get answers from the LLM you chose
- **Family groups** — shared calendar and reminders, shopping list,
  meal ideas, family summary, shared notes, polls
- **Friends groups** — meetup and trip planning, split expenses,
  recommendations, games
- **Work groups** — meeting notes and action items, task tracking,
  scheduling
- **Memory** — per-group memory, so each group has its own context
- **Calendar** — one shared calendar per group (Google Calendar, or
  Outlook for work groups), with `/today`, `/week`, and reminders
  before events

Private tools (changing the model, adding a database, viewing logs)
stay only in your 1:1 chat with the bot. Only the admin can change
settings.

## The installer

This repo holds the **Groot installer** — a small program that sets
Groot up on a Linux machine. It is a terminal wizard: it asks a few
questions, one at a time, in plain language, then writes the settings
and starts Groot in Docker.

This repo holds only the built executables. The Groot bot ships as a
Docker image that the installer pulls.

## Download

Pick the build for your machine — most PCs and
servers are amd64, Raspberry Pi and ARM servers are arm64.

The installer downloads into `~/.groot-installer/` — the same folder
where it later keeps its settings (`.env`, `docker-compose.yml`).
Create the folder first, then download into it:

```sh
# amd64 (most PCs / servers)
mkdir -p ~/.groot-installer
curl -L -o ~/.groot-installer/install-groot https://raw.githubusercontent.com/tionghieng/groot-installer-download/main/install-groot-linux-amd64
chmod +x ~/.groot-installer/install-groot
~/.groot-installer/install-groot
```

```sh
# arm64 (Raspberry Pi, ARM servers)
mkdir -p ~/.groot-installer
curl -L -o ~/.groot-installer/install-groot https://raw.githubusercontent.com/tionghieng/groot-installer-download/main/install-groot-linux-arm64
chmod +x ~/.groot-installer/install-groot
~/.groot-installer/install-groot
```

### Double-click launcher

Prefer double-clicking? Download `install-groot.desktop` into the
same folder, then double-click it — a terminal opens and the
installer runs. (On first use your file manager may ask you to trust
it: right-click the file → Allow Launching, then double-click.)

```sh
curl -L -o ~/.groot-installer/install-groot.desktop https://raw.githubusercontent.com/tionghieng/groot-installer-download/main/install-groot.desktop
chmod +x ~/.groot-installer/install-groot.desktop
```

Verify the download with the checksums in `SHA256SUMS`:

```sh
cd ~/.groot-installer
curl -L -o SHA256SUMS https://raw.githubusercontent.com/tionghieng/groot-installer-download/main/SHA256SUMS
sha256sum install-groot
```

Compare the hash it prints with the line for your build in
`SHA256SUMS` — they must match.

## Before you start

- A Linux machine (Ubuntu works) that stays on, with
  [Docker and Docker Compose](https://docs.docker.com/engine/install/)
  installed
- A Telegram account — you will create a bot with
  [@BotFather](https://t.me/BotFather)
- An LLM API key (e.g. DeepSeek, OpenAI) — or Ollama running locally

## What the installer asks

- **Step 0** — Checks your machine: Docker, Compose, Postgres, Ollama
- **Step 1** — Which LLM Groot should use first (a working key is
  required to continue), then pick a model from the list
- **Step 2** — Your Telegram bot token from @BotFather, and your own
  Telegram user ID (so only you can change settings)
- **Step 3** — Database, optional — SQLite is the default, just a
  file, no setup. Postgres or MySQL if you already run one.
- **Step 4** — Writes a private `.env` and `docker-compose.yml` to
  `~/.groot-installer/`, and logs in to the image registry
  automatically
- **Step 5** — Start Groot now? Say yes and it pulls the image and
  starts the bot

Then send `/start` to your bot in Telegram. If it replies, you are
done. Add the bot to a group as admin, and @mention it to talk to it.

## Help

```sh
./install-groot --help       # show all options
./install-groot --dry-run    # walk through without writing anything
./install-groot --check-only # check Docker only
./install-groot --uninstall  # remove Groot completely
```

Logs: `cd ~/.groot-installer && docker compose logs -f agent`
