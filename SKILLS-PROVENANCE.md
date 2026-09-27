# Skill provenance

Every skill here was read in full and scanned before adding: license OK; no credential/env reads, no injection text, no unexpected network calls. Files are kept byte-identical to upstream (only non-Claude `openai.yaml` files removed).

| Skill | Source | Commit | License | Added |
|---|---|---|---|---|
| supabase-postgres-best-practices | github.com/supabase/agent-skills | 551274e | MIT | 2026-09-27 |
| supabase | github.com/supabase/agent-skills | 551274e | MIT | 2026-09-27 |
| react-best-practices | github.com/vercel-labs/agent-skills | 063bee9 | MIT | 2026-09-27 |
| webapp-testing | github.com/anthropics/skills | 3337550 | Apache-2.0 | 2026-09-27 |
| frontend-design | github.com/anthropics/skills | 3337550 | Apache-2.0 | 2026-09-27 |
| caveman | github.com/JuliusBrussee/caveman | 2fd153c | MIT | 2026-09-27 |
| vibe-security | github.com/raroque/vibe-security-skill | 850938f | MIT | 2026-09-27 |
| ponytail | github.com/DietrichGebert/ponytail (skills/ponytail only; hooks NOT included) | e3ba2aa | MIT | 2026-09-27 |
| no-ai-slop | github.com/petergyang/no-ai-slop | 000650b | MIT | 2026-09-27 |

Notes:
- caveman and ponytail activate on coding sessions; say "stop caveman" / "stop ponytail" to turn off.
- webapp-testing/scripts/with_server.py runs the local dev-server command you pass it (shell=True). Local use only.
