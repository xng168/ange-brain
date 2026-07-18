# Mandarin Build Kit: Verification & Sync Complete

- **Verified all 7 build-kit files** against the authoritative web session and found + fixed a gap: applied missing inline Python cleanup (message 58) that corrected stale content in CLAUDE.md, language-pack-schema.md, and build-guide.md.
- **All kit files now pass validation**: 292 words / 584 clips / 211 images in the spreadsheet (exact match); CLAUDE.md references corrected (Expo, not Xcode); language-pack schema renumbered; HTML landing page verified (265 lines, 2 intentional Formspree ID markers).
- **Found index.md is out of sync**: venture note describes ~150 words (ages 3–7, 3 activities) but real kit is 292 words (ages ~5–10, 5 activities + parent area + spaced repetition) targeting heritage kids who *speak* but can't *read* Mandarin — needs rewrite.
- **28 other conversations remain untouched**: raw JSON archived in `_sources/`, but per layered + full-transcript choice, eyewear branding, HK visa, resume tailoring, and 25 others haven't been migrated to notes or filed yet.
- **Recommended next**: (1) sync index.md to match authoritative kit (quick), (2) run full layered migration of 28 conversations into transcript notes filed by pillar.
