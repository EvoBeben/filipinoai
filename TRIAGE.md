# Triage — EvoBeben/filipinoai — 2026-10-15

## Verdict: KEEP

## What it is
"Pepe" — a portable Filipino AI persona prompt: a warm, witty Taglish assistant persona (PERSONA.md) that a user can load into ChatGPT, Claude, Grok, or a local model via a GitHub link or copy-paste, plus a README with activation instructions and an AGENTS.md for coding agents.

## Live check (gh, 2026-10-15)
- Repo: PUBLIC, default branch `main`, last push 2026-10-13T23:50:28Z, disk 13 KB, GitHub description **empty**, no primary language (no code).
- Open issues: **0**. Open PRs: **1** — #1 `psy/debug-pass` "Docs alignment pass: AGENTS/README consistency with PERSONA" (2 files, +2/−2, opened 2026-10-13, still unmerged).
- Remote branches (5): `main`, `GROK` (tip identical to `main` @ 0b35546), `add-persona-prompt` and `readme-points-to-persona` (both fully merged ancestors of `main`), `psy/debug-pass` (PR #1).

## Stack / structure
- No code at all. Three Markdown files, 51 lines total: `PERSONA.md` (canonical persona + greeting, 25 lines), `README.md` (activation instructions, 19 lines), `AGENTS.md` (agent instructions, 7 lines).
- No build system, package manifest, tests, CI, deploy config, or LICENSE.

## Build result
- **N/A — nothing to build.** No `package.json` / `Makefile` / `requirements.txt` / `pyproject.toml` exists (checked, all absent); documented "setup" is reading/copying Markdown, which was done in full.
- Link check: the one external URL in the repo (the `blob/main/PERSONA.md` activation link) targets a file verified present on `main`; all internal cross-references (README ↔ PERSONA ↔ AGENTS) resolve to files in the repo root.

## Code health
- Content is consistent and current: the Kiko → Pepe rename is complete — **zero "Kiko" remnants on `main`** — and README, AGENTS.md, and PERSONA.md agree on name, greeting, and rename offer.
- No TODO/FIXME markers anywhere.
- **Hardcoded secrets: none found** — pattern scan (api key / secret / password / token / key-block markers) returned zero hits. Expected for a docs-only repo, but verified since this repo is public.
- Dead weight is branches, not code: 3 of 4 non-main branches are fully merged, and `GROK` is a duplicate pointer at `main`'s tip.
- Only real failure mode so far is cross-file drift: the rename took 3 separate commits (one per file), and open PR #1 exists solely to re-align AGENTS.md/README wording with canonical PERSONA.md.

## The 5 improvements (ranked by impact/effort)
1. **Add a raw-content activation link next to the blob URL** — the README tells AIs to "read" the `github.com/.../blob/...` page, which serves an HTML wrapper many fetchers handle poorly; adding the `raw.githubusercontent.com` URL for PERSONA.md (plain Markdown) raises activation success across tools for a one-line change.
2. **Land or close PR #1, then prune the merged/duplicate branches** — merge the approved 2-line alignment in `psy/debug-pass` (or close it as declined), and delete `add-persona-prompt`, `readme-points-to-persona`, and `GROK` (all fully merged; GROK == main tip) so `main` is unambiguous as the canonical source.
3. **Add a LICENSE and fill in the GitHub description/topics** — this is a public repo whose whole purpose is other people copying the persona into their own chats; with no license it is all-rights-reserved by default, and the empty description makes it undiscoverable.
4. **Version the persona (CHANGELOG + a v1 tag/release)** — anyone hot-linking PERSONA.md gets silent behavior changes whenever `main` moves (as the Kiko → Pepe rename proved); a tag lets users pin a version and a changelog tells them what changed.
5. **Add a tiny consistency check** — a grep-level script or GitHub Action asserting the persona name matches across all three files, PERSONA.md still contains exactly one `---` divider above the prompt, and internal links resolve — drift between the three files is this repo's only demonstrated defect class.
