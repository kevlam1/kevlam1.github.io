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

## Artifact 2: MIDI Visualizer (due Oct 18; first Claude Code build)
**Idea (Kevin's words, tightened):** a browser-based MIDI player and Synthesia-style visualizer. Load a MIDI file, watch notes fall in real time onto a piano, and play along with a connected piano keyboard.

**Fit with the spec:** small, does one real thing, and it is something Kevin would use. It does not need AI at runtime (that is Artifact 3). It does not have to be deployed, but a static page would deploy to GitHub Pages or Vercel easily.

**Suggested phases (a suggestion, not a decision)**
1. Load a `.mid` file and parse it into a list of notes (pitch, start time, duration). Print the parsed data and compare against a file whose notes are known.
2. Draw falling notes over a piano keyboard on a canvas, synced to a clock. Play, pause, restart.
3. Play audio for the notes.
4. Stretch: accept notes from a connected keyboard and mark hits and misses.

**Verify**
- Use two or three MIDI files with known content (short scale, a short piece Kevin knows). Check note counts, timing, and tempo changes against what he knows.
- Test play/pause/seek timing for drift. Test a file with many simultaneous notes for frame rate (Kevin likes optimization, so measure it).
- Do not assume what the agent says about a MIDI library. Read the docs and show the API it uses.

**Unverified, check first**
- Which browsers support the Web MIDI API (input from a connected keyboard). Check MDN or caniuse. Do not assume Safari or Firefox support.
- Whether to parse MIDI with a library or by hand, and the library's license.
- Where test MIDI files come from (license). Prefer files Kevin made or that are clearly free.

## Artifact 3: README.md Architect (due Oct 25; "AI inside it")
**Idea:** a Claude Code skill that analyzes a project's codebase and generates a README from its real structure, technologies, and functionality.
- Read the Artifact 3 page first. Confirm that a skill run by Claude Code counts as the model doing part of the work each time it runs.
- The risk is invented claims. Require the generated README to state only what is in the code, and to say "not found" instead of guessing.
- Test on Kevin's own repos: the portfolio, Cardex, and PokéGuess. Compare the output to the real READMEs and the real code. Record every wrong claim in the log.
- Do not let it include secrets from `.env` files or config.

## Artifact 4: Service Booking Tool (due Nov 8; for someone outside the team; pair or trio)
**Idea:** a booking system for a service provider to manage availability, appointments, and customer requests.
- Read the Artifact 4 page first. The "someone" must be a real person outside the team. Find that person before designing anything, and ask how they take bookings today, what annoys them, and what a first version must do.
- Customers' personal details will be involved. Decide early what is stored, where, and who can see it.
- Plan the smallest version the client would actually use, and have the client try it. A pair or trio means agreeing on a repo, branches, and who owns what.

## Artifact 5: Game Reference Tool (due Dec 13; the moonshot)
**Idea:** a fast, no-bloat reference for the games Kevin and his friends play: **League of Legends** (champions and items: base stats, ability text, item stats and effects), then **Valorant** (agents, weapons, skins, maybe a model viewer), then **Overwatch** (heroes, perks, player lookup, win/loss by hero and mode). A 3x3 grid of picks that "represent" the user for each game. Information only. No lore, no ads, no wiki sprawl.

This started as Artifact 2 and was moved here because three games is far larger than 8 to 12 hours. A scoped plan was written when it was Artifact 2 (League only, phase 1). With about five weeks, the scope can grow. Read the Artifact 5 page for what it requires (the overview says it may be deployed to real users).

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

## Ideas considered and not chosen (in case plans change)
- Weekly dev summary: reads git history across local repos and writes a markdown report. A plain script can only collect and format; real prose summaries need an AI call (Artifact 3 territory).
- Duplicate and clutter finder with a dry-run mode (compare size, then partial hash, then full hash, and measure speedup).
- Card price watcher for a Pokémon wishlist (Pokémon TCG API, Discord webhook alert).
- Riot match logger or a rate-limit-friendly API client with a cache (uses a development key; keep it out of the repo).
- Project launcher, repo health check, site uptime logger, incremental backup tool, spaced-repetition flashcards, fast note search, Pokémon team type checker, Discord bot for a friends server.
- Free-tier hosting questions (Firebase, Vercel limits) were raised in another chat AI's answer. Those numbers were not verified here. Check the current docs before relying on them.
