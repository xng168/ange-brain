# TCM App

*(working name — rename once the venture has a real name, same as [[Ventures/Meridian/index|Meridian]] did)*

Food/symptom tracker app that layers Traditional Chinese Medicine food-property insight (thermal nature, organ affinity, symptom-based recommendations) onto a MyFitnessPal-style daily logging experience.

- **Stage:** Research complete — wedge and audience decided (2026-07-12). Not yet spec'd for build: no Build Plan or Super Prompt yet (see Documents below). Validating via TikTok content test before committing to build.
- **Model:** Likely freemium mobile app (subscription for personalized recommendations), TBD
- **Origin:** Angela's own idea, explored 2026-07-12

## Concept
- Log food like MyFitnessPal, but each food/ingredient carries TCM properties: thermal nature (hot/warm/neutral/cool/cold), five flavors, organ/meridian affinity
- Symptom- or season-triggered recommendations (e.g. flu symptoms → suggested/avoided foods)
- Positioning thread: "ancient wisdom meets modern tracking" — same narrative lane as Meridian

## Positioning

The gap: existing TCM food tools (TCM Food Therapy, Qi Health, practitioner quiz sites) are static content/lead-gen, not tracking apps with a retention loop; Ayurveda apps (AyuRythm, Prana, Dosha Diet) proved the "traditional-medicine personalized food app" model works in the West but nothing equivalent exists for TCM; even the dominant Chinese tracker (Boohee) is calorie-first, not TCM-property-first. Lead wedge is **dampness/gut-health/bloating** — it maps TCM vocabulary almost 1:1 onto an already-massive, already-trending Western wellness conversation (digestive health market $60.4B→$124.9B by 2034), with the lowest regulatory/credibility risk of the candidate wedges. Audience: Western wellness first, broaden to diaspora/general TCM audience later. Same "ancient wisdom meets modern app" narrative lane as [[Ventures/Meridian/index|Meridian]], and can reuse the Ange.beee distribution channel the way Meridian does.

## MVP scope (v1) — draft, not yet finalized into a Super Prompt

Scoped to the dampness/gut-health wedge, not all of TCM nutrition:

1. Onboarding: TCM body constitution quiz (9 types), framed in Western-friendly language, weighted toward identifying damp/spleen-qi-deficient patterns
2. Food logging (MyFitnessPal-style) with TCM property tags per food: thermal nature, five flavors, organ affinity
3. Symptom journal scoped to digestion/energy (bloating, sluggishness, water retention) logged alongside food, surfacing correlations over time
4. "What to eat when..." lookup scoped first to dampness/digestion, immune/flu, and low energy — not the full materia medica
5. Seasonal tips tied to the 24 solar terms (二十四节气) as a retention/content hook

**Deliberately cut from v1 (backlog, see Feature ideas below):** photo/barcode scanning, practitioner directory/telehealth, cycle-syncing module, postpartum confinement program, AI chat assistant. Revisit once the dampness wedge has traction.

## Market research (2026-07-12)

**Opportunity:**
- Personalized nutrition market ~$18-20B (2025-26); diet/nutrition apps growing ~16.6% CAGR through 2035
- Ayurveda diet apps (closest working analogue) growing ~12.7% CAGR — proves "traditional medicine + personalized food app" is a fundable category in the West
- Clinical evidence exists: an RCT found a TCM-constitution-based mHealth app improved HbA1c/BMI vs. control in prediabetes ([PMC10337399](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10337399/)) — real credibility asset most wellness apps don't have

**Competitors:**
- Direct TCM tools (TCM Food Therapy, Qi Health, Dipara, various practitioner quiz sites) — mostly static web quizzes/content, not tracking apps with a retention loop
- Ayurveda apps (AyuRythm, Prana, Dosha Diet, Doshify) — proven business model, no TCM equivalent at this polish
- Mainstream trackers (MyFitnessPal, Cronometer, Yuka) — no traditional-medicine lens at all
- Boohee 薄荷健康 (dominant Chinese tracker, 100M+ users, 17 years) — calorie-first, not TCM-property-first, even in the most TCM-literate market

