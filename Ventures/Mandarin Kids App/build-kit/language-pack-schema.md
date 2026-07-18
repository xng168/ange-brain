# Language-Pack Schema — v2 Draft (symmetric two-language model)

The single rule this whole design protects: **the app code contains zero specific words, audio, or scripts.** Everything language-specific lives in a pack file the app reads at runtime. English/Chinese is the first pack; future pairs are new packs, not new code.

**What changed from v1 (and why):** the two languages are now fully symmetric. Instead of one side being "heritage" and the other "support" — which assumed a fixed role — a pack now has `language_1` and `language_2`, each carrying an **identical set of fields**, each with its own text, audio, and script details. Which language the child is currently learning is a *setting the app tracks*, not something baked into the data. This means a future Spanish/English pack, or a Korean/Japanese pack, or a pack where the child switches direction freely, all use the exact same shape. Every pack is interchangeable.

This draft is deliberately scoped to the languages we can foresee soon — alphabetic (Latin-script) languages and character-based Asian languages. It is **not** designed for every language on Earth (no right-to-left, no grammatical-gender handling yet). Expect to revise the format *once*, when a genuinely different second language arrives. That revision will be small because content is already separated from code.

---

## 1. Pack structure (top level)

A pack is one file (JSON) plus a folder of assets (audio, images, stroke data). The file has four sections:

- `pack_meta` — the two languages this pack contains and how each behaves
- `levels` — the difficulty ladder
- `categories` — vocabulary groupings
- `cards` — the actual content (the word list)

---

## 2. `pack_meta` — the two languages, described identically

Both languages are described with the **same block of flags**, so neither is privileged. The code reads these flags rather than "knowing" anything about a specific language.

```json
"pack_meta": {
  "pack_id": "zh-hans-en",   // simplified pack; traditional ships as its own pack: zh-hant-en
  "version": "2.0.0",
  "display_name": "Chinese (Simplified) · English",
  "language_1": {
    "name": "Chinese (Mandarin)",
    "code": "zh",
    "script": "simplified",
    "uses_characters": true,
    "uses_romanization": true,
    "romanization_name": "pinyin",
    "is_tonal": true,
    "has_stroke_order": true
  },
  "language_2": {
    "name": "English",
    "code": "en",
    "script": "latin",
    "uses_characters": false,
    "uses_romanization": false,
    "romanization_name": null,
    "is_tonal": false,
    "has_stroke_order": false
  },
  "learning_directions": ["1_from_2", "2_from_1"],
  "default_direction": "1_from_2",
  "audio_format": "m4a"
}
```

Every language block has the identical seven fields — a language simply fills in the ones that apply and sets the rest to `false`/`null`. English sets `uses_characters`, `uses_romanization`, `is_tonal`, `has_stroke_order` all to false; Chinese sets them true. A future Spanish block would look like English's but with `name: "Spanish"`. Because the fields are always the same, the app never needs to know *which* language is in slot 1 — it just reads the flags.

`learning_directions` lists which ways this pack can be studied (`1_from_2` = "shown language 2, learn language 1"), and the app lets the child switch between any listed direction — this is what powers your "choose which language to improve" feature. `default_direction` is just the starting point.

---

## 3. `cards` — the content entries (both sides identical in shape)

Each flashcard has a `language_1` block and a `language_2` block **with the same fields**. Whichever language a word "starts" in, both sides are described the same way. Script-specific fields are simply `null` when a language doesn't use them.

```json
{
  "id": "0001",                     // required, unique
  "category": "family",             // required, matches a category id
  "level": 1,                        // required, matches a level id
  "language_1": {
    "text": "妈妈",                 // required — how it's written
    "text_alt": null,               // optional variant field; traditional Chinese is a SEPARATE pack, not this field
    "romanization": "māma",         // optional — null if language has none
    "tones": [1, 0],                // optional — null if not tonal
    "audio": "audio/zh/0001.m4a",   // required — native-speaker recording
    "stroke_data": "strokes/zh/0001.json"  // optional — null if no stroke order
  },
  "language_2": {
    "text": "mom",                  // required
    "text_alt": null,
    "romanization": null,
    "tones": null,
    "audio": "audio/en/0001.m4a",   // required — English gets its OWN audio file
    "stroke_data": null
  },
  "image": "images/0001.png",       // standard field — a picture for this word; null for abstract words (see §7)
  "notes": "core family word"       // optional — internal, not shown to child
}
```

The key point for your second request: **`language_2` (English here) has its own `audio` field, filled in exactly like `language_1`.** Both languages are always fully recorded, so the child can hear either side and study in either direction. The only fields English leaves empty are the ones that don't apply to it (romanization, tones, stroke data) — but the *fields exist* in both blocks, so the shape is identical and any future pack drops in cleanly.

---

## 4. Difficulty levels

The key insight that makes leveling here different from a normal language app: **the child already knows these words in one language.** So difficulty is driven by how frequently the word comes up in the child's actual home life, and — for character-based languages — how visually complex the writing is. The ladder moves from single high-frequency words → common everyday words → broader vocabulary → short phrases.

```json
"levels": [
  { "id": 1, "name": "First Words",         "unit": "single words / characters" },
  { "id": 2, "name": "Everyday Words",      "unit": "common everyday words" },
  { "id": 3, "name": "Around Me",           "unit": "broader vocabulary" },
  { "id": 4, "name": "Putting It Together", "unit": "short phrases" }
]
```

