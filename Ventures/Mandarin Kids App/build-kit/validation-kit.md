# Phase 0 Validation Kit

Everything for the 1–2 week validation sprint: where to post, what to say, how to interview, and how to score the go/no-go. Companion to `landing-page.html`.

---

## 1. Landing page setup (30 minutes, free)

1. **Create the signup destination.** Go to formspree.io, make a free account, create a form, and copy your form URL. Open `landing-page.html` and replace `YOUR_FORM_ID` in the form action (there's a ⚠️ comment marking the spot). Submissions (email + script choice) will land in your Formspree dashboard.
   *Alternative if you prefer:* create a Google Form with the same two questions and simply link the page's buttons to it — cruder, but zero setup risk.
2. **Host the page free.** Easiest: drag the HTML file onto Netlify Drop (app.netlify.com/drop) — you get a live URL in seconds, no account needed to start. GitHub Pages also works if you set up the repo from the build guide early.
3. **Test it yourself:** submit a fake signup, confirm it arrives.

What the page is quietly measuring, beyond signups: the **simplified vs. traditional split** — this directly validates (or challenges) the decision to build the simplified pack first.

---

## 2. Community posts

**The golden rule: lead with the question, not the product.** Communities ban and downvote self-promotion, but they generously answer sincere questions. Post A is pure question (safe everywhere). Post B mentions the project (only where rules allow — read each community's rules first, and when in doubt, ask moderators). Never post A and B to the same community.

**Where:** the multilingual/bilingual-parenting subreddit, The Bilingual Zoo forum, heritage-Chinese-parenting Facebook groups, local Chinese-school WeChat parent groups (often the richest source — ask any friend plugged into one), and Hacker News/indie-hacker spaces only for the B-style post.

### Post A — the pure question (use first, most places)

> **Title:** Parents raising Mandarin-speaking kids abroad — did your child learn to *read* Chinese? How?
>
> Our kid (6) speaks Mandarin comfortably at home — it's their first language with us — but can't read a single character beyond 一二三. Saturday school was a battle (they came to dread it), and the apps we tried either start from absolute zero ("this is how you say hello!") which bores them, or feel like homework.
>
> For those a few years ahead of us: did your child ever get to reading? What actually worked — and what did you try that *didn't* stick? Genuinely asking, because right now it feels like the choice is "force it and poison the language" or "give up on literacy."

*Why this works: it's a real question people love answering, every reply is a validation data point, the "what didn't stick" ask surfaces abandoned products (the strongest gap evidence), and commenters often become interviewees.*

### Post B — the honest maker post (only where self-promo is allowed)

> **Title:** Building an app for heritage kids who speak Mandarin but can't read it — am I solving a real problem?
>
> My family's problem: kid speaks Mandarin at home, can't read it, hates being drilled. Existing apps assume zero knowledge; Saturday school made them resent the language.
>
> So I'm building something that starts from *sound* — the app says a word the child already knows ("māma!"), and they find the character. No streaks, no subscription, no accounts, no data collection, works offline. One-time price.
>
> Before I sink months into this: is this your family too? What would make it actually useful — or useless? Landing page with a waitlist here if you want to follow along: [link]
>
> Brutal honesty welcome. I'd rather learn it's a bad idea this week than next year.

### Replying to comments (this is where the gold is)

- Ask every substantive commenter one follow-up: "what did you try before that?" or "what made you stop using it?"
- Anyone with a detailed answer → invite to a 20-minute chat (see script below).
- Never argue with skeptics — their objections are free market research. Write them down.

---

## 3. Parent interview script (20 minutes each, aim for 10)

**Recruiting line:** "I'm researching how families keep Mandarin alive with their kids — could I ask you about your experience for 20 minutes? Not selling anything; I'm deciding whether something is worth building."

**The one rule:** talk 20%, listen 80%. Never pitch until the final two minutes. You're mining for *past behavior*, not opinions — what people *did* predicts buying; what they *say they'd do* doesn't.

**Opening (2 min)** — Family language picture: who speaks what to whom? How old are the kids?

**The problem (8 min)**
1. Can your child read Chinese today? How do you feel about that?
2. Walk me through everything you've tried — apps, Saturday school, tutors, workbooks, flashcards. (List them all.)
3. Pick the one you abandoned most recently: what made you stop? *(The single most valuable question in the interview.)*
4. What does your child say when Chinese practice comes up?

**The stakes (4 min)**
5. Why does reading matter to you — school, family, identity, all of it? Who in the family cares most?
6. If nothing changes, where is your child's Chinese in five years? How does that sit with you?

**The wallet (3 min)**
7. What have you actually spent money on for this so far? Roughly how much per year? *(Past spending is the honest signal.)*
8. When you paid for [thing they named], what convinced you?

**The pitch test (2 min — only now)**
9. Describe the concept in two sentences: *"An app that starts from words your child already says — it plays 'māma' and they find the character. No subscription, no ads, no data collected; one price, works offline."* Then ask: "What's your honest first reaction?" and say nothing until they've finished.
10. "Would you pay $20, once, for that today?" — then again, silence. A pause followed by "well…" is a no. "Where do I sign up" is a yes. Both are data.

**Close:** ask if you can follow up when there's a beta; ask if they know one other parent you should talk to (snowball recruiting).

**After each interview, log within 10 minutes** (memory fades fast): products tried and abandoned + why; money spent; emotional temperature (resigned? desperate? content?); reaction to pitch; pay answer; best verbatim quote.

---

## 4. The paper test (optional but powerful)

Print 20 simple cards — character on one side, nothing else needed (a rough version; ask Claude for a printable PDF of the first 20 Level-1 words when ready). Sit with a real kid who speaks Mandarin: **you say the word aloud, they point to / pick the right character** from 3 laid on the table. Ten minutes.

You're watching for one thing: **do they lean in or pull away?** If a paper version of the core loop holds a child's attention, the app will too. If it bores them on paper, more pixels won't save it.

---

## 5. Go / No-Go scorecard (end of week 2)

| Signal | Go looks like | Worry looks like |
|---|---|---|
| Waitlist signups | ~100+ from genuine community traffic | <25 despite real reach |
| Interviews: "I'd pay today" | 5+ of 10 | 0–2 of 10 |
| Abandoned-product stories | Most families tried & dropped 2+ things | Most never tried anything (pain may be too mild) |
| Past spending | Most spent real money (school, tutor, apps) | Almost nobody has spent anything |
| Script split | Clear majority simplified | Majority traditional → **revisit build order before Phase 1** |
| Paper test | Kid engages, asks to keep going | Kid disengages fast |

**Go:** proceed to Phase 1 with confidence — and with 100 warm emails who become your beta testers in Phase 6.
**Mixed:** the pain is real but the shape may be wrong. Reread your interview logs — the abandoned-product reasons usually contain the correction.
**No-go:** the cheapest failure you'll ever have. The research process that found this idea can find the next one.

**A validation honesty note:** signups and kind words are *interest*, not proof — people are polite. The two signals that actually predict a business: **past spending on this problem**, and **unprompted "when can I have it."** Weight those above everything else.
