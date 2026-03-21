# Kalshi Alert Bot

> Real-time price and market alerts for Kalshi via Telegram. Get notified the moment a market hits your target price, moves sharply, or a new market opens in your category - no trading, just instant alerts.

*Last updated: March 2026*

## What is Kalshi Alert Bot?

Kalshi Alert Bot monitors Kalshi markets and sends instant notifications to your Telegram (or Discord) when configured conditions are triggered. No auto-trading, no API keys for order placement - just your API key for reading market data and a Telegram bot token.

Set price alerts, volume spike alerts, new market alerts, and sharp move alerts. The bot runs in the background, checks Kalshi every few seconds, and messages you the moment something worth watching happens.

---

## Alert Types

**Price alerts** - notify when a market crosses your target YES or NO price

**Sharp move alerts** - notify when a market moves more than X% within the last N minutes (unusual activity signal)

**New market alerts** - notify when Kalshi opens a new market in your configured categories (politics, sports, crypto, economics)

**Whale alerts** - notify when order book depth on a market drops suddenly, indicating a large fill

**Resolution alerts** - notify when a tracked market resolves, with the final YES/NO outcome

**Daily summary** - sends a morning digest of all open tracked markets and their overnight price changes

---

## Engine Features

* **Telegram integration** - instant message to your private chat or group channel
* **Discord integration** - webhook-based alerts to your Discord server (optional)
* **Multi-market tracking** - watch up to 50 markets simultaneously
* **Category subscriptions** - auto-add new markets in configured categories without manual setup
* **Alert cooldown** - prevent duplicate alerts within a configurable window
* **Alert history** - all triggered alerts logged locally with timestamp and market details

---

## Two Ways to Run It

| | Windows App | Python Bot |
|---|---|---|
| **Setup** | Double-click | `pip install` + config |
| **Alerts** | Telegram + Discord | Customizable |
| **Config** | `config.toml` | Direct code access |
| **Logs** | Dashboard | JSON alert log |

## Download

