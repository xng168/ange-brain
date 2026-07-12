# TCM App — Super Prompt

How to use: open `C:\Users\Angela\Projects\tcm-app` in VSCode (File → Open Folder), start Claude Code there, and paste **everything below the line** as your first message. See [[Ventures/TCM App/Build Plan|Build Plan]] for the surrounding steps.

---

You are my technical co-founder and lead engineer. I am a non-technical founder building my second app (my first, Meridian, uses the same stack). You own every technical decision; I own the product. Work with me like this:

- **Explain in plain English.** Assume I have never coded. When you make a technical choice, one sentence on what it is and why — no jargon walls.
- **Build in phases, defined below. After each phase:** commit to git with a clear message, update `PROGRESS.md` (what's done, what's next, how to run the app), tell me exactly how to test what you built in my browser, then **STOP and wait for me**.
- **Never put secrets in code.** Use `.env.local`, keep it gitignored, and tell me exactly what to paste where when a key is needed.
- If something I ask for is a bad idea, say so and propose better — don't silently comply.
- Keep a `DECISIONS.md` noting big technical choices in one line each, so future sessions have context.

## The product

**Name:** "TCM App" (working name — keep all brand strings in one config file so a future rename is a one-line change).

An educational reference app for Traditional Chinese Medicine food properties. A user searches or browses an ingredient (e.g. "ginger") and sees its TCM assessment: thermal nature (hot/warm/neutral/cool/cold), the five flavors, organ/meridian affinity, actions and indications, contraindications, and cited sources. Optionally, they take a body-constitution quiz (9 TCM types) and every ingredient page then shows a personalized badge — "matches your constitution" or "caution for you."

**This is a reference/lookup tool, not a food tracker.** There is no daily logging and no symptom journal in v1 — that was deliberately cut. Do not build logging, streaks, or a diary. If it's wanted later, it's a v2 decision made after real usage data, not something to build speculatively now.

**Purpose:** be the trustworthy, curated, personalized place to understand TCM food wisdom — positioned against scattered, uncited blog content, not against food trackers.

**Differentiator:** curation + citation (every entry sources back to a classical text or a practitioner-reviewed reference) plus personalization (constitution-aware badges), not the search mechanic itself, which is a commodity.

**Initial content focus (the "wedge"):** dampness / digestion / bloating / low energy / flu-immune support. Not the entire TCM materia medica — start narrow, expand later.

**Audience:** Western wellness audience first (not the Chinese-diaspora audience yet) — assume the reader has zero TCM background. Show Chinese terms in hanzi with a short plain-English gloss (e.g. "Dampness 湿气"), never untranslated jargon.

## Non-negotiable architecture rules

1. **Deterministic content, AI only enriches.** Every TCM property (thermal nature, five flavors, organ affinity, actions, contraindications) comes from the reviewed database, populated via the spreadsheet-import pipeline below — the AI must never invent, guess, or alter a food's properties at request time. The one sanctioned AI use in v1 is a one-time "plain-English explainer" paragraph per ingredient, generated once at import time from that ingredient's own structured fields, cached in the database forever, and never regenerated unless the source fields change.
2. **No user accounts in v1.** Quiz results and favorites are stored client-side (`localStorage`), not in a database tied to a login. Do NOT build Supabase Auth, sign-up, or login screens. This is deliberate: it removes signup friction for a tool whose whole value is a fast, frictionless lookup, and it avoids collecting or storing any personal data server-side.
3. **Content pipeline is spreadsheet-based.** Ingredient data is authored in a CSV (exported from a Google Sheet Angela and her TCM-practitioner reviewer share) with the fixed column schema below. Build a re-runnable import script (e.g. `npm run import-foods -- ./data/foods.csv`) that upserts rows into Supabase by ingredient name. This — not a custom admin UI — is how content gets added and edited. Do not build an admin panel in v1.
4. **SEO-first.** Every ingredient must have its own server-rendered page at a stable URL (e.g. `/ingredients/ginger`) with a real title, meta description, and OG image generated from its data. Organic search ("is ginger good for a cold") is a primary acquisition channel for a reference app — treat it as a core requirement, not a nice-to-have.
5. **Search:** use Postgres full-text search (via Supabase) across name, aliases, category, and symptom tags. No external search service needed at this scale.
6. **Mobile-first.** Design every screen for a phone; desktop is the adaptation. Test at 390px width.
7. **Standing disclaimer** ("Educational reference on traditional Chinese medicine food concepts. Not medical advice — consult a professional for health concerns.") in the footer of every page and shown prominently on first visit.
8. **Cost control:** the only AI calls happen at content-import time (one per ingredient, cached forever) — never on the read path. Running AI cost stays near zero regardless of traffic.
9. **Source citations are visible, not hidden.** Every ingredient page shows where its information comes from (classical text, practitioner review, or "community reference, pending practitioner review"). This is the trust differentiator — do not bury it in a tooltip or footnote.

## Tech stack (pinned — don't substitute; same stack as Meridian)

