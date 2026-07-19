# Productivity Self Care Pet

A customisable **self-care pet that lives on your screen** — it roams along the edges, pops up at random times as a cute mini-distraction, and gives gentle "you've been on screen a while" nudges based on the apps *you* choose to restrict. Part focus companion, part desktop toy. The emotional hook is a personalised creature you don't want to neglect.

- **Name:** Productivity Self Care Pet — working name, created 2026-07-19. Almost certainly a placeholder (long, descriptive); real name TBD.
- **Stage:** Idea / evaluation. Not spec'd, not built.
- **Objective:** Gentle, non-punitive screen-time awareness through an emotional companion, not a blocker or a nag.
- **Genesis:** Started as "Tamagotchi × productivity / Finch-style self-care pet that reminds you when you overuse social media." First-pass review found that space over-crowded (see Competitors). Angela then refined it (2026-07-19) toward the distinctive part: **a roaming on-screen companion + generic reminders**, deliberately *not* needing to know which app you're on.

## The refined concept (what makes it different)

The pivot that matters: this is **not** primarily a screen-time *blocker*. It's a **roaming screen pet** that happens to nudge.

- The pet is drawn **on top of** whatever you're doing — walks along the screen edges, pops in at random, cute idle animations. It's a persistent companion, visible while you use other apps.
- Reminders are **generic** ("you've been scrolling a while — come play with me?"), triggered by a threshold on a user-chosen set of restricted apps. It deliberately does **not** identify or call out the specific app. This sidesteps the whole iOS privacy wall (you don't need to know it's TikTok) and simplifies the build.
- The **moat is emotional + aesthetic**, not technical: a customisable, personality-driven creature you form an attachment to. Same reason Finch works — but delivered as an ambient screen buddy rather than an app you have to open.

## Distinctiveness verdict

**More distinctive than the original pitch — yes.** The reframe moves it out of the crowded "self-care app / app-blocker" categories and into the **desktop-pet / roaming-companion** genre, then fuses that with self-care positioning. That fusion is genuinely un-owned:

- The roaming-overlay-pet genre is **proven but unpolished** — Shimeji, Desktop Goose, eSheep, Neko, Messenger chat-heads. These are mostly free novelty/hobby toys. **None** are positioned as a branded, customisable, monetisable *self-care* product with intentional screen-time nudging.
- Finch is a contained app you open; blockers (one sec, Opal) are invisible until they interrupt. **Nobody offers an always-present pet that reacts to your screen use.** That ambient-companion angle is the wedge.
- Distribution fit is strong: roaming pets are extremely screenshot/share/TikTok-friendly (Desktop Goose went viral on exactly Angela's channels). See [[Content/index|Content]].

Caveat: distinctiveness is in *positioning + art + brand*, not defensible tech. Anyone can build a sprite that walks the screen. The defensibility has to come from character design, personality, brand, and Angela's audience — not code.

## Feasibility — the platform picture FLIPS here

The whole product hinges on one capability: **can an app draw a character on top of / roaming over other apps?** The answer is entirely platform-dependent, and it reverses the earlier "iOS-first" instinct.

- **Windows / macOS desktop — YES, easiest.** This is the classic desktop-pet pattern: a transparent, frameless, always-on-top, click-through window. Electron or Tauri do this well. Desktop Goose / Shimeji prove it works and can go viral. **This is the strongest home for the exact vision — and it matches Angela's original "laptop device" instinct.**
- **Android — YES.** The `SYSTEM_ALERT_WINDOW` ("draw over other apps") overlay permission is exactly the Messenger chat-heads mechanism — a floating view over everything. Pair with `UsageStatsManager` (which, unlike iOS, *can* see specific app usage) + a foreground service for the nudge triggers. Doable; fiddlier (battery, background limits, one-time permission friction).
- **iOS — NO. Hard wall.** iOS does **not** let third-party apps draw over other apps or roam the home screen. There is no floating-window API. Best available: notifications, Live Activities (Dynamic Island / lock screen — fixed templates, not a free-roaming pet), home-screen widgets (static), and the Screen Time shield screen (only appears *when you open a blocked app*). **The hero mechanic is impossible on iOS as described.** (This reverses the earlier blocker-concept advice to go iOS-first — because the mechanic changed, not the reasoning.)

**Difficulty:**
- Desktop MVP: **low-to-moderate.** The window/overlay plumbing is well-trodden; a charming MVP is a weeks-not-months job for a capable build. The real work — sprite animation, edge-pathing, personality, customisation — is **art and design**, which is Angela's strength.
- Android: **moderate** (overlay + foreground service + usage stats + battery/permission UX).
- iOS: **not feasible** for the hero mechanic; would need a fundamentally degraded redesign (widgets / Live Activities / notifications only).

**Stack mismatch to flag:** Angela's current momentum is Expo / React Native (the [[Ventures/Mandarin Kids App/index|Mandarin Kids App]]). The *strongest* version of this idea is a **desktop app (Electron / Tauri)** — a different stack that doesn't reuse that work. Android overlay via RN is possible but not RN's strength. So "build this next" ≠ "reuse what I just learned."

## Competitor research

- **[[#Genesis|Finch]]** — self-care pet, goal/habit driven, 500k+ reviews, huge on TikTok. The incumbent for "self-care pet + productivity," but a contained app, no ambient/roaming presence, no real-time screen-time reaction.
- **one sec / Opal / Forest / ScreenZen / Clearspace** — screen-time nudge/block apps. No emotional pet companion; invisible until they interrupt.
- **Desktop Goose / Shimeji / eSheep / Neko** — the actual roaming-pet genre this competes in on desktop. Proven appeal, viral potential — but free novelty toys, not self-care-positioned, not customisable-as-a-product, not monetised. **This is the gap.**
- **Messenger chat-heads** — the mobile-overlay pattern (proof the Android mechanic works), not a product competitor.

## Open questions

- **Platform decision** is the first fork: **Desktop (best fit for the vision, matches the "laptop" instinct) vs Android (mobile reach, more friction) vs both.** iOS is out for the hero mechanic — accept that up front.
- Is this the best use of build time **right now**, given [[Ventures/Mandarin Kids App/index|Mandarin Kids App]] is mid-build and the strongest platform here needs a *new* stack (Electron/Tauri)? Or park it as a spec'd "next" venture?
- What's the monetisation model — one-time purchase (fits the desktop-toy/novelty audience and Angela's no-subscription lean elsewhere), cosmetic/pet packs, or freemium?
- Real name + brand (the moat is brand + art, so this matters more here than for a utility app).

## Honest summary

The refinement is a real improvement: **more distinctive and more buildable** — *if* Angela accepts desktop and/or Android and drops iOS for the roaming mechanic. The opportunity is modest but real (proven genre + no polished self-care-branded product owns it + a creator audience that's a perfect distribution match). The risks are (1) low technical defensibility — it lives or dies on art, personality, and marketing, and (2) it's yet another app idea competing for build time against ventures already in flight.

Related: [[Ventures/index|Ventures]] · [[Content/index|Content]] (build-in-public / distribution) · [[Open Items]]