**Level 1 — First Words.** The most frequent, simplest words a child says constantly. Instant wins so it never feels like Saturday school.
**Level 2 — Everyday Words.** Common two-part everyday words: family, food, animals, colors, feelings, objects.
**Level 3 — Around Me.** Broader vocabulary and the wider world — home, nature, routine, travel, time.
**Level 4 — Putting It Together.** Known words combined into short, high-value phrases — the "read a message from grandma" payoff.

Levels are entries in this list, so **adding a Level 5 later is one more line of data, not a code change.** The app counts levels from the pack; it never assumes there are four.

---

## 5. Vocabulary categories

Categories cut *across* levels and exist to power the matching game and let a parent pick a theme. Like levels, they're data — **add a new category by adding a line; the app never hardcodes the list.**

```json
"categories": [
  { "id": "family",     "name": "Family & People" },
  { "id": "food",       "name": "Food & Drink" },
  { "id": "body",       "name": "Body" },
  { "id": "animals",    "name": "Animals" },
  { "id": "numbers",    "name": "Numbers" },
  { "id": "colors",     "name": "Colors" },
  { "id": "actions",    "name": "Actions" },
  { "id": "home",       "name": "Home & Objects" },
  { "id": "nature",     "name": "Nature & Weather" },
  { "id": "feelings",   "name": "Feelings" },
  { "id": "routine",    "name": "Daily Routine" },
  { "id": "social",     "name": "Greetings & Manners" },
  { "id": "describing", "name": "Describing Words" },
  { "id": "travel",     "name": "Travel & Places" },
  { "id": "time",       "name": "Time" }
]
```

---

## 6. Worked example (a few real cards)

```json
"cards": [
  {
    "id": "0001", "category": "family", "level": 1,
    "language_1": { "text": "妈", "text_alt": null, "romanization": "mā", "tones": [1],
                    "audio": "audio/zh/0001.m4a", "stroke_data": "strokes/zh/0001.json" },
    "language_2": { "text": "mom", "text_alt": null, "romanization": null, "tones": null,
                    "audio": "audio/en/0001.m4a", "stroke_data": null },
    "image": "images/0001.png"
  },
  {
    "id": "0006", "category": "food", "level": 1,
    "language_1": { "text": "水", "text_alt": null, "romanization": "shuǐ", "tones": [3],
                    "audio": "audio/zh/0006.m4a", "stroke_data": "strokes/zh/0006.json" },
    "language_2": { "text": "water", "text_alt": null, "romanization": null, "tones": null,
                    "audio": "audio/en/0006.m4a", "stroke_data": null },
    "image": "images/0006.png"
  }
]
```

---

## 7. Images (a standard per-card field)

Every card has an `image` field. This is deliberate: the picture belongs to the *word*, so it's reused everywhere — flashcards, the matching game, and anything added later. The matching game is therefore not a separate content pile; it simply draws from cards that already carry an image. One picture per word, sourced once.

**Two rules the app must follow:**

1. **`image` can be `null`, and the app must handle that gracefully.** Roughly two-thirds of the words are concrete and picturable (cat, water, red, airplane); the rest are abstract (to want, sorry, yesterday, how are you?) and have no sensible picture. Forcing an image onto an abstract word produces confusing art, so those cards set `image: null`. Any screen that shows images must fall back cleanly — a flashcard with no image just shows the word and plays audio; it must never render a broken-image box.
2. **The matching game only uses cards where `image` is not null.** That's still plenty of cards for a fun game, and it keeps the game visual and unambiguous. The game must count its available image-cards from the pack, never assume a fixed number.

**Sourcing (a content-gate item — must run in parallel with the build, not after):** all images need a licence permitting commercial use, in one consistent visual style, and must be child-appropriate and instantly recognisable. The recommended v1 route is a single commercially-licensed children's icon set in one flat, friendly style covering the ~200 concrete words, with the licence documentation kept in the project as proof. Track the source and licence of each image as you go (the content spreadsheet has a column for this).

## 8. How this proves out for the next language

A Spanish/English pack reuses this exact format. Because both blocks already have identical fields, Spanish just goes in `language_1` with its own audio, and English stays in `language_2` — no code change, and the tracing/pinyin features switch off automatically because Spanish's flags say so:

```json
{
  "id": "0001", "category": "family", "level": 1,
  "language_1": { "text": "mamá", "text_alt": null, "romanization": null, "tones": null,
                  "audio": "audio/es/0001.m4a", "stroke_data": null },
  "language_2": { "text": "mom", "text_alt": null, "romanization": null, "tones": null,
                  "audio": "audio/en/0001.m4a", "stroke_data": null },
  "image": "images/0001.png"
}
```

Same schema, same activities, no code change. That's the payoff of deciding the symmetric model now.

---

## Decisions locked (previously open questions)

1. **Simplified vs. traditional → two separate packs.** A family picks their pack at install (`zh-hans-en` or a future `zh-hant-en`); `text_alt` is not used for traditional characters. The traditional pack is future work (see CLAUDE.md future features).
2. **Level 4 phrase audio → one audio file per whole phrase.** Simpler to record, and it teaches natural phrase rhythm and tone flow.
3. **Images → a standard per-card field** (see §7): one image per concrete word, `null` for abstract words, single consistent commercially-licensed style, with source/licence tracked per word in the content spreadsheet.
