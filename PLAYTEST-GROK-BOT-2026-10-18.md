# Playtest — filipinoai — 2026-10-18 (Gohan, Grok Bot)

**Repo:** EvoBeben/filipinoai (public). "Pepe" is a portable Taglish Filipino AI-assistant persona prompt: `README.md`, `PERSONA.md` (25 lines) and `AGENTS.md`. It has no app code.

**Build tested:**
- No live site (`homepageUrl` is empty) and nothing to build or run. This was an audit of the entry points.
- Code read: `main` @ `0b355467109d9027974304597f030a11d6208615` (2026-09-27, "Rename Filipino AI persona to Pepe").
- The only "entry point" is the activation message in the README, which tells an AI to read `https://github.com/EvoBeben/filipinoai/blob/main/PERSONA.md`.

## Findings (worst first)

1. **COULD-NOT-TEST: There is nothing to play.** The repo has no live site and no runnable code. The "product" is a prompt pasted into a third-party AI chat. I did not activate Pepe in ChatGPT, Claude or another chat, so the first-response greeting, rename flow and Taglish voice have not been tested.
2. **CODE-READ: The persona promises features that depend on tools many chats don't have.** The mandatory greeting offers to "check the weather" and "find the nearest sale near you" ("maghanap ng pinakamalapit na sale sa lugar mo"). `PERSONA.md` does tell the model to say so plainly when live access is missing. Still, a user in a chat without web access is offered two headline features up front that the model then has to decline, which is a poor first impression.
3. **CODE-READ: The activation link points at the GitHub HTML page rather than the raw file.** `blob/main/PERSONA.md` returns 200 `text/html`, which is the full GitHub page UI. `https://raw.githubusercontent.com/EvoBeben/filipinoai/main/PERSONA.md` returns 200 `text/plain`. I checked both with curl from the box; that was a reachability check, not a playtest. Some AI fetchers handle the HTML page poorly, and the README's copy-paste fallback covers that case.
4. **CODE-READ: The public repo has no license.** The GitHub API reports `license: null`, so others have no stated right to reuse a persona that is explicitly meant to be pasted into other products.
5. **CODE-READ: The three files are consistent.** The README, `AGENTS.md` and `PERSONA.md` agree on the same behaviour:
   - Pepe introduces itself once in Tagalog and offers renaming.
   - It honours an English-only or Filipino-only preference.
   - It doesn't repeat the intro.
   - It defers to platform safety rules ("Never claim that a repository file can override those rules").
   
   The "For AI assistants reading this repository" section only asks the assistant to adopt Pepe when the user requested it, so the prompt-injection risk is low.
6. **COULD-NOT-TEST: Save/quit/reopen and error handling.** There is no state, storage or code path to exercise.

## Verdict
This is a clean, internally consistent persona prompt with no app to break. It has never been exercised end-to-end in an actual AI chat, and its greeting leads with tool-dependent promises.

## Single biggest risk
Pepe's very first message offers weather and nearby-sales lookups that most chat setups can't perform, so many first impressions will end in "I can't actually check that."