**Whitespace:** no polished app combines daily food logging + per-food TCM property tags + symptom/season-based recommendations. Existing TCM tools are lead-gen quizzes, not trackers.

**Risks:** health-claim language risks App Store/regulatory scrutiny (frame as "traditional wellness insight," not medical advice); TCM food-property data isn't standardized across sources; audience split between diaspora users (want accuracy) and Western wellness audience (want quick/vibes content).

**Target audience decision (2026-07-12):** Western wellness audience first, broaden to diaspora/general TCM audience later. Validating via a TikTok content test first — see [[Content/Ideas/TCM food properties series]] and the black-sesame-video edit task in [[Open Items]].

## Candidate niche wedges (2026-07-12 research)

Ranked by fit with the Western-wellness-first audience decision and current trend strength:

1. **Dampness / gut health / bloating** (strongest fit) — digestive health products market is $60.4B (2025) → projected $124.9B by 2034; 37% of Americans now seek digestive-health benefits from diet (up from 30% in 2022); gut-health product launches up 61% 2024→2025. TCM's "dampness" (湿气) framework already maps onto this conversation almost 1:1, and TCM-flavored dampness/bloating content is already circulating organically on TikTok (gua sha for digestion, "how to clear dampness"). Best overlap of TCM authenticity × an already-massive, already-trending Western wellness category, and it stays food-first rather than sliding into diagnostic territory.
2. **Cycle syncing / hormone-aware eating** — huge existing conversation (#cyclesyncing has 285M+ TikTok views, search volume for "cycle syncing diet" doubled since 2022) but currently low-credibility: most creators cite no sources or credentials, and outlets (Time, peer-reviewed articles) are actively calling parts of it unsubstantiated. TCM has a genuine, citable food-therapy tradition here (warming foods around menstruation, classical tonics like 四物汤). Real opportunity to be the "credible, source-cited" entrant into a trend currently starved of one — but needs careful framing (cite classical/practitioner sources, avoid overclaiming efficacy) given the scrutiny the category is already under.
3. **Postpartum confinement (坐月子 / zuo yue zi)** — narrower, shorter-lifecycle audience (pregnant/postpartum, ~30-40 day window per user) but proven crossover appeal and willingness to pay: a Western mom's 30-day Chinese confinement vlog went viral (2.9M views, largely Western audience praise), and confinement retreat centers (Boram NYC, Village SF) are already selling this to non-diaspora customers. High-intent, high-conversion, but works better as a specific program/content pillar inside a broader app than as the sole wedge, since it can't carry ongoing daily retention past the postpartum window.
4. **Qi/Yang deficiency, cold hands & feet, fatigue** — real interest exists (TikTok "adrenal fatigue" discovery content) but overlaps with "adrenal fatigue," a concept conventional-medicine sources actively flag as contested/harmful-trend territory. More reputational risk, weaker signal than the above three — deprioritize as a lead wedge.

**Working recommendation:** lead with dampness/gut health/bloating as the MVP wedge (biggest market, cleanest TCM-to-Western-trend mapping, lowest regulatory/credibility risk), with cycle syncing as a strong second content pillar once the credibility positioning is dialed in, and postpartum confinement as a later feature/program rather than the initial focus.

## Feature ideas (2026-07-12 brainstorm)

**Core loop (beyond static education):**
- Symptom-based lookup — searchable "what to eat when..." for flu, bloating, low energy, cramps, insomnia, etc. (directly maps to the content test)
- Body constitution quiz (9 TCM types) as onboarding — proven pattern from Ayurveda apps' dosha quizzes and from direct competitors (TCM Food Therapy, Qi Health); personalizes recommendations from day one
- Seasonal tips tied to the 24 solar terms (二十四节气) — a TCM-native seasonal calendar that's novel and shareable for a Western audience, good push-notification/retention hook

**Differentiating (closes whitespace nothing else covers):**
- Symptom journal with trend tracking — log recurring symptoms (cold feet, poor sleep, bloating) alongside food and see correlations over time; none of the Ayurveda or mainstream trackers do this longitudinal view
- Food pairing/combination cautions — TCM-specific "don't combine X with Y" guidance, not present in any mainstream tracker
- Photo/barcode scan → TCM property breakdown (Yuka-style) — bigger build lift (needs food recognition + packaged food data) but a strong differentiator if feasible later

**Growth/retention:**
- Shareable quiz results (constitution type) — viral, TikTok-native, same mechanic as MBTI/astrology quiz shares; plugs straight into the Ange.beee distribution channel
- AI chat assistant for "ask about any food or symptom" — cheap to build via LLM + curated dataset (RAG), and rides the "40% of nutrition apps will have an AI coach by end of 2026" trend from the market research
- Therapeutic recipes (congee, herbal soups) tied to symptom/season/constitution — same retention driver that works for Prana/AyuRythm in the Ayurveda space

**Possible monetization beyond subscription:**
- Licensed TCM practitioner directory/telehealth booking (affiliate or booking-fee revenue) — also doubles as the human review layer already planned for data accuracy
- Dual "simplified" vs. "traditional depth" content modes — lets the app serve the Western-first audience now without foreclosing the diaspora audience later

## Data sourcing strategy (2026-07-12)

- **Primary/classical texts:** 本草纲目 *Compendium of Materia Medica* (Li Shizhen, Ming dynasty) — full text public domain/CC BY-SA 4.0 at [Chinese Text Project](https://ctext.org/datawiki.pl?if=en&res=588089&remap=gb); 黄帝内经 *Huangdi Neijing* for foundational theory. These are the ur-sources almost every modern hot/cold food chart traces back to.
- **Modern secondary reference:** Paul Pitchford's *Healing with Whole Foods: Asian Traditions and Modern Nutrition* — the standard English-language reference used by acupuncture schools for food thermal nature; used as a structural model, not scraped wholesale (copyright).
- **Academic pharmacology databases** (herb-level compound/target data — useful for cross-checking an herb's traditional attributions, not consumer-ready food charts out of the box): TCMSP, ETCM, TCMID, BATMAN-TCM, HERB, SymMap.
- **Statistical bridge method:** a peer-reviewed study correlating nutrient composition (water content, potassium/sodium ratio, etc.) with TCM hot/cold classification ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2666154320300247)) — usable to infer properties for foods missing from classical texts (avocado, quinoa, protein powder, packaged foods).
- **Human review layer:** licensed TCM/Chinese medicine practitioner sign-off before publishing any entry — legitimacy, liability protection, and a marketing asset ("reviewed by licensed practitioners").
- **Proposed schema per food entry:** thermal nature, five flavors, organ/meridian affinity, actions/indications, contraindications, source citation(s), confidence/consensus level (since classical and clinic sources sometimes disagree).

## Documents

- **Build Plan** — not yet created. Write once ready to move from research to build, mirroring [[Ventures/Meridian/Build Plan|Meridian's Build Plan]] (step-by-step, no coding experience assumed).
- **Super Prompt** — not yet created. Write once MVP scope above is finalized and a tech stack is chosen, mirroring [[Ventures/Meridian/Super Prompt|Meridian's Super Prompt]] (paste into a fresh Claude Code session to build). Should encode: the dampness-wedge MVP scope, the Western-first audience/tone, the data-sourcing + practitioner-review pipeline, and the same "deterministic-data + AI-interpreter" principle Meridian uses (AI explains/personalizes pre-verified TCM data, never invents a food's property).

## Tasks
- [ ] Run the TikTok content test (see [[Content/Ideas/TCM food properties series]]) before committing further research/build time
- [ ] Once validated: write Build Plan + Super Prompt (see Documents above)

## Notes / progress
_(running notes here)_

Related: [[Ventures/index|Ventures]], [[Ventures/Meridian/index|Meridian]]
