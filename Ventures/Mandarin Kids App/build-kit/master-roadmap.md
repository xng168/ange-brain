# Heritage Words — Master Roadmap: Build to Launch

The single ordered plan from today to a live App Store app. It orchestrates two tracks that run **in parallel** — the **Build track** (the app) and the **Content track** (words, audio, images) — and shows where they converge. Work the phases in order; within a phase, the build and content steps happen side by side.

**Your other documents (this plan points to them, doesn't repeat them):**
- `CLAUDE.md` — the super prompt that drives Claude Code (the build's brain).
- `language-pack-schema.md` — the data format all content follows.
- `build-guide.md` — how to actually operate Claude Code day to day (the no-Mac / Windows path).
- `heritage-words-content-list.xlsx` — the 292-word content list + audio/image/licence tracker.

**Honest framing before you start:** demand is not yet proven (Phase 1 fixes that), the content work takes real calendar time so it starts early, and your first App Store submission may be rejected with reasons — that's normal, not failure. Budget 3–5 months of nights and weekends end to end. Total cash roughly $500–2,000.

---

## PHASE 0 — Decide it's worth building (1–2 weeks, ~$50)

Goal: confirm real parents want this *before* investing months.

- [ ] Build a simple landing page (one page: the "speaks Mandarin but can't read it yet?" hook, the grandma-message promise, the no-subscription/no-data pledge, an email signup). Claude can generate this for you.
- [ ] Post where these parents gather: multilingual-parenting subreddit, The Bilingual Zoo forum, heritage-language Facebook/WeChat parent groups. Don't pitch — ask about the "speaks but can't read" experience, share the page where allowed.
- [ ] Talk to 10 parents. Key questions: what have you tried and abandoned? what would success look like this year? would you pay ~$20 once? Listen hardest for abandonment stories.
- [ ] Optional paper test: print 20 cards, watch a real kid use them.
- **Go / no-go:** ~100 genuine signups, or 5 of 10 parents saying "I'd pay today" → proceed. Polite interest but no signups → the pain may be real but this shape is wrong; revisit before building.

---

## PHASE 1 — Set up tools + lock the content spec (1 week)

Goal: everything installed, and the content list finalised so recording can begin.

**Build track:**
- [ ] Get a paid Claude plan (Pro minimum — Claude Code needs it).
- [ ] Install Node.js (LTS) from nodejs.org.
- [ ] Install Claude Code (Desktop app Code tab is easiest; or `irm https://claude.ai/install.ps1 | iex` in PowerShell). Run `claude doctor` to confirm.
- [ ] Install Expo Go (free) on your iPhone/iPad.
- [ ] Make a project folder; put `CLAUDE.md` and `language-pack-schema.md` inside it.

**Content track (start now, runs for weeks):**
- [ ] Finalise the ~292-word list in the spreadsheet — adjust any words you want.
- [ ] **Native-speaker proofread (REQUIRED GATE).** A fluent Mandarin speaker checks every character, pinyin, tone, and English meaning in the two yellow columns. Pay special attention to tone sandhi (不/一, 3rd-tone pairs) and neutral tones. **Nothing gets recorded until this is done** — re-recording is the expensive mistake.
- [ ] Confirm the three locked decisions are reflected: simplified pack only for v1 (traditional is a separate future pack), one audio file per phrase, image field per word.

---

## PHASE 2 — Build the foundation: M0–M2 (expect this to feel slow — everything is new)

Goal: a running app that displays real flashcards from the data pack. Operate using the loop in `build-guide.md`: one milestone per session, run the app on your phone after every change, commit to git when it works.

**Build track:**
- [ ] **M0 — Skeleton.** Expo project, git repo, sample pack of ~20 placeholder cards, app launches to a home screen on your iPhone. Creates `content-todo.md` and `later.md`. *Success = empty home screen on your phone.*
- [ ] **M1 — Pack engine.** The loader that reads/validates the pack and exposes cards, levels, categories. The foundation everything else stands on — build carefully.
- [ ] **M2 — Flashcards.** Browse cards, filter by level/category, flip, play both audios, toggle learning direction.

**Content track (in parallel):**
- [ ] Line up your Mandarin voice recorder (native speaker) and English voice recorder. One bilingual person can do both; a warm human voice matters more for the heritage side.
- [ ] Decide image source (see Phase 3 checklist) and start a trial of one licensed icon set.

---

## PHASE 3 — Build the activities: M3–M6 (this speeds up a lot)

Goal: all v1 activities working on placeholder content.

**Build track:**
- [ ] **M3 — Recognition game.** Hear a word → tap the right character. Gentle feedback, feeds progress.
- [ ] **M4 — Matching game.** Memory-style pairing, using cards that have images.
- [ ] **M5 — Parent-child mode.** Two-player co-op on one device. (Claude proposes 2–3 designs first.)
- [ ] **M6 — Parent area + progress.** Parental gate, per-word progress (solid/shaky/unseen), weekly off-screen suggestion, settings.

**Content track — produce the real assets (this is the gate; finish during this phase):**
- [ ] Record Mandarin audio: ~292 clips, quiet room, one word/phrase per file, filenames matching the `audio/zh/…` column exactly.
- [ ] Record English audio: ~292 clips, matching the `audio/en/…` column. (~584 clips total across both.)
- [ ] Source images for the **211 concrete words**: one consistent visual style, commercial-use licence, child-appropriate, instantly recognisable. Recommended: a single licensed children's icon set. Leave the 81 abstract words image-free.
- [ ] **Log every image's source + licence** in the spreadsheet's yellow column, and save licence documentation in your project folder as proof.
- [ ] Native-speaker listens back to a sample of recordings for tone accuracy.

---

## PHASE 4 — Bring it together: M7 (integration)

Goal: the app runs on the real 292-word pack, not placeholders.

- [ ] **M7 — Real content swap.** Replace placeholder pack with the finalised pack: real audio (both languages), real images, correct pinyin. Verify every card loads, every clip plays, abstract cards show no broken image. Empty `content-todo.md`.
- [ ] Full walkthrough yourself on your phone — every level, every category, every activity.

---

## PHASE 5 — Polish + compliance: M8

Goal: the app is store-ready and legally clean for the Kids Category.

- [ ] **M8 — Ship polish.** App icon, launch screen, accessibility pass (VoiceOver labels, larger text), performance check on an older device.
- [ ] **Kids-Category compliance review** against `CLAUDE.md` hard constraints: parental gate in front of settings/links; no ads; no third-party analytics or trackers; no accounts; no data collection.
- [ ] **Privacy policy** — required by Apple even when you collect nothing. Have Claude draft a plain "this app collects no data" policy; host it on a free public page (you'll need the URL for the store listing).
- [ ] Decide pricing (one-time purchase, ~$15–25) and confirm no subscription code exists.
- [ ] Pick the app name; do a quick search to check it isn't obviously taken/trademarked.

---

## PHASE 6 — Beta test on real families (2–3 weeks)

Goal: catch real problems before the public does. You have **two beta routes** — you can use either or both.

**Route A — PWA beta (faster, cheaper, recommended for early/wider testing).** Because every V1 feature works as a PWA (V1 was deliberately kept free of native-only features), you can ship the app as a web link. Advantages: share by URL instantly, **no $99 Apple account needed yet**, no App Store review delay, works on Android and desktop too (wider tester pool), and you push fixes instantly. Trade-offs on iOS: testers must tap "Add to Home Screen" manually, and a non-installed PWA's data can be evicted after ~7 days — so tell parents to install it to the home screen. **Test one thing hard before relying on this: offline audio playback and saved progress after the app's been closed for a few days on a real iPhone** — that's where iOS PWAs are weakest and where your app leans.
- [ ] Ask Claude: "Produce a PWA/web build of the app with Expo for web, set up offline asset caching in IndexedDB, request persistent storage, and give me a shareable URL + an 'Add to Home Screen' prompt for iOS."
- [ ] Share the link with early testers (including Phase 0 families); collect feedback; fix and redeploy instantly.

**Route B — TestFlight beta (closest to the real store experience).** Use this when you want feedback on the actual native app as users will finally get it, or before the paid launch.
- [ ] Quick pre-beta test: hand your own/friends' kids the phone (Expo Go), watch silently, note every hesitation. Fix, commit.
- [ ] **Enrol in the Apple Developer Program ($99/year)** — needed from here on.
- [ ] Create an Expo (expo.dev) account for EAS cloud builds. (Free tier works; ~$19/mo speeds up builds during your shipping month — cancel after.)
- [ ] Ask Claude: "Prepare an EAS production iOS build and TestFlight submission, and walk me through EAS + App Store Connect step by step." EAS handles Apple's signing certificates for you from Windows.
- [ ] Invite 10–20 heritage families via TestFlight. Collect feedback 2–3 weeks. Fix only the recurring issues — resist rebuilding everything.

**Recommended:** run the **PWA beta first** (Route A) to validate the experience early and cheaply with more families, then a short **TestFlight beta** (Route B) right before launch to check the real native build. The paid v1 launch (Phase 7) is still the App Store native app — a PWA can't do App Store one-time-purchase billing.

---

## PHASE 7 — Launch on the App Store (submission + review)

Goal: live in the store.

- [ ] Ask Claude for a pre-submission compliance re-check against the Kids-Category checklist.
- [ ] Prepare the App Store listing: name, subtitle, description (lead with "speaks Mandarin but can't read it yet?" and the no-subscription/no-data promise), keywords, privacy-policy URL.
- [ ] Set the App Store privacy label to **"Data Not Collected."**
- [ ] Complete the age-rating questionnaire in App Store Connect.
- [ ] Capture screenshots on your iPhone (Claude tells you which sizes Apple requires).
- [ ] Submit for review. Review currently averages 24–72 hours; kids' apps get extra scrutiny. **A first-attempt rejection is common and comes with specific reasons — paste them to Claude, fix, resubmit.** Not a setback, just the process.
- [ ] Approved → set release. You're live.

---

## PHASE 8 — After launch (ongoing)

- [ ] Watch reviews for real pain points (and for the billing/trust praise your no-subscription pledge should earn).
- [ ] Fix bugs in small, committed increments; ship updates via the same EAS → App Store flow.
- [ ] Your `later.md` is now the roadmap. Post-v1 features (more games, printable worksheets, tracing, traditional-character pack, more languages) get built under the "Future features" rules in `CLAUDE.md` — one at a time, v1 stability first.
- [ ] Each new language pack is data, not code — the payoff of the architecture. Guard that.

---

## The whole thing at a glance

| Phase | What | Rough time | Cash |
|---|---|---|---|
| 0 | Validate demand | 1–2 wk | ~$50 |
| 1 | Tools + lock content, **proofread gate** | 1 wk | Claude plan |
| 2 | Build M0–M2 (foundation) | 3–5 wk | — |
| 3 | Build M3–M6 + **produce audio & images** | 4–6 wk | $250–1,500 content |
| 4 | M7 integration | 1 wk | — |
| 5 | M8 polish + compliance + privacy policy | 2–3 wk | — |
| 6 | Beta: PWA (free) and/or TestFlight | 2–3 wk | $0 PWA / $99 Apple + ~$0–19 EAS |
| 7 | App Store launch | 1–2 wk (+ review) | — |
| 8 | Post-launch / roadmap | ongoing | — |

## Three rules that keep the whole thing alive (from the build guide)
1. **Never skip a git commit** after a working milestone.
2. **Never add scope mid-milestone** — ideas go in `later.md`.
3. **Run the app after every change** — the screen is the truth, not the description of what was built.

## The dependencies that most often trip people up
- The **native-speaker proofread must finish before audio recording starts.**
- **Audio and images must be done by M7**, so they start back in Phase 2–3, not at the end.
- **Don't pay Apple's $99 until Phase 6** — everything before it works without a developer account.
- **Privacy policy + "Data Not Collected" label are required even though you collect nothing** — easy to forget, blocks submission.
