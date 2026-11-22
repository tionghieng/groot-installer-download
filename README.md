# Groot — Telegram group assistant

**Groot** (GROup bOT) is a personalised Telegram assistant that lives
in your groups and helps everyone in them. It runs on your own
machine, in Docker, 24/7, and can use any LLM — OpenAI, Anthropic,
Google Gemini, DeepSeek, a local Ollama model, or any OpenAI-compatible
custom model.

You talk to it in Telegram: in a 1:1 chat with the bot, or by
@mentioning it in a group. It only replies in groups when mentioned
(or when you use `/ask`), so it never spams your chats.

To run it, download the **installer** below and run it once — it asks a
few questions (your LLM, your Telegram bot), writes the settings,
then Docker downloads the Groot image and starts Groot. In addition, you can download the
**launcher** (`install-groot.desktop`) and double-click it: it opens a
terminal and runs the installer for you.

This repo holds only the built executables. The Groot bot ships as a
Docker image that the installer pulls.

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

## Download

1. **Installer** — pick the build for your machine: most PCs and
   servers are amd64, Raspberry Pi and ARM servers are arm64.

   The installer downloads into `~/.groot-installer/` — the same
   folder where it later keeps its settings (`.env`,
   `docker-compose.yml`). Create the folder first, then download
   into it:

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

2. **Launcher** — prefer double-clicking? Download
   `install-groot.desktop` into the same folder, then double-click
   it — a terminal opens and the installer runs. (On first use your
   file manager may ask you to trust it: right-click the file →
   Allow Launching, then double-click.)

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

## Prerequisite

### System Requirement

- A Linux machine (Ubuntu works) that stays on, with
  [Docker and Docker Compose](https://docs.docker.com/engine/install/)
  installed

### Groot Requirement

- A Telegram account — you will create a bot with
  [@BotFather](https://t.me/BotFather)
- An LLM API key (e.g. DeepSeek, OpenAI) — or Ollama running locally

### Nice to Have Requirement

- A Postgres or MySQL database, if you want one instead of the
  built-in SQLite (which needs no setup)
- A web search provider — SearXNG, DuckDuckGo, Tavily, or Brave
  (Tavily and Brave need an API key). Without one, Groot can't
  search the web
- A Google service account, if you want Google Calendar in your
  groups — every chat already gets a built-in calendar

## Using Groot

After the installer finishes, send `/start` to your bot in Telegram.
If it replies, you are done.

Add the bot to a group as admin, then @mention it to talk to it.
It only replies in groups when mentioned, so it never spams your
chats.

In your 1:1 chat with the bot you can change its settings — the
model, web search, calendar, and more. Only you, the admin, can
change settings.

To update Groot, change its setup, back it up, or remove it, just
run the installer again — it offers all of those on its menu.

## Help

```sh
./install-groot --help       # show all options
./install-groot --dry-run    # walk through without writing anything
./install-groot --check-only # check Docker only
./install-groot --uninstall  # remove Groot completely
```

Logs: `cd ~/.groot-installer && docker compose logs -f agent`
