# Build Guide: Heritage Words v1 (working title) — Windows / No-Mac Edition

A step-by-step path from zero coding experience to a shipped iOS app, using Claude Code as your developer while you act as product owner and tester. Read this once fully before starting.

---

## How this works (the honest version)

You will not be writing code by hand. Claude Code is an AI coding agent: you describe what you want in plain English, it writes the code, you run the app and report what you see. Your real jobs are (1) deciding what to build — largely already done in the super prompt, (2) testing every change on a real screen, and (3) keeping scope discipline. Expect friction: things will break, and "describe the bug clearly, paste the error, let Claude fix it" is the loop you'll live in. Budget 2–4 months of nights and weekends.

**The no-Mac architecture in one paragraph:** iOS apps normally require a Mac. We route around that with React Native + Expo — you write the app on Windows, test it live on your own iPhone through the free Expo Go app (scan a QR code, your app appears on the phone and updates as code changes), and when it's time to ship, Expo's cloud service (EAS) builds the final iOS app on rented Macs and delivers it to Apple's TestFlight for you. Bonus: this stack makes a future Android version cheap, since it's the same code.

---

## Step 0 — What you need before anything

1. **A Windows PC** (what you have) — Linux also works.
2. **An iPhone or iPad for testing.** This is now your test device from day one, which is genuinely nicer than a simulator.
3. **A paid Claude plan.** Claude Code requires a Pro, Max, Team, Enterprise, or Console account — the free plan does not include it. Pro is the entry point; if you hit usage limits during long sessions, Max is the upgrade path.
4. **An Apple ID** (free). The **$99/year Apple Developer Program** is NOT needed yet — only at Step 8 (TestFlight). Don't pay it until then.
5. The two project files from this conversation: `CLAUDE.md` (the super prompt) and `language-pack-schema.md`.

## Step 1 — Install the tools (≈45 minutes)

