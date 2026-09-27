# vs-skills

Single source of truth for Verified Solutions' vetted Claude Code skills. Installed as a plugin — never copy these into product repos.

## Install (once per machine)
In Claude Code:
1. `/plugin marketplace add blkceasear31/vs-skills`
2. `/plugin install vs-skills@vs-skills`

## Update
1. Change skills here, bump `version` in `.claude-plugin/plugin.json`, commit, push.
2. On each machine: `/plugin marketplace update vs-skills`

## Add a skill
1. Vet it (read every file; run the build-skill-scout checks).
2. Copy the skill folder into `skills/`, unchanged.
3. Add a row to `SKILLS-PROVENANCE.md` (source, commit, license).
4. Bump version, commit, push.

Repo-specific skills (e.g. Aptora's `wo`, guardian's `adr`) stay in that repo's `.claude/skills/`.