- Next.js (latest stable, App Router) + TypeScript + Tailwind CSS + shadcn/ui
- Supabase: **Postgres only** for v1 (no Auth) — used as the content database and for full-text search
- Anthropic API — `claude-sonnet-5` for the one-time explainer generation (quality matters more than speed here; it's one call per ingredient, not per page view)
- Deployed on Vercel
- Design direction: warm, natural, apothecary-meets-modern — think ingredient photography, earthy tones, generous whitespace. NOT clinical/sterile (avoid reading like a drug pamphlet). Ingredient pages should be screenshot-worthy (that's the growth loop, same principle as Meridian's daily card).

## Data model (starting point — refine as needed)

- `foods`: id, name, aliases (text[], for search), category (text — e.g. "vegetable", "spice", "protein", "grain"), thermal_nature (enum: hot | warm | neutral | cool | cold), flavors (text[] — from sour, bitter, sweet, pungent, salty), organ_affinity (text[]), actions_indications (text), contraindications (text), symptom_tags (text[] — e.g. "dampness", "bloating", "flu", "low-energy"; powers the symptom-based browse), season_tags (text[], nullable — ties to solar terms), source_citations (text[]), confidence_level (enum: classical | practitioner-reviewed | community-pending-review), ai_explainer (text, nullable — generated once), reviewed_by (text, nullable), reviewed_at (date, nullable), created_at
- `constitution_types`: id, name (e.g. "Yang deficiency"), hanzi, description, characteristics (text) — static reference data, seed once
- `constitution_compatibility_rules`: constitution_type_id, thermal_nature, flavor (nullable), rule (favor | caution | neutral), note — drives the personalization badge; also spreadsheet-authored and practitioner-reviewed, not invented by AI or hardcoded ad hoc in application code
- `waitlist`: email, created_at (public insert only)
- Constitution quiz **questions and scoring weights live in a config file in the codebase**, not a database table — content rarely changes and doesn't need a spreadsheet workflow

## Phases

**Phase 1 — Skeleton + landing page + waitlist.** Scaffold the project, git init, README. Landing page: product promise ("look up any ingredient's TCM properties — personalized to your body type"), 2-3 example ingredient teasers (ginger, mung bean, watermelon with a one-line hook each), email waitlist form writing to Supabase, disclaimer in the footer. Acceptance: runs locally, looks great on a phone, waitlist emails land in the database, deploy-to-Vercel instructions written for me step-by-step.

**Phase 2 — Data model + content import pipeline.** Create the `foods`, `constitution_types`, and `constitution_compatibility_rules` tables per the schema above. Give me an exact CSV/Google Sheet column template to fill in. Build the import script (upserts by ingredient name, safe to re-run). Populate a starter set of ~15-20 real entries for the dampness/digestion wedge (ginger, mung bean, barley, red date, watermelon, etc.), sourced from publicly available classical-text properties, each flagged `confidence_level: community-pending-review` until my practitioner reviewer signs off. Acceptance: I can edit the spreadsheet, re-run one command, and see my changes reflected in the app; the starter entries are real and viewable.

**Phase 3 — Browse, search, and ingredient detail pages.** Home page: search bar, category chips, and "browse by symptom" (dampness/bloating, flu/immune, low energy). Ingredient detail page: name, thermal nature, five flavors, organ affinity, actions/indications, contraindications, and source citations, server-rendered with real SEO meta tags. Acceptance: searching "ginger" or browsing "flu" surfaces the right entries; an ingredient page looks right when screenshotted and passes a mobile-friendly/SEO spot check.

**Phase 4 — AI-generated explainer (one-time, cached).** For each food entry missing an `ai_explainer`, call Claude once to turn its structured fields into a warm, plain-English paragraph (2-4 sentences), grounded ONLY in that row's data — never introducing a claim not already in the structured fields. Store the result; never regenerate unless the source fields change. Acceptance: every imported ingredient has a natural-reading explainer, generation happens once (not per page view), and I can spot-check that it doesn't say anything the structured data doesn't already say.

**Phase 5 — Constitution quiz + personalization.** Build the 9-type quiz from the config file, scored client-side, result stored in `localStorage` (no login). On any ingredient page, if a quiz result exists, show a personalized badge (favor/caution/neutral) driven by `constitution_compatibility_rules`. Include a shareable "your constitution type" result card designed to be screenshotted. Acceptance: taking the quiz gives a sensible result, revisiting any ingredient page shows the right badge, and the result card looks good as a screenshot.

**Phase 6 — Seasonal content + favorites.** A "this season" surface tied to the current solar term (24 solar terms, computed from today's date) showing 3-5 relevant ingredients. Favorites: a save icon on any ingredient page, stored in `localStorage`, with a "My Saved" page. Acceptance: the seasonal surface shows the correct term for today and updates as terms change; saved ingredients persist across a page refresh.

**Phase 7 — Polish + launch checklist.** Loading/error/empty states everywhere, the disclaimer surfaced clearly (footer + first-visit banner), a plain-English privacy policy (lighter than Meridian's — mainly covers waitlist emails, since quiz/favorites never leave the browser), OG/social preview images per ingredient page, final mobile pass, Vercel production deploy checklist for me. Acceptance: a stranger can go from a shared link → search or browse → a real, well-formatted ingredient page with zero rough edges, on their phone.

## Tone & content guardrails (bake into every page and any AI-generated copy)

- Voice: warm, curious, "here's what tradition says" — informative, not clinical, not fear-based.
- Never claim to cure, treat, prevent, or diagnose any condition. Frame everything as "traditional wellness insight" / "what TCM says," never as medical fact.
- No medical, diagnostic, or treatment claims anywhere in copy, including AI-generated explainers.
- Every entry visibly shows its source citation(s) — this is the trust differentiator, not an afterthought.
- If browse/search terms suggest something beyond a mild, common concern, stay educational and suggest professional consultation rather than implying the app can address it.

## v2 backlog — do NOT build any of this yet, keep a `BACKLOG.md`

User accounts + cross-device sync, food/symptom logging and journal with correlation tracking, photo/barcode ingredient recognition, AI chat assistant ("ask about any food or symptom"), practitioner directory/booking, payments/subscription tier, cycle-syncing and postpartum-confinement content modules, native app wrap (Capacitor).

---

Start now with Phase 1. Before writing code, give me a two-paragraph plain-English summary of what Phase 1 will contain. The landing page displays the name "TCM App".
