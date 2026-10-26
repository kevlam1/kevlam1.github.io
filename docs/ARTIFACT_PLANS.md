# Artifact plans and ideas

These are Kevin's placeholder ideas plus scoped suggestions. Suggestions are not decisions. Kevin picks. The Artifact 3, 4, and 5 specs have **not** been read. Read each artifact's page before planning it, because it may change the requirements.

## How each artifact repo should start (from the Artifact 2 page and the course guide)
1. Create the repo first, before writing code. Commit as you go.
2. Add a short `CLAUDE.md` in the first session (required or not is unverified, but it is useful). Add a log of what was planned, asked for, decided, and abandoned.
3. Use plan mode when the design is not yet clear.
4. Check what the agent built actually works. Print raw data before trusting it. Run the tests or the app yourself.
5. When finished, fill in the portfolio card (title, link, short reflection) and submit the portfolio link on Canvas.

### Starter CLAUDE.md for a new artifact repo
```markdown
# Project: <name> (TCSS 490 Artifact N)

## Goal
<one or two sentences>. Small scope, built in the time the artifact allows.

## Rules
- Phase 1 only unless I say otherwise: <the smallest useful version>.
- Before using any API field, file format, or library feature, print the raw data or docs and show me.
- Commit small and often. Add to LOG.md when we decide something or drop something.
- No new dependencies without asking. No secrets in the repo (my repos are public).
- Check what you build by running it. Say what you checked and what you could not.

## How to run / test
<fill in>

## Open questions
<fill in>
```