1. **Install Node.js** (the runtime Expo's tooling needs): download the LTS version from nodejs.org and run the installer with default options.
2. **Install Claude Code.** Two options:
   - *Easiest for beginners:* download the **Claude Desktop app** and use the built-in Code tab — no terminal needed.
   - *Terminal route:* open PowerShell and paste: `irm https://claude.ai/install.ps1 | iex` — the native installer needs nothing else. Afterwards run `claude doctor` to confirm the install is healthy. (If `claude` isn't recognized, the installer will have shown a note about adding it to your PATH — paste that note to Claude in the Desktop app or a new PowerShell window and ask for the fix.)
3. **Sign in** when prompted (a browser window opens; log in with your Claude account).
4. **On your iPhone:** install the free **Expo Go** app from the App Store.

## Step 2 — Set up the project (≈15 minutes)

1. Make a folder for the project, e.g. `HeritageWords`, somewhere easy like Documents.
2. Put `CLAUDE.md` and `language-pack-schema.md` inside it. `CLAUDE.md` is special: Claude Code automatically reads a file with that exact name at the start of every session — it's the project's permanent memory. That's why the super prompt lives there.
3. Open Claude Code (Desktop app Code tab, or type `claude` in a terminal opened inside that folder) and point it at this folder.

## Step 3 — The first session (Milestone 0)

Type this as your first message:

> Read CLAUDE.md and language-pack-schema.md fully. Then set up Milestone M0 exactly as described: a new Expo (React Native, TypeScript) project, a git repository, and a sample language pack with 20 placeholder cards. Explain what you did in plain English, then tell me exactly how to start the development server and open the app on my iPhone with Expo Go, step by step, assuming I have never done this before.

The flow you'll be taught: Claude starts the development server, a QR code appears, you scan it with your iPhone camera, and the app opens inside Expo Go. Your PC and phone must be on the same Wi-Fi. **Success for today = you see the app's empty home screen on your own iPhone.** That's a real milestone; stop there if you're tired.

## Step 4 — The working rhythm (repeat for every milestone)

This loop is the whole build. Each session:

1. **Start:** "Let's do milestone M__. Recap what it involves before writing code."
2. Let Claude build it. It will ask permission before running commands — read what it plans to do; approve if it matches the milestone.
3. **Run the app on your iPhone** via Expo Go. Changes appear live as Claude saves code — you'll often watch the app update in your hand within seconds.
4. **Test like a bored 6-year-old:** tap everything, tap fast, tap the wrong thing, rotate the screen, close and reopen the app.
5. Report problems in plain English with exactly what you saw: "I tapped the panda card and the app showed a red error screen" beats "it's broken." Expo shows errors two places — a red screen on the phone and text in the terminal; copy-paste the terminal text to Claude, or photograph/transcribe the phone message.
6. When the milestone works, say: **"Commit this milestone to git with a clear message."** Git is your undo button — if a later session breaks things, Claude can restore the last good version. Never skip the commit.
7. One milestone per session. Resist "while we're here, let's also…" — that instinct is how solo projects die.

**When things go wrong** (they will): paste the error, describe what you expected vs. saw, and if you're going in circles say "stop, explain in plain English what you think is wrong and list three possible causes." If a session gets confused, start a fresh session — CLAUDE.md means no context is truly lost. `claude doctor` diagnoses install-level problems.

## Step 5 — The milestones (already specified in CLAUDE.md)

M0 project skeleton → M1 pack loader → M2 flashcards → M3 recognition game → M4 matching game → M5 parent-child mode → M6 parent area + progress → M7 real content swap → M8 build & compliance. Details live in the super prompt so Claude always has them. Expect M0–M2 to feel slow (everything is new), M3–M5 to speed up dramatically, and M8 to take longer than you think.

**One stack-specific rule to know exists (Claude enforces it, you just need to recognize it):** during development, the app must stay compatible with Expo Go — meaning no exotic add-ons that require custom-built versions of the testing shell. If a feature ever genuinely needs one, Claude is instructed to stop and explain the trade-off first. This keeps your daily loop simple.

## Step 6 — Content production (parallel track, start by M3)

While building, line up the content so M7 isn't blocked — this is the gate we discussed:

1. Finalise the ~292-word list in `heritage-words-content-list.xlsx` (already drafted); have your native speaker proofread it — the yellow columns are theirs.
2. Record native-speaker Mandarin audio (~292 clips) AND English audio (~292 clips — both languages are fully recorded; ~584 total). Quiet room, phone or USB mic, one word/phrase per file, filenames exactly matching the spreadsheet's audio columns.
3. Native-speaker proofread of every character, pinyin, and tone. Non-negotiable.
4. Source images for the 211 concrete words (licensed icon set in one consistent style is the budget-sane route — keep the licence file and log each source in the spreadsheet's Image Source column; the 81 abstract words correctly have no image).
5. Stroke data: not needed for v1 (tracing is v1.5), so skip for now.

## Step 7 — Real-family testing

Before strangers, test with your own or friends' kids for a week — hand them your phone with Expo Go open. Watch silently: where a child hesitates or loses interest is your bug list. Fix, commit.

## Step 8 — Cloud build + TestFlight (now pay the $99)

This is where the no-Mac magic happens:

1. Enroll in the Apple Developer Program ($99/year).
2. Create a free account with **Expo (expo.dev)** — their EAS service is the cloud that builds iOS apps for you. The free tier works but queues can be slow; a paid tier (~$19/month, cancel when done) speeds builds up during your shipping month.
3. Tell Claude: "Prepare the app for an EAS production iOS build and TestFlight submission, and walk me through the EAS and App Store Connect setup step by step." EAS handles the Apple signing certificates (the usual Mac-only pain) automatically and can upload the finished build straight to TestFlight from your Windows machine.
4. Invite 10–20 heritage families — ideally from the communities in your validation research. TestFlight lets them install pre-release builds. Collect feedback for 2–3 weeks, fix the recurring complaints only.

## Step 9 — App Store submission

1. Ask Claude to run a pre-submission compliance review against the Kids Category checklist in CLAUDE.md (parental gate, no data collection, privacy labels = "Data Not Collected", privacy policy page — Claude can draft it; host it on a free page).
2. Prepare the listing: name, screenshots (taken on your own iPhone — Claude walks you through what Apple requires), description leading with "speaks Mandarin but can't read it yet?" and the no-subscription/no-data promise.
3. Submit through App Store Connect (Apple's web dashboard — works fine from Windows). Review currently averages 24–72 hours, but kids' apps get extra scrutiny — a rejection on first attempt is common and normal; it comes with reasons, which you paste to Claude and fix.

## Budget recap

Claude paid plan (monthly) + Apple Developer $99/year (Step 8 only) + EAS ~$0–19/month (Step 8 only) + content $250–1,500 (audio, proofread, images) + $0 servers forever. Total cash for v1: roughly **$500–2,000** depending on content choices, plus your time.

## Working with outside developers (if you ever bring in help)

You are not locked into doing this alone, and the Windows/Expo path doesn't restrict who can help. The project is a standard, portable React Native + Expo codebase — plain files tracked in git — so any developer on any operating system can join it. A Mac-using developer can do everything you can *plus* run the iOS simulator and local iOS builds, so bringing in Mac help unlocks extra options rather than requiring any conversion. Nothing here needs to be rebuilt to hand it over.

If you hire help, the handoff is simple:

1. **Put the project on a private GitHub repo.** Git is already your undo button; a hosted repo is also the standard way to share code. Ask Claude to "walk me through creating a private GitHub repository and pushing this project to it" when you're ready — it's a 15-minute one-time setup.
2. **Give the developer read (or write) access to that repo.** They clone it and run the same commands you do — no other transfer needed.
3. **Share `CLAUDE.md` and `language-pack-schema.md`** — they double as onboarding docs; a good developer will understand the architecture and constraints in minutes.
4. **What they'd need their own copies of:** your Expo (EAS) account or an invite to it, and — only at ship time — access to your Apple Developer account (App Store Connect supports adding team members with limited roles, so you never hand over your full login).
5. **Keep it conventional.** The super prompt already forbids exotic, non-standard add-ons; that rule doubles as portability insurance — a boringly standard project is the easiest kind for outside help to join.

The only scenario that would need a Mac and a genuine rebuild is deliberately abandoning React Native for Apple-native Swift — an unlikely, years-away strategic choice that nothing you're doing now forces or forecloses. For any normal "I need an extra pair of hands" situation, your project is ready to hand off as-is.

## The three rules that keep this alive

1. **Never skip a git commit** after a working milestone.
2. **Never add scope mid-milestone** — write ideas in a `later.md` file instead.
3. **Run the app after every change.** If you only read Claude's description of what it built, you're not testing — the screen is the truth.