# TCM App: Research & MVP Scope Finalized

**What was done:**
- Completed comprehensive market research: identified digestive-health market at $60.4B (2025) → $124.9B by 2034; validated Ayurveda apps (AyuRythm, Prana, Dosha Diet) as proof-of-concept category at 12.7% CAGR; surveyed 5+ competitor categories (static TCM sites, mainstream trackers, Chinese apps like Boohee)
- **Resolved audience tension:** locked decision to lead with Western wellness audience first (not Chinese diaspora), as proven by massive digestive-health trend ($60.4B market, 37% of Americans now seek digestive benefits from diet)
- **Selected dampness/gut-health as the lead wedge:** strongest fit for this audience decision—maps TCM vocabulary almost 1:1 onto existing bloating/wellness conversation, already trending on TikTok, lowest regulatory/credibility risk vs. cycle-syncing (contested in mainstream media) or postpartum confinement (narrower lifecycle)
- **Locked MVP scope (v1)** scoped explicitly to dampness/gut-health wedge only: TCM body constitution quiz (9 types) + MyFitnessPal-style food logging with TCM tags + digestion/energy symptom journal + scoped "what to eat when" lookup + seasonal tips (24 solar terms); deliberately cut photo scanning, practitioner directory, AI chat, cycle-syncing, postpartum program to v2 backlog
- **Documented complete data-sourcing pipeline:** primary sources (*Compendium of Materia Medica*, *Huangdi Neijing*), secondary reference (Pitchford's *Healing with Whole Foods*), academic databases (TCMSP, ETCM, TCMID, BATMAN-TCM, HERB, SymMap), statistical bridge method for modern foods (nutrient composition → TCM properties), licensed practitioner review layer, proposed per-entry schema with citations & confidence levels
- **Restructured venture file to mirror Meridian format:** added Positioning section, explicit MVP scope breakdown, Documents section with Build Plan & Super Prompt placeholders (noting what they should encode: dampness wedge scope + Western-first tone + data pipeline + "deterministic data + AI interprets" principle), migrated tasks to Open Items.md checklist

**Key decisions made:**
- Validation gates before build: run TikTok content test first (black sesame video + TCM food properties series) to confirm audience response before committing to Build Plan + Super Prompt
- Reuse Meridian's "deterministic data + AI interprets, never invents" architecture for TCM food properties—AI personalizes/explains pre-verified data, never generates made-up properties
- Western-first positioning as initial wedge, explicitly deferring diaspora/general TCM audience to v2 once dampness wedge has traction
- Scope ruthlessly for v1: avoid photo scanning (ML cost) and AI chat (tempting but non-core) to get to product-market fit faster

**What's next:**
Run the TikTok content test (existing Ange.beee channel) before writing Build Plan or Super Prompt—the validation result should shape what actually goes in the build spec. Two concurrent tasks: (1) edit black sesame video, (2) film/post TCM food properties series (ginger, flu-symptom foods). Once validated, write Build Plan + Super Prompt, mirroring Meridian process.
