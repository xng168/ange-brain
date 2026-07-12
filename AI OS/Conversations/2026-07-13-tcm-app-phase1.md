# TCM App Phase 1 scaffolded and tested

- **Built Phase 1 from scratch:** Scaffolded a Next.js 16 + TypeScript + Tailwind + shadcn/ui project at `C:\Users\Angela\Projects\tcm-app` with a working landing page, product narrative (3 ingredient teasers: ginger, mung bean, watermelon), and a functional waitlist form wired to Supabase.

- **Fixed a build blocker:** Discovered Next.js 16's default Turbopack crashes on this machine; diagnosed the native error, switched the project to webpack (which builds and runs cleanly), and documented the decision in `DECISIONS.md` for future reference (Meridian may hit the same issue).

- **Project infrastructure:** Added project-memory files (`PROGRESS.md`, `DECISIONS.md`, `BACKLOG.md`, `README.md`), a Supabase schema with SQL setup, a security policy for insert-only access, and disclaimer footer on every page. Committed to local git repo.

- **Tested locally:** Dev server runs, landing page renders correctly with all UI components, production build succeeds, and form submission is wired (awaiting live Supabase connection).

- **Next steps (requires your action):** Create a new Supabase project, add URL + anon key to `.env.local`, run the SQL schema, test the form with a live email submission, then push to GitHub and connect Vercel. After that, move to Phase 2 (data model + spreadsheet import pipeline) in Claude Code.