## Artifact 2: MIDI Companion (due Oct 18; first Claude Code build)
**Idea (Kevin's words, tightened):** a browser-based MIDI player and Synthesia-style visualizer. Load a MIDI file, watch notes fall in real time onto a piano, and play along with a connected piano keyboard. The most important mode is Learn: play along with the file.

**Repo:** `kevlam1/midi-companion` (created on GitHub 2026-10-12). Clone it into `TCSS 490/midi-companion` and work on it in a Claude Code session started in that folder.

**Fit with the spec:** small enough for one week, does one real thing, and Kevin will use it with his own MIDI keyboard. It does not need AI at runtime (that is Artifact 3). Deploying is optional for the grade (the card can link to the repo), but the plan is Vercel.

**Time:** Kevin has about 8 to 10 hours a day through Sunday Oct 18 (roughly 50 hours), so audio and Learn mode are in scope.

**Reference app: midee** (`github.com/aayushdutt/midee`, live at `midee.app`). Kevin uses it and likes that it is clean, simple, responsive, and has clear keys and notes. Checked on 2026-10-12 through the GitHub API and its `package.json`:
- **No license** (`"license": null`), so all rights are reserved. Use it for ideas only. Do not copy its code, assets, or styling.
- Stack: Vite + TypeScript, Solid for UI, PixiJS for drawing, Tone.js for audio, `@tonejs/midi` for parsing, `@tonejs/piano` for the piano sound. About 1.9 MB of TypeScript, built since April 2026, so it is far larger than a one-week build.
- Modes: Play, Live, and Learn (Learn has a wait mode that pauses at each chord until the right notes are held, plus hand selection and loop).

**Stack decision (Kevin, 2026-10-12): Vite + TypeScript, no UI framework, Canvas 2D for drawing.**
- React was considered and dropped. The app is one big canvas plus a small toolbar, and per-frame animation should stay outside a UI framework anyway.
- TypeScript was chosen because Learn mode compares key presses against typed note data, and with about 50 hours the setup cost is worth it.
- Vite is the build tool (dev server, TypeScript, bundling). Using a common tool that midee also uses is not copying. Kevin asked about this and accepted the reasoning.
- PixiJS was not chosen. Canvas 2D should handle a few hundred falling notes. Measure the frame rate before reconsidering.
- Node v24.14.1 and npm 11.21.0 are installed (checked 2026-10-12). Vite's minimum Node version is not yet checked.

**Proposed dependencies (each needs Kevin's OK after reading its license)**
1. `@tonejs/midi` to parse `.mid` files. License not yet checked.
2. `tone` for audio. License not yet checked.
3. Piano sound: open question. Maybe `@tonejs/piano` or a simpler synth first. Check the sample license.
Keep the list short so the project does not mirror midee's dependency list.

**Week plan (a plan, not a promise)**
- Mon: repo setup, `CLAUDE.md`, `LOG.md`, deploy a blank Vite page to Vercel, then parse a test MIDI file and print the notes.
- Tue: draw the keyboard and falling notes, with play, pause, restart, and seek driven by one clock.
- Wed: audio.
- Thu: Web MIDI input from Kevin's keyboard; keys light up when pressed.
- Fri: Learn wait mode (pause at each chord until the right notes are held). Left/right hand selection if there is time.
- Sat: polish, log, portfolio card. Sun: buffer.
- Not this week: intervals, sight reading, themes, streaks, video export, sample library.

**Verify**
- A test MIDI file Kevin knows note for note (for example a C major scale he records himself). Check note count, pitches, and timing against what he played.
- Test play/pause/seek timing for drift. Test a file with many simultaneous notes for frame rate (measure it).
- Do not assume what the agent says about a library. Read the docs and show the API it uses.

**Copyright:** MIDI arrangements of real songs are often copyrighted. Keep Kevin's songs in a gitignored `songs/` folder. Commit only test files he made.

**Still to check**
- Which browsers support Web MIDI (check MDN). Test in Chrome or Edge.
- How Kevin's keyboard connects to the PC (USB directly, or a MIDI-to-USB cable).
- Vercel's current docs for deploying a Vite project (Kevin has an account but has not deployed on his own).

## Artifact 3: README.md Architect (due Oct 25; "AI inside it")
**Idea:** a Claude Code skill that analyzes a project's codebase and generates a README from its real structure, technologies, and functionality.
- Read the Artifact 3 page first. Confirm that a skill run by Claude Code counts as the model doing part of the work each time it runs.
- The risk is invented claims. Require the generated README to state only what is in the code, and to say "not found" instead of guessing.
- Test on Kevin's own repos: the portfolio, Cardex, and PokéGuess. Compare the output to the real READMEs and the real code. Record every wrong claim in the log.
- Do not let it include secrets from `.env` files or config.

## Artifact 4: Game Reference Tool (due Nov 8; for someone outside the team; pair or trio)
**Swapped on 2026-10-25:** this slot used to hold the Service Booking Tool, and the Game Reference Tool used to be Artifact 5. Kevin's friends who play the same games are the intended users. The Artifact 4 page has not been read, and it asks for a real person outside the team, so check that the friends fit before designing anything.
- Read the Artifact 4 page first. Ask the friends what they look up today, what annoys them, and what a first version must do.
- A pair or trio means agreeing on a repo, branches, and who owns what. Due Nov 8, so scope the phases below down to what fits.
- The phases, architecture and data sources below were written for a five-week moonshot (it was Artifact 5). With less time, expect to keep phase 1 and perhaps phase 2.

**Idea:** a fast, no-bloat reference for the games Kevin and his friends play: **League of Legends** (champions and items: base stats, ability text, item stats and effects), then **Valorant** (agents, weapons, skins, maybe a model viewer), then **Overwatch** (heroes, perks, player lookup, win/loss by hero and mode). A 3x3 grid of picks that "represent" the user for each game. Information only. No lore, no ads, no wiki sprawl.

This started as Artifact 2, was moved to Artifact 5 because three games is far larger than 8 to 12 hours, and moved again to Artifact 4 on 2026-10-25. A scoped plan was written when it was Artifact 2 (League only, phase 1).

**Suggested phases**
1. League champions and items from a local snapshot of Data Dragon data (champion list and search, champion page with base stats and growth values, ability text as given, item list and search, item page with stats and effect text, patch version shown).
2. The 3x3 champion grid, saved in the browser (localStorage), shareable.
3. Valorant (reference only first), then Overwatch (heroes and perks first, player lookup last).
4. Skins, models, splash art, and richer views.

**Architecture suggestion:** a static site. A small snapshot script downloads the current patch's data into `data/`, and the site reads those files. This keeps pages fast, avoids rate limits and cross-origin problems, and the caching is the optimization story. Live calls are needed only for Overwatch player lookup.

**Data sources and status**
| Game | Source | Status |
| --- | --- | --- |
| League | Data Dragon: Riot's static data (champions, items, runes), versioned by patch, fetched by plain URL | Read in community docs. Documented as inaccurate in places (spell data, item stats), may lag a patch by a day or two, and spell text contains unresolved variables |
| League | Community Dragon: community files that fill ddragon's gaps | More complete but harder to parse |
| Valorant | valorant-api | **Not verified.** Check what it offers, whether it needs a key, and whether it allows browser calls |
| Overwatch | OverFast API, an unofficial API that scrapes Blizzard pages | Read in docs. The public instance has a per-second rate limit (see its home page), and player data depends on the player's profile being public |

**Things to check before relying on them**
- What `champion.json` and `item.json` really contain. Print them and read the fields. Item effects probably appear as description text.
- How stats scale with level. The in-game formula is believed to be non-linear, not growth times level. Verify on the wiki before showing level-based numbers, or show only base and growth values.
- Whether a browser page can call each API (CORS).
- Riot's rules on using game assets (splash art, icons) and any required disclaimer (for example "not endorsed by Riot Games").
- Riot developer keys: a development key is for testing and personal use, a public product needs a production key, and the key must never be in a public repo or in browser code. Static data from Data Dragon needs no key, per the pages read.

**Verify:** spot-check at least five champions and five items against in-game values or the official wiki, and record every disagreement in the log. Test the patch check (does the page show the right version and does the snapshot update). Test empty and error states and a phone-sized window.

**Non-goals for the first version:** exact ability damage numbers (the data is unreliable), accounts, a backend, anything needing a key.

## Artifact 5: Overloaded (due Dec 13; the moonshot)
**Idea:** a browser-based virtual Magic: The Gathering tabletop simulator: build a deck, join a table, and play with friends in real time. Chosen on 2026-10-25, replacing the Game Reference Tool, which moved to Artifact 4. About 5 to 7 weeks.
- It has its own repo and folder, `../Overloaded/` (`github.com/kevlam1/Overloaded`), with its own `CLAUDE.md`. The vision, phases, architecture and open questions live there, so they are not repeated here.
- The Artifact 5 page has not been read. Nothing is built yet.

## Ideas considered and not chosen (in case plans change)
- Service Booking Tool (was Artifact 4): a booking system for a service provider to manage availability, appointments, and customer requests. Dropped on 2026-10-25 when the Game Reference Tool took Artifact 4. If it comes back, it needs a real person outside the team, and decide early what customer data is stored, where, and who can see it.
- Weekly dev summary: reads git history across local repos and writes a markdown report. A plain script can only collect and format; real prose summaries need an AI call (Artifact 3 territory).
- Duplicate and clutter finder with a dry-run mode (compare size, then partial hash, then full hash, and measure speedup).
- Card price watcher for a Pokémon wishlist (Pokémon TCG API, Discord webhook alert).
- Riot match logger or a rate-limit-friendly API client with a cache (uses a development key; keep it out of the repo).
- Project launcher, repo health check, site uptime logger, incremental backup tool, spaced-repetition flashcards, fast note search, Pokémon team type checker, Discord bot for a friends server.
- Free-tier hosting questions (Firebase, Vercel limits) were raised in another chat AI's answer. Those numbers were not verified here. Check the current docs before relying on them.
