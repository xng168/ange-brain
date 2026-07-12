# Plugins and Skills

Installed deliberately in Phase 11 — every ENABLED plugin loads its skills into every session, so only what earns its keep daily is enabled. Everything else is installed but disabled, for on-demand use.

| Skill / Plugin | Installed | Enabled | Purpose |
|---|---|---|---|
| claude-mem | ✔ | ✔ Enabled | Persistent memory across sessions — also drives the session-summary Stop hook writing into AI OS/Conversations/ |
| Marketing Skills (`marketing-skills@marketingskills`) | ✔ | ✔ Enabled | 47 marketing skills: SEO, copywriting, ad creative, growth loops — daily content work for Ange.beee |
| ECC (`ecc@ecc`) | ✔ | ✘ Disabled | 278 skills, agents, hooks for serious app/software development — big token cost (~34k/session), only worth it once building an app in earnest |
| C-Level Advisor (`c-level-skills@claude-code-skills`) | ✔ | ✘ Disabled | Virtual C-suite advisory (CEO/CFO/CMO/etc. personas) for business strategy sessions — ~5.5k tokens/session, enable only when doing strategy work |
| GStack | ✔ (cloned to `C:\Users\Angela\tools\gstack`, not yet activated) | ✘ Disabled | Garry Tan's dev-workflow skillset (browse, ship, design-review, deploy, etc.) — for when app/website building starts |

## Enabling a disabled plugin later

```
claude plugin enable ecc@ecc
claude plugin enable c-level-skills@claude-code-skills
```

## Activating GStack

GStack isn't a Claude Code plugin in the marketplace sense — it's cloned to a neutral tools folder so it stays fully inactive until needed. To actually activate it when starting to build an app or website:

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup
```

(The copy at `C:\Users\Angela\tools\gstack` can be deleted at that point, or just re-cloned directly into `~/.claude/skills/gstack` — either works.)
