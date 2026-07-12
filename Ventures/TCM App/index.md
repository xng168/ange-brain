# TCM App

*(working name — rename once the venture has a real name, same as [[Ventures/Meridian/index|Meridian]] did)*

Food/symptom tracker app that layers Traditional Chinese Medicine food-property insight (thermal nature, organ affinity, symptom-based recommendations) onto a MyFitnessPal-style daily logging experience.

- **Stage:** Idea / market research complete
- **Model:** Likely freemium mobile app (subscription for personalized recommendations), TBD
- **Origin:** Angela's own idea, explored 2026-07-12

## Concept
- Log food like MyFitnessPal, but each food/ingredient carries TCM properties: thermal nature (hot/warm/neutral/cool/cold), five flavors, organ/meridian affinity
- Symptom- or season-triggered recommendations (e.g. flu symptoms → suggested/avoided foods)
- Positioning thread: "ancient wisdom meets modern tracking" — same narrative lane as Meridian

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

## Data sourcing strategy (2026-07-12)

- **Primary/classical texts:** 本草纲目 *Compendium of Materia Medica* (Li Shizhen, Ming dynasty) — full text public domain/CC BY-SA 4.0 at [Chinese Text Project](https://ctext.org/datawiki.pl?if=en&res=588089&remap=gb); 黄帝内经 *Huangdi Neijing* for foundational theory. These are the ur-sources almost every modern hot/cold food chart traces back to.
- **Modern secondary reference:** Paul Pitchford's *Healing with Whole Foods: Asian Traditions and Modern Nutrition* — the standard English-language reference used by acupuncture schools for food thermal nature; used as a structural model, not scraped wholesale (copyright).
- **Academic pharmacology databases** (herb-level compound/target data — useful for cross-checking an herb's traditional attributions, not consumer-ready food charts out of the box): TCMSP, ETCM, TCMID, BATMAN-TCM, HERB, SymMap.
- **Statistical bridge method:** a peer-reviewed study correlating nutrient composition (water content, potassium/sodium ratio, etc.) with TCM hot/cold classification ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2666154320300247)) — usable to infer properties for foods missing from classical texts (avocado, quinoa, protein powder, packaged foods).
- **Human review layer:** licensed TCM/Chinese medicine practitioner sign-off before publishing any entry — legitimacy, liability protection, and a marketing asset ("reviewed by licensed practitioners").
- **Proposed schema per food entry:** thermal nature, five flavors, organ/meridian affinity, actions/indications, contraindications, source citation(s), confidence/consensus level (since classical and clinic sources sometimes disagree).

## Tasks
_(add tasks here as they come up)_

## Notes / progress
_(running notes here)_

Related: [[Ventures/index|Ventures]], [[Ventures/Meridian/index|Meridian]]