| Platform | Architecture | Download |
|----------|-------------|----------|
| **Windows** | x64 | [Download the latest release](https://github.com/5000demongoat/kalshi-alert-bot/releases) |

---

## Quick Start

```
# 1. Download from Releases
# 2. Edit config.toml - set Kalshi API key, Telegram bot token, alert rules
# 3. Run Alert Bot - monitoring starts immediately
```

### Python

```bash
cd kalshi-alert-bot/python
pip install -r requirements.txt
python kalshi-alert-bot-v.1.0.6.py
```

---

## How It Works

![kalshi alert bot pipeline](https://github.com/user-attachments/assets/77f24728-ae9d-4f21-8ba5-d91e5a317ff1)

Four stages per cycle:

1. **Fetch** - pulls current prices for all tracked markets from Kalshi API
2. **Evaluate** - checks each market against configured alert rules
3. **Trigger** - marks alerts that meet conditions, applies cooldown filter
4. **Deliver** - sends formatted Telegram/Discord message with market details

### Config Reference

```toml
[monitoring]
poll_interval_seconds = 10
max_tracked_markets = 50

[alert_types]
price_alerts = true
sharp_move_alerts = true
new_market_alerts = true
whale_alerts = true
resolution_alerts = true
daily_summary = true
daily_summary_time = "08:00"

[price_alert_rules]
# Add individual market alerts here
[[price_alert_rules.markets]]
market_title_contains = "Federal Reserve"
alert_if_yes_above = 0.70
alert_if_yes_below = 0.25

[sharp_move]
min_move_pct = 8.0
window_minutes = 15

[new_market]
categories = ["politics", "economics", "sports", "crypto"]

[cooldown]
alert_cooldown_minutes = 30

[kalshi]
api_key = ""
api_secret = ""
environment = "prod"

[telegram]
bot_token = ""
chat_id = ""

[discord]
webhook_url = ""
enabled = false
```

---

## Alert Message Format

**Price alert:**
```
KALSHI ALERT - Price Target Hit

Market: Will the Federal Reserve cut rates at the May 2026 meeting?
YES Price: 0.72 (your alert: above 0.70)
Change from open: +12.3%
Time: 2026-03-21 14:32 UTC

kalshi.com/markets/...
```

**Sharp move alert:**
```
KALSHI ALERT - Sharp Move Detected

Market: Will Republicans win the Ohio Senate seat in 2026?
YES Price: 0.38 → 0.51 (+34.2% in 12 min)
Possible cause: new poll / news event
Time: 2026-03-21 09:17 UTC
```

**New market alert:**
```
KALSHI ALERT - New Market Opened

Category: Politics
Market: Will [Candidate] win the Pennsylvania Governor race in 2026?
YES Price: 0.47
Resolution: November 3, 2026

kalshi.com/markets/...
```

---

## Screen UI
![kalsh3g](https://github.com/user-attachments/assets/6475ed0b-d5c6-4c91-9eca-190bbdc61be4)


## Verified Live

**Configuration used:**
* Price alerts + sharp moves, 10-second polling, Telegram delivery

**Sharp move alert triggered:**

| | Details |
|---|---|
| Market | Will Republicans hold the House majority after 2026 midterms? |
| Move | YES 0.44 to 0.58 (+31.8%) in 9 minutes |
| Alert delivered | Telegram, 0.4 seconds after detection |

---

## Frequently Asked Questions

**What is Kalshi Alert Bot?**
Kalshi Alert Bot is a monitoring tool that watches Kalshi markets and sends you Telegram or Discord messages when price, volume, or market conditions match your configured rules. No auto-trading - alerts only.

**Do I need to give it trading permissions?**
No. The bot only needs read access to Kalshi market data. It does not place orders, so you do not need to share any order-placement API permissions.

**How fast are the alerts?**
The bot polls Kalshi every 10 seconds by default. Alert delivery via Telegram takes an additional 1-3 seconds. For most prediction market use cases, this is effectively real-time.

**Can I add a specific market to watch?**
Yes. Add a `market_title_contains` rule with a keyword from the market title and set your target price. The bot monitors it and alerts when that price is hit.

**What is a whale alert?**
A whale alert triggers when a sudden large drop in order book depth is detected for a market, suggesting a significant fill just happened. This can indicate smart money entering or exiting a position.

**Can I get a morning digest instead of real-time alerts?**
Yes. Enable `daily_summary = true` and set `daily_summary_time`. The bot sends a structured message each morning showing all tracked markets, their current prices, and 24-hour changes.

**Does it support Discord?**
Yes. Set `enabled = true` under `[discord]` and provide a webhook URL. Alerts are sent to both Telegram and Discord simultaneously if both are configured.

**Is Kalshi Alert Bot available for Windows?**
Yes. A standalone Windows x64 application is included. The Python version runs on any platform with Python 3.10+.

---

## Use Cases

- **Kalshi price alert bot** - get notified instantly when any Kalshi market crosses your target YES or NO price
- **Kalshi Telegram bot** - receive real-time Kalshi market alerts directly in your Telegram chat
- **Prediction market sharp move detector** - catch unusual price moves before the crowd reacts
- **New Kalshi market notifications** - be first to see new markets open in your categories
- **Kalshi Discord alerts** - send Kalshi price and resolution alerts to your Discord server via webhook
- **Kalshi whale tracker** - detect large fills in the order book and get alerted to smart money activity
- **Kalshi resolution notifier** - get a Telegram message the moment a tracked market resolves YES or NO

---

## Repository Structure

```
kalshi-alert-bot/
+-- kalshi-alert-bot-v.1.0.6.exe
+-- config.toml
+-- data/
|   +-- alerts/
|   +-- logs/
|   +-- dll/
+-- python/
|   +-- src/
|   |   +-- market_monitor.py
|   |   +-- alert_engine.py
|   |   +-- telegram_client.py
|   |   +-- discord_client.py
|   +-- requirements.txt
+-- README.md
```

---

## Requirements

```
python-dotenv, typer[all], httpx, websockets, kalshi-python, python-telegram-bot, devtools
```

* Kalshi account with API access (read-only)
* Telegram bot token (from @BotFather)
* Optional: Discord webhook URL

---

*Set it. Forget it. Get the alert.*
