# TCM App

*(working name — rename once the venture has a real name, same as [[Ventures/Meridian/index|Meridian]] did)*

Educational TCM ingredient repository app — search or browse an ingredient to see its Traditional Chinese Medicine assessment (thermal nature, five flavors, organ affinity, symptom relevance), personalized against your TCM body constitution. Tracking/logging is a possible future layer, added only if user demand shows up — it is not the initial focus.

- **Stage:** Building — Phase 1 done (2026-07-13). Project scaffolded at `C:\Users\Angela\Projects\tcm-app` (Next.js/TypeScript/Tailwind/shadcn), landing page + waitlist form (Supabase-backed) built, tested locally, and committed to git. Not yet deployed — needs a Supabase project created and connected (see Tasks). **Pivoted 2026-07-12** from a MyFitnessPal-style food tracker to an educational ingredient lookup/repository, with personalization (not tracking) as the differentiator.
- **Model:** TBD, and genuinely open — a reference/lookup tool doesn't support a subscription as naturally as a tracker does (see Open gaps below). Needs its own pricing thesis, not a carryover of the tracker-era subscription assumption.
- **Origin:** Angela's own idea, explored 2026-07-12

## Concept
- Search or browse any ingredient → see its TCM assessment: thermal nature (hot/warm/neutral/cool/cold), five flavors, organ/meridian affinity, actions/indications, contraindications, source citations
- Optional constitution quiz (9 TCM types) personalizes the assessment — same ingredient can show "matches your constitution" or "caution for you" depending on who's looking
- Symptom/goal-based browse (e.g. "flu," "bloating," "low energy") surfaces relevant ingredients — this is where the dampness/gut-health wedge lives
- Positioning thread: "ancient wisdom meets modern reference" — same narrative lane as Meridian
- Tracking/logging over time is an explicit **future** layer, added only if usage shows people want to log rather than just look things up (Angela's decision, 2026-07-12)

## Positioning

The gap isn't "no one has TCM food content" — plenty of blogs and clinic sites (TCM Food Therapy, Qi Health, various practitioner pages) already publish hot/cold food charts. The gap is that none of it is **curated to one consistent, trustworthy standard, searchable in one place, or personalized to the person looking it up.** That's the actual product: not the search mechanic (a commodity), but the curation/trust layer (practitioner-reviewed, cited sources) plus the personalization layer (constitution-aware results). Lead wedge is **dampness/gut-health/bloating** — it maps TCM vocabulary almost 1:1 onto an already-massive, already-trending Western wellness conversation (digestive health market $60.4B→$124.9B by 2034), with the lowest regulatory/credibility risk of the candidate wedges. Audience: Western wellness first, broaden to diaspora/general TCM audience later.

**Product ladder:** free ingredient lookup (acquisition, matches search intent from TikTok content) → personalized recommendations via the constitution quiz (retention/differentiation) → tracking/journal as a deeper layer *later, only if demand emerges* (not assumed up front). Same "ancient wisdom meets modern app" narrative lane as [[Ventures/Meridian/index|Meridian]], and can reuse the Ange.beee distribution channel the way Meridian does — each TikTok video previews one database entry, so the content-to-product mapping is direct.

## MVP scope (v1) — draft, not yet finalized into a Super Prompt

Scoped to the dampness/gut-health wedge, not all of TCM nutrition:

1. Searchable ingredient/food database — search by name or browse by category; each entry shows thermal nature, five flavors, organ/meridian affinity, actions/indications, contraindications, and source citation(s)
2. Symptom/goal-based browse — "flu," "bloating," "low energy," etc. surface relevant ingredients, scoped first to dampness/digestion, immune/flu, and low energy
3. Constitution quiz (9 TCM types), optional at onboarding — once taken, ingredient entries show a personalized "for you" badge
4. Seasonal content tied to the 24 solar terms (二十四节气) — browse/discovery hook, since a pure search tool has no natural return-visit trigger otherwise
5. Save/favorite ingredients — lightweight list, not a log

**Deliberately cut from v1 (backlog, see Feature ideas below):** daily food logging, symptom journal/correlation tracking, photo/barcode scanning, practitioner directory, cycle-syncing module, postpartum confinement program, AI chat assistant. Tracking/personalization-over-time is explicitly a "build later if demand shows up" item, not a deferred v1 feature that's already been committed to.

## Market research (2026-07-12)

**Opportunity:**
- Personalized nutrition market ~$18-20B (2025-26); diet/nutrition apps growing ~16.6% CAGR through 2035
- Ayurveda diet apps (closest working analogue) growing ~12.7% CAGR — proves "traditional medicine + personalized food app" is a fundable category in the West
- Clinical evidence exists: an RCT found a TCM-constitution-based mHealth app improved HbA1c/BMI vs. control in prediabetes ([PMC10337399](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10337399/)) — real credibility asset most wellness apps don't have

**Competitors:**
- Direct TCM tools (TCM Food Therapy, Qi Health, Dipara, various practitioner quiz sites) — static content/lead-gen, inconsistent quality, no personalization
- Ayurveda apps (AyuRythm, Prana, Dosha Diet, Doshify) — proven business model for "traditional medicine + personalized app," no TCM equivalent at this polish
- Mainstream trackers (MyFitnessPal, Cronometer, Yuka) — no traditional-medicine lens at all
- Boohee 薄荷健康 (dominant Chinese tracker, 100M+ users, 17 years) — calorie-first, not TCM-property-first, even in the most TCM-literate market

**Whitespace:** no single, curated, personalized destination for TCM ingredient information — existing content is scattered across blogs/clinic sites of inconsistent quality with zero personalization. The edge has to be curation/trust (practitioner-reviewed, cited) plus personalization (constitution-aware), since the underlying search mechanic itself is a commodity anyone could copy.

**Risks:** health-claim language risks App Store/regulatory scrutiny (frame as "traditional wellness insight," not medical advice); TCM food-property data isn't standardized across sources; audience split between diaspora users (want accuracy) and Western wellness audience (want quick/vibes content); as a reference tool, monetization is less obvious than a tracker's subscription model (see Open gaps).

**Target audience decision (2026-07-12):** Western wellness audience first, broaden to diaspora/general TCM audience later. Validating via a TikTok content test first — see [[Content/Ideas/TCM food properties series]] and the black-sesame-video edit task in [[Open Items]].

## Candidate niche wedges (2026-07-12 research)

Ranked by fit with the Western-wellness-first audience decision and current trend strength:

1. **Dampness / gut health / bloating** (strongest fit) — digestive health products market is $60.4B (2025) → projected $124.9B by 2034; 37% of Americans now seek digestive-health benefits from diet (up from 30% in 2022); gut-health product launches up 61% 2024→2025. TCM's "dampness" (湿气) framework already maps onto this conversation almost 1:1, and TCM-flavored dampness/bloating content is already circulating organically on TikTok (gua sha for digestion, "how to clear dampness"). Best overlap of TCM authenticity × an already-massive, already-trending Western wellness category, and it stays food-first rather than sliding into diagnostic territory.
2. **Cycle syncing / hormone-aware eating** — huge existing conversation (#cyclesyncing has 285M+ TikTok views, search volume for "cycle syncing diet" doubled since 2022) but currently low-credibility: most creators cite no sources or credentials, and outlets (Time, peer-reviewed articles) are actively calling parts of it unsubstantiated. TCM has a genuine, citable food-therapy tradition here (warming foods around menstruation, classical tonics like 四物汤). Real opportunity to be the "credible, source-cited" entrant into a trend currently starved of one — but needs careful framing (cite classical/practitioner sources, avoid overclaiming efficacy) given the scrutiny the category is already under.
3. **Postpartum confinement (坐月子 / zuo yue zi)** — narrower, shorter-lifecycle audience (pregnant/postpartum, ~30-40 day window per user) but proven crossover appeal and willingness to pay: a Western mom's 30-day Chinese confinement vlog went viral (2.9M views, largely Western audience praise), and confinement retreat centers (Boram NYC, Village SF) are already selling this to non-diaspora customers. High-intent, high-conversion, but works better as a specific content pillar inside the app than as the sole wedge.
4. **Qi/Yang deficiency, cold hands & feet, fatigue** — real interest exists (TikTok "adrenal fatigue" discovery content) but overlaps with "adrenal fatigue," a concept conventional-medicine sources actively flag as contested/harmful-trend territory. More reputational risk, weaker signal than the above three — deprioritize as a lead wedge.

**Working recommendation:** lead with dampness/gut health/bloating as the MVP wedge (biggest market, cleanest TCM-to-Western-trend mapping, lowest regulatory/credibility risk), with cycle syncing as a strong second content pillar once the credibility positioning is dialed in, and postpartum confinement as a later content pillar rather than the initial focus.

## Feature ideas (2026-07-12 brainstorm)

**Core loop (v1 — the lookup/repository experience):**
- Symptom/goal-based browse — "what to eat when..." for flu, bloating, low energy, cramps, insomnia, etc. (directly maps to the content test)
- Constitution quiz (9 TCM types) — personalizes ingredient assessments from day one, same pattern Ayurveda apps use for dosha
- Seasonal tips tied to the 24 solar terms (二十四节气) — discovery/return-visit hook for a search-first app

**Future — add only if usage shows demand (not committed to v1 or v2 by default):**
- Food logging + symptom journal with trend tracking — the original tracker concept; revisit only once the lookup tool has traction and users are asking for a way to log
- Food pairing/combination cautions — TCM-specific "don't combine X with Y" guidance
- Photo/barcode scan → TCM property breakdown (Yuka-style) — bigger build lift (needs food recognition + packaged food data)

**Growth/retention:**
- Shareable constitution quiz results — viral, TikTok-native, same mechanic as MBTI/astrology quiz shares; plugs straight into the Ange.beee distribution channel
- AI chat assistant for "ask about any food or symptom" — cheap to build via LLM + curated dataset (RAG), rides the "40% of nutrition apps will have an AI coach by end of 2026" trend from the market research
- Therapeutic recipes (congee, herbal soups) tied to symptom/season/constitution — retention driver, can layer on top of the lookup database without needing logging

**Possible monetization (needs its own thesis — see Open gaps):**
- Ads or a one-time "pro" unlock (deeper content, offline access, ad-free) — more typical for reference/lookup apps than subscription
- Licensed TCM practitioner directory/telehealth booking (affiliate or booking-fee revenue) — also doubles as the human review layer already planned for data accuracy
- Affiliate links on recommended ingredients/teas
- Dual "simplified" vs. "traditional depth" content modes — lets the app serve the Western-first audience now without foreclosing the diaspora audience later

## Data sourcing strategy (2026-07-12)

Even more central now than under the tracker concept — the database *is* the product.

- **Primary/classical texts:** 本草纲目 *Compendium of Materia Medica* (Li Shizhen, Ming dynasty) — full text public domain/CC BY-SA 4.0 at [Chinese Text Project](https://ctext.org/datawiki.pl?if=en&res=588089&remap=gb); 黄帝内经 *Huangdi Neijing* for foundational theory. These are the ur-sources almost every modern hot/cold food chart traces back to.
- **Modern secondary reference:** Paul Pitchford's *Healing with Whole Foods: Asian Traditions and Modern Nutrition* — the standard English-language reference used by acupuncture schools for food thermal nature; used as a structural model, not scraped wholesale (copyright).
- **Academic pharmacology databases** (herb-level compound/target data — useful for cross-checking an herb's traditional attributions, not consumer-ready food charts out of the box): TCMSP, ETCM, TCMID, BATMAN-TCM, HERB, SymMap.
- **Statistical bridge method:** a peer-reviewed study correlating nutrient composition (water content, potassium/sodium ratio, etc.) with TCM hot/cold classification ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2666154320300247)) — usable to infer properties for foods missing from classical texts (avocado, quinoa, protein powder, packaged foods).
- **Human review layer:** licensed TCM/Chinese medicine practitioner sign-off before publishing any entry — legitimacy, liability protection, and a marketing asset ("reviewed by licensed practitioners").
- **Proposed schema per food entry:** thermal nature, five flavors, organ/meridian affinity, actions/indications, contraindications, source citation(s), confidence/consensus level (since classical and clinic sources sometimes disagree).

## Open gaps before this becomes a Super Prompt (2026-07-12)

- **Differentiation vs. free web content is now the central risk.** Blogs and clinic sites already publish hot/cold food charts for free. The app has to win on curation/trust (practitioner-reviewed, cited) and personalization (constitution-aware results) — if it can't clearly beat "just Google it," there's no product.
- **Monetization needs its own thesis.** A reference/lookup tool doesn't support subscription as naturally as a tracker does — ads, a one-time "pro" unlock, or affiliate revenue are more typical for this category. Don't carry over the tracker-era subscription assumption without re-testing it.
- **AI boundary rule (non-negotiable, mirrors Meridian's rule 1):** the reviewed food database is the only source of truth for TCM properties. The AI (if/when a chat feature is added) explains and personalizes; it never asserts a property that isn't in the database.
- **Retention strategy changes shape.** No daily logging habit to hook into anymore — retention now depends on content freshness (new ingredients, seasonal tips), search/browse quality, and organic search traffic (SEO/ASO), not push-notification-driven streaks.
- **Legal/regulatory still needs real attention**, though lighter than the tracker version since there's no personal health journal in v1: proper privacy policy, actual legal review of TCM disclaimer language, entity decision before launch.
- **Bring the practitioner in earlier.** An early advisor (not just pre-launch QA) speeds up data compilation and gives "developed with a licensed TCM practitioner" as a credibility line from the first TikTok post.
- **Distribution plan beyond organic TikTok:** fine for validation, but eventual launch needs an ASO pass — search-intent content (e.g. "is ginger good for flu") is arguably a stronger organic/ASO fit for a lookup tool than it would be for a tracker.
- **No success metric defined yet for the content test:** decide before posting — save rate and comment sentiment are the leading indicators, not follower count.
- **Tracking/personalization-over-time is parked, not cancelled.** If usage data later shows people want to log symptoms/food over time, revisit the original tracker concept (and its own open gaps: symptom-correlation risk, push-notification retention, health-data privacy bar) as a v2+ layer — don't build it speculatively before then.

## Revenue ideas & cost forecast (2026-07-12)

**Revenue ideas, ranked:**
1. Freemium content depth — free basic thermal-nature lookup, one-time "Pro" unlock for full detail (five flavors, organ affinity, contraindications, recipes, personalized digest). Fits a reference app better than recurring subscription.
2. **Cross-venture synergy** — if [[Ventures/Supplement Brand/index|Supplement Brand]] or [[Ventures/Beauty Brand/index|Beauty Brand]] end up selling anything TCM-adjacent (herbs, teas), the app becomes a native distribution channel for Angela's own commerce instead of losing margin to third-party affiliates.
3. B2B licensing of the practitioner-verified database to other apps/wearables/recipe platforms once it's mature — high-margin, doesn't depend on consumer scale.
4. Practitioner directory/booking commission — doubles as the human review relationship already planned.
5. Sponsored ingredient features — needs clear "sponsored" labeling or it undercuts the trust positioning.
- **Deprioritized: banner/display ads** — cheapens the "curated trust" brand the whole positioning depends on.

**Cost forecast:**
- One-time to reach a validated MVP: roughly **AUD $600–$5,000**, dominated by the practitioner review fee (~15-30 hrs reviewing ~150-300 MVP entries; clinic-employee TCM practitioner pay is ~AUD $35-40/hr but freelance consulting review work is more realistically $80-150/hr — get real quotes, don't anchor on the low end). Everything else (books, domain, design assets) is under a few hundred dollars combined; the AI-assisted build itself is already covered by the existing Claude subscription.
- Recurring, early stage: **under $50/month** — Vercel free Hobby tier is free but its terms bar commercial/revenue-generating use, so budget Pro ($20/mo) once live; Supabase free tier covers up to 50,000 MAUs (likely enough well past MVP, $25/mo on Pro if exceeded); AI API cost is ~$0 if personalization stays rule-based (constitution × ingredient tags) rather than an LLM call per lookup — same deterministic-data principle as Meridian. App store fees (Apple $99/yr, Google Play $25 one-time) deferred if web-first.
- Also budget for later, not at MVP: trademark registration for the real brand name (a few hundred to ~$1,000+ AUD via IP Australia), and whether professional indemnity/business insurance is warranted once publishing health-adjacent content commercially.
- **Bottom line:** infra is cheap enough that profitability isn't gated on scale — a handful of paying users covers hosting. The real cost and bottleneck is the practitioner's time to get the data right.

## Documents

- [[Ventures/TCM App/Build Plan|Build Plan]] — Angela's step-by-step, no coding experience assumed (2026-07-13)
- [[Ventures/TCM App/Super Prompt|Super Prompt]] — paste into a fresh Claude Code session in `C:\Users\Angela\Projects\tcm-app` to build (2026-07-13)

**Key build decisions locked in:** same stack as Meridian (Next.js/Supabase/Vercel/Claude API) for consistency and reused accounts; **no user accounts in v1** (constitution quiz result + favorites stored in the browser via localStorage — removes signup friction and personal-data exposure); **content authored in a spreadsheet** and imported via a script rather than a custom admin UI; **SEO-first** architecture since organic search is a real acquisition channel for a reference tool; AI used only for a one-time, cached per-ingredient "explainer" paragraph generated at import time — never a live call on the read path.

## Tasks
- [x] Phase 1 built: project scaffolded, landing page + waitlist form, tested locally, committed to git (2026-07-13)
- [ ] **Create a new Supabase project** (separate from Meridian's) — Supabase dashboard -> New Project
- [ ] Copy the Project URL + anon key (Project Settings -> API) into `C:\Users\Angela\Projects\tcm-app\.env.local` (copy from `.env.local.example` first)
- [ ] Run `supabase/schema.sql` once in the Supabase SQL Editor (creates the waitlist table)
- [ ] Test locally: `npm run dev` in that folder, open `http://localhost:3000`, submit the waitlist form, confirm a row lands in Supabase
- [ ] Once tested: push to a new GitHub repo and connect it to Vercel (same env vars added in Vercel's project settings) to get a live link
- [ ] Run the TikTok content test (see [[Content/Ideas/TCM food properties series]]) once the link is live — can run in parallel with later phases
- [ ] Continue the build: open `C:\Users\Angela\Projects\tcm-app` in VSCode, start Claude Code, say "Read PROGRESS.md and continue with the next phase" for Phase 2 (data model + spreadsheet import pipeline)
- [ ] Bring the TCM practitioner reviewer in early, per the Open Gaps section above

## Notes / progress
- 2026-07-12: Pivoted from MyFitnessPal-style tracker to educational ingredient lookup/repository as the primary focus. Personalization (constitution quiz) stays; tracking/logging becomes a future layer added only if demand emerges, not an assumed v2.
- 2026-07-13: Phase 1 built and committed — Next.js/TypeScript/Tailwind/shadcn scaffolded, landing page with 3 ingredient teasers, Supabase-backed waitlist form (insert-only RLS), disclaimer footer, `npm run build` verified working. **Found and fixed a real environment issue:** Next.js 16's default Turbopack production build crashes natively on this machine — `dev`/`build` scripts were pinned to `--webpack`, which builds and runs cleanly. Documented in the project's own `DECISIONS.md` in case it resurfaces on Meridian too.

Related: [[Ventures/index|Ventures]], [[Ventures/Meridian/index|Meridian]]
