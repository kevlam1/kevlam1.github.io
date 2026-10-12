# CLAUDE.md: Kevin Lam's TCSS 490 portfolio

Read this file first. Longer background is in `docs/` (index at the bottom). Keep this file under 200 lines and move anything long into `docs/`.

## What this project is
- Public portfolio at https://kevlam1.github.io. Repo: `kevlam1/kevlam1.github.io`. GitHub Pages serves `main` from the root.
- It is Artifact 1 of TCSS 490 (Generative AI and Software Development, UW Tacoma, Autumn 2026). Every later artifact is handed in by filling in its card here and submitting this same link on Canvas.
- Plain HTML, CSS, and JavaScript. No framework, no build step, no package.json. Keep it that way.
- Owner: Kevin Lam, senior in Computer Science and Systems. Windows, IntelliJ IDEA Ultimate.

## Files
- `index.html`: the whole portfolio. All CSS is in one `<style>`; scripts are IIFE blocks at the bottom.
- `log.html`: the build-log page. It fetches `log.md` in the browser and renders it.
- `log.md`: the build log text. Single source of truth, written in Kevin's first-person voice.
- `images/`: card images (`artifact-1.jpg` to `artifact-5.jpg`, `side-project-1.jpg`, `side-project-2.jpg`).
- `docs/`: background notes carried over from the web-chat sessions. Everything in it is public except `docs/PROJECT_CONTEXT.md`, which is gitignored and exists only on Kevin's machine.
- `CLAUDE.local.md`: Kevin's private notes for this project. Gitignored.
- Site files (`log.md`, `log.html`, `images/`) are lowercase because GitHub Pages is case-sensitive. Keep new site files lowercase.

## Run and check
- No install, no build. From the project folder run `python -m http.server 8000`, then open http://localhost:8000.
- It does not live-reload. Refresh after saving.
- Phone testing: same Wi-Fi, cellular off, use the computer's IPv4 address from `ipconfig`, never `localhost`. Windows Firewall may need to allow Python on Private networks.
- There are no automated tests. Verification means looking at it. After every change check desktop width and phone width, keep the DevTools console open (no red errors), and emulate `prefers-reduced-motion`.
- Always say what you checked and what you could not check.
- A push to `main` deploys, with up to roughly 10 minutes of delay. Do not commit or push unless Kevin asks.

## Hard rules
- No frameworks, bundlers, Tailwind, or npm dependencies. Outside scripts only from jsDelivr, pinned to a version (`lenis@1`, `marked@12` today). Google Fonts serves DM Sans.
- Keep Kevin's wording. Never rewrite his About text, card reflections, or log entries to say something that did not happen.
- This repo is public. No keys, tokens, emails, phone numbers, or IP addresses in any file, including `docs/`.
- The LinkedIn icon is commented out in the footer until Kevin has a real profile URL. Do not restore the generic link.
- Every animation must respect `prefers-reduced-motion`.
- One definition per CSS rule. Replace blocks wholesale instead of appending near the old copy, and never put CSS inside `<script>` or script inside `<style>`.
- Every inline SVG needs `width`, `height`, and `fill` set directly. An unsized SVG renders huge and black.
- Do not copy third-party code with unclear licenses. Shadertoy code is covered by a restrictive default license. React Bits components are React, so port the idea to plain JS.
- Do not rename or delete files without asking. Do not push, force-push, or rewrite history.

## How to work with Kevin
- Start from a clean `git status`. If it is not clean, say so before editing.
- Explain before building when something is new to him (hosting was). Ask for an explanation of a file before changing it.
- Explain what a shell command does before running it.
- If a request can be read two ways, say how you read it before building. The card layout was misread three times.
- Be exact about placement: name the file and the block you changed. Do not change your approach in the middle of a reply.
- Keep scope small. If a request is much bigger than the time he has, say so and propose a smaller first version.
- Check claims against real files or real output. Say what is verified and what is not. When you are unsure, say so instead of guessing.
- When you made a mistake, say so plainly and fix it.
- More preferences are in `../CLAUDE.md` (the `TCSS 490` folder, shared by every artifact repo, not in git) and in `docs/PROJECT_CONTEXT.md` (local only).

## The log protocol
- Kevin keeps `log.md` as the course-required record of what he planned, asked for, decided, and abandoned. After a meaningful change, add to the log directly, in his first-person voice and matching the existing entries, and mention it in your summary so he can review it in the diff.
- Structure: `# title`, tool lines, then `## What I set out to build` (a plain always-open card), then numbered `## N. Title` sections (shown under "The build"), then the unnumbered reflection sections.
- Use bold labels (`**What I asked for**`, `**What changed**`, `**Decisions**`). Never add scratch headings or loose bullets at the bottom, because every `##` becomes a box and a menu entry on the log page.
- Update "Not yet verified" and "Still to do" when their state changes. Record where an AI got something wrong, including you.
- Do not claim you tested something you did not.

## Site conventions (details in `docs/SITE_GUIDE.md`)
- Sections: `#intro`, `#about`, `#artifacts` (5 cards), `#side-projects` (Cardex, PokéGuess), `footer#connect`.
- Card anatomy: `.card-entrance` wrapper (slide-in) around `article.card.live` or `article.card.locked`, containing `.media` and `.card-body`.
- Unlock a card when its artifact is finished: change `card locked` to `card live`, change the status pill to `status live` with the text "Live", replace the description and toolkit pills, add a link, replace the image and alt text, then log it. No JavaScript changes are needed.
- Color tokens are CSS variables in `:root` (`--bg #0f172a`, `--panel #1e293b`, `--line #334155`, `--text #e2e8f0`, `--muted #94a3b8`, `--accent #ffffff`). Font is DM Sans with Arial as the fallback, on both pages. Theme is navy with white accents and a grain overlay.
- Tunable effect settings are constants at the top of each script. They are listed in `docs/SITE_GUIDE.md`.

## Known pitfalls (full list in `docs/LESSONS_LEARNED.md`)
- Backdrop blur over the animated WebGL background is expensive. The background is capped at about 30fps for that reason.
- Animate the `.card-entrance` wrapper, not `.card`, or the entrance overwrites the tilt transform.
- `scroll-behavior: smooth` does not smooth wheel scrolling. Lenis does, and it must be stopped while the card popup is open.
- The navy strip at the bottom of a phone is the browser's toolbar collapsing, not a bug in the site.
- IntelliJ shows some false warnings (CSS variables set by JavaScript, classes created by scripts). Tell Kevin which warnings are harmless.
- Renames that only change letter case can be missed by git on Windows. Verify `log.md` is lowercase on GitHub.

## Open work
See `docs/TODO.md`. Artifact plans and ideas are in `docs/ARTIFACT_PLANS.md`.

## docs/ index
- `PROJECT_CONTEXT.md` (local only, gitignored): the course, deadlines, grading, what is verified and what is not, history
- `SITE_GUIDE.md`: how `index.html`, `log.html`, and `log.md` are built, with every tunable setting
- `LESSONS_LEARNED.md`: mistakes and fixes so they are not repeated
- `ARTIFACT_PLANS.md`: ideas and scoped plans for Artifacts 2 to 5
- `TODO.md`: open items
