# Telegram Bridge: Laptop vs. VPS

## Current setup
The Telegram bridge (`_sources/telegram_bridge.py`) runs as a hidden background process, started automatically via a shortcut in the Windows Startup folder (`_sources/telegram_bridge_watchdog.vbs`), which relaunches it automatically if it ever crashes.

**This only works while this laptop is turned on and logged in.** If the laptop is off, asleep, or shut down, the bridge stops — messages sent to the bot while it's down won't be picked up until the laptop is back on and logged in again (Telegram queues them; they'll be processed once the bridge restarts).

## Why laptop-first
- Zero extra cost — no hosting bill
- Simple to set up and debug directly
- Fine for a single person capturing ideas casually throughout the day, as long as the laptop is generally on/available

## When to move to a VPS
The laptop-only setup becomes a real limitation once:
- Angela wants to capture ideas reliably even when the laptop is off/traveling without it
- The bridge needs to be "always on" for consistency (e.g. relying on it daily and getting annoyed by missed captures)
- Other automations depend on this bridge running 24/7

**Signal to act on:** if missed captures because the laptop was off becomes a recurring annoyance, that's the cue to move the bridge (and possibly sync.ps1) to a small always-on VPS (e.g. a $5-6/mo box). At that point the bot token and vault repo access need to move with it — same secrets.env pattern, just hosted elsewhere.

Related: [[Daily Stack]], [[Open Items]]
