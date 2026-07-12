# TCM App Waitlist Bug Fix & Audit

- **2 bugs found, fixed, verified, and committed** (commit 4ecc702): (1) Missing Supabase env handling would crash the site on form submission if `.env.local` wasn't configured—now fails gracefully with "The waitlist isn't connected yet" message; (2) Email deduplication treated `Foo@Example.com` and `foo@example.com` as different users—now lowercased before saving.

- **Production-ready checks passed**: build succeeds, lint has zero warnings, database security policy is correct, `.env.local` properly excluded from git (template tracked), disclaimer footer on all pages.

- **Deferred non-blockers**: No rate limiting on waitlist (acceptable for Phase 1, revisit at Phase 7 polish); `shadcn` listed as app dependency instead of build-only tool (harmless).

- **Next step**: Create Supabase project, fill `.env.local`, run schema SQL, test real form submission—exact steps in TCM App tasks. From prior session: prep work (content-test success metrics, practitioner outreach draft, ingredient shortlist, Open Items) still pending.
