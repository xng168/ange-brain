# Meridian — Business Model

Revenue streams and cost forecast, drafted 2026-07-12. All figures USD. Assumptions are marked — revisit after beta.

## Revenue streams (ranked)

### 1. Premium subscription — the core engine
Free tier: profile + charts, daily card, core reading, 10 chat messages/day.
**Premium (~$7.99/mo or $49.99/yr):** unlimited AI chat, full yearly deep reading, monthly deep readings, (v2: compatibility readings).

Competitor benchmarks: CHANI ~$11.99/mo · The Pattern ~$14.99/mo · Co-Star premium ~$2.99–5.99/mo · Dimensional Plus ~$60/yr. $7.99 sits deliberately mid-pack — under the "wellness app" ceiling, above impulse-tier. *(Hypothesis — test $5.99 vs $7.99 vs $9.99 later.)*

Freemium reality check: consumer apps convert **2–5%** of active users to paid. Astrology skews engaged/ritualistic (daily open habit), so 3–5% is achievable once the readings feel personal.

### 2. One-off paid readings (à la carte) — very natural for this category
Fortune telling has a strong pay-per-reading culture (especially in the Chinese metaphysics market — people pay real money for 流年 reports). One-offs monetise people who won't subscribe:
- **"Your Year Ahead" deep report** ($9.99–14.99) — flagship; sells hardest around Western New Year AND Lunar New Year (Meridian gets *two* peak seasons — a real structural advantage over Co-Star)
- Career/decision reading, relationship-style reading ($4.99–9.99)
- **Giftable readings** — "buy a Year Ahead for a friend" (birthdays, LNY); gifting doubles as acquisition

### 3. Compatibility unlocks (v2, with the social layer)
Free: basic compatibility score with a friend. Paid: full synastry + BaZi 合婚-style + personality-pairing deep dive. Built-in viral loop — you must invite the friend to unlock. This is Dimensional's money-maker; ours goes deeper with the East-meets-West angle.

### 4. Creator-flywheel (indirect but real)
Meridian content on Ange.beee = $0 CAC. In reverse, the app grows the audience, which raises brand-deal value. Later: sponsorships/collabs inside content (not inside the app), and — given Angela's e-commerce ambitions — element/sign-based physical products (candles, jewellery) as a separate venture bridge. **Do none of this before the app has traction.**

### ✗ Not doing: ads
Cheapens a trust/self-knowledge product, terrible revenue below ~1M users, conflicts with premium positioning.

## Revenue scenarios (subscription + one-offs)

Assumes $7.99/mo blended (annual discount pulls average down → use $7/payer), one-offs adding ~20% on top of subscription revenue.

| Registered users | Paid conversion | Subscription /mo | + One-offs | Revenue /mo |
|---|---|---|---|---|
| 1,000 | 3% | ~$210 | ~$40 | **~$250** |
| 10,000 | 4% | ~$2,800 | ~$560 | **~$3,350** |
| 100,000 | 5% | ~$35,000 | ~$7,000 | **~$42,000** |

Payment rails: **Stripe** on the web app (~2.9% + $0.30 per charge). This is a big reason web-first wins: a native iOS app must sell digital goods through Apple's in-app purchase (15% cut under the Small Business Program, 30% above $1M). Web revenue keeps ~97%.

## Cost forecast

### AI unit economics (the cost that scales with users)
Current API pricing: Claude Sonnet 5 $3 in / $15 out per million tokens (intro $2/$10 until 2026-08-31); Haiku 4.5 $1/$5; cached input ~0.1× price. Meridian's architecture generates each reading **once and caches it in the database**, so cost scales with users, not with opens:

| Item | Model | Frequency | Est. cost |
|---|---|---|---|
| Core "Know Yourself" reading | Sonnet 5 | once per user | ~$0.04 |
| Yearly outlook | Sonnet 5 | 1×/year | ~$0.04 |
| Monthly direction | Sonnet 5 | 1×/month | ~$0.02 |
| Daily card | Haiku 4.5 | 1×/day, generated on open | ~$0.002/day |
| Chat message | Sonnet 5 (context prompt-cached) | per message | ~$0.005–0.01 |

→ **Typical active free user: $0.10–0.40/month.** Heavy premium chat user: $2–4/month worst case — still >50% margin on $7.99. The free-tier chat cap (10/day) is the safety valve; the daily card is nearly free by design.

### Fixed costs by stage

| Stage | Infra | AI total | Total /mo | Notes |
|---|---|---|---|---|
| **Build (now)** | $0 (free tiers) | $5–20 one-off credit | **<$50 total** | Only real spend: Anthropic Console credit + domain (~$15/yr) when named |
| **Beta, 0–1k users** | $0–45 | $10–50 | **~$50–100** | Vercel Pro $20 (Hobby tier is non-commercial — upgrade when charging money), Supabase free until limits |
| **Growth, 1k–10k** | ~$45–100 | $100–400 | **~$150–500** | Supabase Pro $25; email service (~$20) for magic links at volume |
| **Scale, 100k** | few hundred | $2k–5k | **~$3k–6k** | Revenue at this stage ≈ $42k/mo — costs stay <15% of revenue |

### Break-even
Running costs pre-scale ≈ $50–100/month → **covered by ~10–15 premium subscribers.** This venture's financial risk is essentially zero; the real cost is Angela's time, and the real risk is retention (do people come back daily?) — which is why the daily card is the signature feature.

### Later costs (only after traction)
Apple Developer $99/yr + Google Play $25 one-off (native wrap) · company registration/GST when revenue is real (get local advice) · optional paid analytics/support tools.

## Key decisions this implies

1. **Don't build payments in MVP** (already the plan) — but Phase 5's yearly/monthly readings should be built as the future premium surface.
2. **Ship the "Year Ahead" report as the first paid thing** — one Stripe payment link can even sell it before full subscription infrastructure exists.
3. **Two new-year seasons** (Jan 1 + Lunar New Year) are Meridian's natural launch/marketing windows — work backwards from the nearest one.
4. Watch one number in beta: **day-7 retention** (do they still open the daily card after a week?). Conversion follows retention in this category.

Related: [[Ventures/Meridian/index|Meridian]] · [[Ventures/Meridian/Build Plan|Build Plan]] · [[Ventures/Meridian/Super Prompt|Super Prompt]]
