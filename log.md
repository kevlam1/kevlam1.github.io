# Build log: Artifact 1 (Portfolio)

**Chat AIs:** Claude (main), ChatGPT (a few sessions when I hit Claude's limit), Gemini (brainstorming only) | **Editor:** IntelliJ IDEA Ultimate | **Host:** GitHub Pages (`kevlam1.github.io`)
**Stack:** plain HTML, CSS, and JavaScript with no build step: `index.html` for the portfolio, `log.html` for this log page, and `log.md` for the log text. Lenis (smooth scrolling) and marked (Markdown rendering) load from a CDN.

---

## What I set out to build

A small front-end portfolio with a card for each of the five course artifacts. Only card 1 is real (it is this site). Cards 2-5 hold placeholder ideas until I finish those artifacts. The site is also how I hand in every artifact, so it has to stay at one stable link all quarter. Over time I will add more elements to it, such as UX and UI, to make sure this is the best work I would be satisfied with.

---

## 1. Planning and hosting

**Date:** 2026-10-06
**Summary:** Learned to host on GitHub Pages and got the repo live before building anything else.

**What I asked for**
- Read the assignment and the course's artifact overview, then asked Claude for a plan.
- Said I did not know how to host a site on GitHub Pages, so we stopped and learned that first.

**What changed**
- Created the public repo `kevlam1.github.io` with a README so a `main` branch existed.
- Added a test `index.html` and turned on Pages from `main` / root. The "Hello" page loaded at `kevlam1.github.io` in a private window.
- Cloned the repo into IntelliJ and started this log.

**Decisions**
- Plain HTML/CSS/JS, no framework. The course deploy guide covers Next.js and Vercel, but a plain site needs no build step.
- Repo named after my username so the link never changes.
- Public repo, since a Pages site is public anyway.

---

## 2. First build and look

**Date:** 2026-10-06
**Summary:** Built the first version of the layout, the staggered load animation, and the navy color theme.

**What I asked for**
- Showed Claude a reference portfolio (dark background, lime accent, big headline, section nav) and said I liked its layout, colors, and animation.
- Asked for: no photo of me, centered text, Georgia serif, and a load animation where each row of text fades in from below, one after another.
- Asked for a grain texture, then for the green to be replaced with #0f172a and its variants.

**What changed**
- Claude wrote a first version with five placeholder cards and the staggered fade-in on the intro.
- Added grain: an SVG noise image tiled over the page and over each card, with a strength setting I can adjust.
- Recolored to a navy theme. #0f172a would have been nearly invisible as an accent on a dark page, so it became the base background and lighter shades handle text, borders, and accents. The accent is now pure white.

---

## 3. Interactive effects

**Date:** 2026-10-06
**Summary:** Added card tilt, cursor spotlight, and the sliding nav highlight, ported from React tutorials to plain JavaScript.

**What I asked for**
- A tilt effect on the Artifact 1 card that also grows it a few pixels on hover.
- A spotlight glow that follows the cursor inside that card.
- An animated sliding highlight on the top nav bar.
- I gave Claude reference tutorials, which were written for React. Claude translated them to plain JavaScript and CSS.

**What changed**
- Cards tilt toward the cursor (up to 5 degrees, scaled to the card's size), grow 16px in width, and show a soft spotlight that follows the mouse. This now applies to every active ("live") card: Artifact 1 and both side projects.
- The nav is a pill-shaped bar with a highlight that slides to the clicked link. I also made it follow whichever section is on screen as I scroll, which goes a step beyond the tutorial.
- Fixed a bug where the highlight twitched after clicking a tab. Scroll tracking now pauses while the page scrolls to the clicked section.
- All motion effects switch off for visitors whose system is set to reduce motion.

**Decisions**
- Locked cards (Artifacts 2-5) get no hover effects until I finish them.
- No Tailwind. Its in-browser version is meant for development, and plain CSS kept things simple.

---

## 4. Content and sections

**Date:** 2026-10-06
**Summary:** Wrote my real About text and intro, and added the footer links, nav tabs, side projects, and toolkit pills.

**What changed**
- Wrote my About section from my own details (Computer Science and Systems senior at UW Tacoma, likes building usable tools and optimization, learning to bring AI into my workflow).
- Rewrote the intro: headline "Building with AI. Learning by making. One artifact at a time." and subtitle "Building optimized systems."
- Added GitHub and LinkedIn icon links to the footer. Later I hid the LinkedIn icon for now, since it only linked to the generic LinkedIn home page.
- Added more tabs to the top bar: Intro, About, Artifacts, Side Projects, Connect. Renamed "Work" to "Artifacts".
- Added a Side Projects section with Cardex and PokéGuess, both live. Descriptions come from their READMEs, and the PokéGuess reflection is adapted from my LinkedIn post.
- Added toolkit pills to the active cards to show the tools used. For the side projects I used their READMEs as the source. Artifact 1's pills are HTML, CSS, JavaScript, WebGL, GitHub Pages, and Claude.
- Drafted my Artifact 1 reflection with Claude's help and edited it to match what happened. Later I added a few lines about moving to ChatGPT and Gemini when I hit Claude's limits, since the assignment says switching is worth a line in the reflection.
- Added placeholder images to the non-active artifact cards to show they are coming soon.

---

## 5. Visual polish

**Date:** 2026-10-06
**Summary:** Added section dividers, card shadows, the underline link animation, and the animated WebGL background.

**What I asked for**
- Lines between the sections, a drop shadow under each card, an animated underline on the Artifact 1 link, and an animated background so the site is not bland.

**What changed**
- Dividers: one thin line that fades out at both ends, with a soft glow. Added a matching line above the footer.
- Soft drop shadows under every card, deeper on active cards while hovered.
- Artifact 1 link: the text lifts slightly and a thick line sweeps out from the center.
- Background: a slow-moving navy wave pattern drawn by a small WebGL shader. I liked the look of Balatro's background, but it was much busier than I wanted, so Claude wrote an original shader instead of copying it.
- I asked for it to be busier and to swirl around the center like the original. Claude zoomed the pattern out, added a coordinate warp and a ripple layer, and added a twist around the screen center, with `ZOOM`, `SWIRL`, and `SPIN` settings I can tune.
- It pauses when the tab is hidden, shows a still frame when reduced motion is on, and falls back to plain navy if WebGL is unavailable.

---

## 6. Card layout and entrance

**Date:** 2026-10-07
**Summary:** Redesigned cards into a wider image-left layout and added the slide-in entrance animation.

**What I asked for**
- More rectangular cards with an image slot for a picture of each artifact, and a reorganized text layout.
- Every card should reserve space for two rows of pills and three lines of description so the rows match across.
- Cards that slide in from the side when the page opens.

**What changed**
- Each card has an image slot on the left. The text on the right is ordered: label (artifact number and due date) with a status pill, title, description, toolkit pills, link.
- Cards are two per row on wide screens, one per row on tablets, and the image moves on top on phones. I widened the card area and gave placeholder cards a "Toolkit: TBA" pill so the rows line up.
- **Entrance animation:** I hit Claude's limit, so I tried this with ChatGPT. It took about 20 minutes of back and forth before it worked. The working version animates a wrapper around each card so the slide-in does not overwrite the tilt.
- Claude later pointed out that the cards finished sliding in on page load, before anyone scrolled down to them. I changed it so each card slides in when it scrolls into view.

---

## 7. Card popup and locked cards

**Date:** 2026-10-07
**Summary:** Added the full-card popup for reflections and made locked cards (Artifacts 2-5) unclickable until finished.

**What I asked for**
- When I pasted in my long reflection, the card looked comically large. I asked for every card to show everything except the reflection, and for a click to fade in a full card from the center of the screen over a blurred background, with the reflection included.
- Artifacts 2-5 should not be clickable until I finish them.

**What changed**
- Clicking a card opens a larger copy of it in a native `<dialog>` with a blurred, dimmed backdrop and a fade-and-scale-in. It closes with the × button, a click outside the card, or Esc.
- Clicking the link inside a card still follows the link instead of opening the popup.
- Cards can also be opened from the keyboard (Tab to focus, Enter or Space to open).
- Locked cards are dimmed, have a normal cursor, and skip the popup and the keyboard focus. To unlock a card I switch its class from `locked` to `live`.

---

## 8. Click stars

**Date:** 2026-10-07
**Summary:** Added a burst of four-pointed stars wherever I click or tap.

**What I asked for**
- Four-pointed stars around my cursor. Then, since a constant effect would get annoying, a burst of stars wherever I click, like a mobile game.

**What changed**
- The first version had four stars constantly orbiting the cursor. I switched it to a burst on each click or tap.
- The stars move into the card popup while it is open, so the popup does not hide them.
- Made the stars brighter (white with a stronger glow) and shortened how long they last.
- All of it is off for visitors who prefer reduced motion.

---

## 9. Gradual blur and smooth scrolling

**Date:** 2026-10-07
**Summary:** Built a gradual blur at the page bottom, fixed scroll performance, and added Lenis smooth scrolling.

**First attempt (ChatGPT, after hitting Claude's limit)**
- Tried adding a gradual blur effect to the bottom of the page.
- The first version used CSS custom properties for the blur values, and my editor flagged them as unresolved.
- After fixing the errors, the effect looked more like a fade or mosaic than a smooth blur.
- I explained several times that `-webkit-` properties were producing red errors in my editor, but they kept appearing in the suggested code.
- It also kept changing the implementation instead of building on the code I had already given it, which made this more frustrating and slower than it needed to be.
- I eventually removed the unresolved variables and `-webkit-` properties and simplified the code.

**Rebuilding it with Claude**
- Once my Claude limit reset, it fixed the problems and got close to what I pictured.
- I tried the React Bits Gradual Blur effect. At first it looked off, with visible seams and a muddy dark tint.
- Claude could not pull the component's source because React Bits renders in the browser. The component is React-only, so it had to be ported to plain JavaScript for my site anyway.
- Cause of the seams: each blur layer was a hard-edged band with no mask. Claude rebuilt it so each layer has its own soft gradient mask and the blur builds up toward the bottom edge.
- Compared with the React Bits demo, mine was less gradual and stretched images. Retuned to 8 layers over a taller band, with a lower peak blur that ramps up on a curve.

**Scroll performance**
- The scroll felt heavy. Backdrop blur over an animated WebGL background gets re-rendered every frame, which is expensive.
- Fixes: capped the background at about 30fps, removed a blur on the header that did nothing because its background was opaque, and throttled the nav's scroll handler to once per frame.

**Smooth scrolling**
- Learned that `scroll-behavior: smooth` only smooths anchor jumps, not normal scrolling.
- Added Lenis for smooth wheel scrolling, routed the nav tabs through it, and paused it while the card popup is open.

**Keeping the footer readable**
- Made the blur fade out over the last 250px of scroll so the footer stays readable. It is hidden once fully faded, so it stops rendering too.
- The fade is applied to each layer, because opacity on the parent would have stopped the layers from seeing the page behind them.

---

## 10. Planning Artifacts 2-5

**Date:** 2026-10-07
**Summary:** Researched Artifact 2's requirements and drafted placeholder ideas for Artifacts 2-5.

**What I did**
- Read the Artifact 2 spec on the course site. It does not have to be a web app or be deployed, a repo link works for the card, and it is my first build with Claude Code.
- While my Claude session was locked, I brainstormed with Gemini. It explained AI image parsing as if Claude Code lived inside the finished app. I questioned it, and it admitted it had blurred the line between the tool that builds the software and the AI the finished app might call.
- Back in Claude, I brainstormed more ideas.

**What I learned**
- Riot API: a development key is for testing and personal use, a public product needs a production key, and the key must stay out of a public repo.
- Data Dragon and Community Dragon cover champion and item data but are documented as inaccurate in places.
- Chat Claude can fetch some web pages, but its sandbox has no network. Claude Code runs on my machine and can inspect real API responses.
- Plan: ask Claude Code to show raw data before trusting it, and put key decisions in `CLAUDE.md`.

**Current placeholder ideas (I will not be held to them)**
- **Artifact 2, MIDI Visualizer:** a browser-based MIDI player and Synthesia-style visualizer that loads MIDI files, shows notes falling in real time, and lets me play along on a connected piano keyboard.
- **Artifact 3, README.md Architect:** a Claude Code skill that analyzes a project's codebase and generates a README from its real structure, technologies, and functionality.
- **Artifact 4, Service Booking Tool:** a booking system for a service provider to manage availability, appointments, and customer requests.
- **Artifact 5, Game Reference Tool:** a fast, no-bloat reference for League of Legends, then Valorant and Overwatch.
- The game reference tool started as my Artifact 2 idea. I wrote a scoped plan for it (`PLAN.md`), and it is now the Artifact 5 idea.

---

## 11. Reviews and fixes

**Date:** 2026-10-07
**Summary:** Fixed editor warnings and bugs Claude found on review, then pushed the first full version live.

**Editor warnings**
- IntelliJ flagged a few CSS warnings (`--mx` and `--my` unresolved, `.gradual-blur-layer` never used, `--fade` unresolved). All were false alarms because JavaScript creates those layers and sets those values at runtime. I added default values to quiet some of them.
- 17 editor errors came from a block of CSS I had pasted inside a script tag. I removed the duplicate.

**Claude's reviews of the file**
- Claude reviewed the whole file more than once and found: a deleted spotlight rule, a nav tab that could not become active by scrolling, leftover colors from the old theme, a missing footer rule, placeholder image paths with no files behind them, and a Cardex link that pointed to my own portfolio. I fixed each.
- Fixed a typo in the Artifacts intro ("build" to "building").

**Going live**
- Pushed the first full version of the site to `main` for a live check, then pushed later changes as I went.

---

## 12. The log page

**Date:** 2026-10-08
**Summary:** Built log.html to render this log.md file, with its own header, menu, and animations.

**What I asked for**
- A page on the site that shows this `log.md`, so the Markdown file stays the single source and I only edit the text in one place.
- A header that matches the main page (same bar color and pill buttons), and a background that fits the main page's theme.
- "What I set out to build" as a plain box instead of a collapsible one, and no menu entry that just scrolls back to the top.
- Reflection boxes separated from the build boxes, with the same dividers as the main page.
- The sidebar menu to drop down when the page opens, and the boxes to slide in on scroll like the cards on the main page.
- A slower, smoother menu drop-down, with Reflection expanded too.
- The boxes to open smoothly instead of popping open.
- The main text centered on the page, with the menu more to the left.
- Something to cover the brief jank while the log renders.
- This `.md` reorganized so it reads in order on the site, with my newer notes folded in.

**What changed: the page and its content**
- Added `log.html`, which loads `log.md` in the browser, renders it with the marked library, and turns each `##` heading into a collapsible box with checklists shown. The footer on the main page links to it.
- "What I set out to build" is now an always-open box and is left out of the menu.
- The boxes are grouped under centered "The build" and "Reflection" headings, separated by the same glowing divider as the main page. "Still to do" stays inside Reflection for now.
- Renamed `LOG.md` to `log.md` so every file name is lowercase, and pointed the footer link at `log.html` to match.
- Reorganized `log.md`: regrouped the sections, made the labels consistent, folded the notes I had parked at the bottom into the numbered sections, and turned finished to-dos into checked items.

**What changed: the contents menu**
- Added a branched contents menu, a plain JavaScript port of a React Bits component. It groups the sections, follows my scroll position, and jumps to a section on click.
- Sidebar drop-down: the rail and group titles fade in one after another, then both groups unfold with each item fading into place. The first version seemed choppy, so I gave Claude more specific instructions. It switched to a gentler ease-in-out curve, slowed the unfold to about a second, and staggered the items, which worked well.

**What changed: motion**
- Boxes slide in from the left as they scroll into view, like the cards on the main page. They trigger when a box's top edge enters the screen, so tall boxes still show up.
- Boxes now open and close smoothly instead of popping. The height, padding, and fade animate together, and it also applies to Expand all, Collapse all, and clicks from the contents menu. It is instant for visitors who prefer reduced motion.
- Loading animation: a glowing star spinning inside dashed rings, using the same star as the click effect, to cover the brief jank when the log renders. It holds the page height open so the footer does not jump, stays up for at least a second so it does not flash, and fades out before the page builds.

**What changed: look and layout**
- Header: same dark bar as the main page, with a pill-shaped container and a highlight that slides to whichever button I hover.
- Background: Claude ported the React Bits Gradient Waves component, which is written in React with the OGL library, to plain WebGL2. Claude recolored it to my navy palette and made it quieter. It renders at half resolution and is capped at about 30fps to keep scrolling smooth.
- On wide screens (1360px and up) the log text is centered on the page and the contents menu sits at the left edge. Narrower windows keep the menu beside the text, because there is not room to do both.

**Decisions**
- Keep `log.md` as the only copy of the text. The page renders it live instead of duplicating it.
- Lowercase file names everywhere (`log.md`, `log.html`), since GitHub Pages is case-sensitive.
- Port components to plain JavaScript instead of adding React or OGL to a site that has no build step.
- Dropped the wave component's mouse parallax and its built-in grain. The page already has a grain overlay, and the background should stay quiet behind the text.
- All the log page's motion switches off for visitors who prefer reduced motion.

---

## 13. Mobile fixes and phone testing

**Date:** 2026-10-08
**Summary:** Tested the site on my phone and fixed the card popup, image sizing, and rotation bugs it turned up.

**What I found on my phone**
- The card popup opened already scrolled down to the reflection.
- In the popup, the text sat above the image and the card lost its grain.
- The card images were too tall.
- After rotating the phone, the card image stayed large when I rotated back.
- A navy strip showed at the bottom of the screen.

**What changed: card popup**
- The popup scrolled down because the browser auto-focused the "Visit…" link. The × button now gets focus instead, and the scroll resets to the top.
- The content now sits in an inner scroller, so the card's grain layer stays put and the image stays above the text. The × button stays pinned while I scroll.

**What changed: cards**
- Cut the image height by about 25% (aspect ratio `2.4 / 1`).
- Fixed the rotation bug. The image's natural size was feeding back into its container, so it is now positioned absolutely inside a fixed-ratio box.
- Phones now show two columns in both portrait and landscape, with the card text and pills shrunk to fit.
- Matched the line heights across cards on mobile so the rows line up.

**What changed: the navy strip at the bottom**
- Tried `lvh` sizing, then oversizing the background layers. Neither worked, so I removed the second attempt.
- It turned out not to be my code. The same strip shows on google.com, because it is the browser's toolbar collapsing.
- Left a couple of harmless leftovers (`clientWidth` / `clientHeight` in the WebGL `resize()`, and `OVERSHOOT = 120`).

**What I learned: testing on a phone**
- `localhost` on a phone means the phone itself, so I need my computer's IP address (`ipconfig`, then the IPv4 address).
- The phone has to be on the same Wi-Fi network, with cellular off.
- IntelliJ's built-in server (port 63342) had "Can accept external connections" grayed out, so I used `python -m http.server 8000` in the project folder instead.
- That Python server only serves files. It does not add or change anything in the project, and it does not live-reload, so I refresh the phone after saving.
- Windows Firewall may need to allow Python on Private networks.

**What I learned: debugging**
- Mobile browsers behave differently from desktop. Fixes for scrolling, fixed layers, and focus often need a real phone to check.
- A layout bug can come from an image's natural size feeding back into its container, which was the rotation bug.
- Not every oddity is my code, like the browser's toolbar causing the navy strip.
- Some of the fixes were guesses that did not work (`lvh`, oversizing). Testing and reporting back exactly what I saw is what narrowed things down.

---

## 14. Footer link, progress bar, and font

**Date:** 2026-10-11
**Summary:** Polished the footer link, added a favicon and link preview, added a scroll progress bar, and switched the font to DM Sans.

**What changed: footer link**
- Gave the footer link to the log page a slowly drifting blue-to-white gradient with a soft glow that brightens on hover.
- Added a small spinning white star on each side of the link, the same star and glow as the log page's loader. It stops spinning for visitors who prefer reduced motion.
- Added a small, faint "build log" caption under the link, so it's clear where `/log.html` goes.

**What changed: favicon**
- Added a favicon to both pages: the site's four-pointed star, turned so its points reach the corners. It's navy on light browser tabs and white on dark ones.
- Moved the favicon into `images/` with the rest of the images, so nothing image-related sits in the root.

**What changed: link preview**
- Made a 1200x630 preview image of the homepage and added Open Graph tags to both pages, so a pasted link shows a title, description, and image instead of a bare URL.

**What changed: cleanup**
- Removed a duplicate copy of the scroll progress bar's CSS rule. Both copies were the same, so nothing looks different.
- Stopped loading the Instrument Serif font. Nothing used it since the switch to DM Sans, so every visitor was downloading it for nothing.

**What changed: scroll progress bar**
- Added a smooth scroll progress bar under the header (a thin blue-to-white glowing line with a bright tip) that glides along with the page scroll.
- Replaced the progress bar’s tip with the same four-pointed star used by the loader and click effect. It spins with scroll position, so it costs nothing when idle.
- The first version of the progress bar’s star showed up huge and black because its CSS wasn’t applied. I replaced the whole progress bar CSS block at once and set the star’s size directly on the SVG.
- Fixed the progress bar's star. Asked Claude to have it spin too.
- Added the same progress bar to the log page. Since opening or closing a box changes how long the page is, the bar re-measures whenever the page's height changes and glides back or forward to match.

**What changed: font**
- Asked for suggestions on different fonts, decided to use "DM Sans", with "Arial" as backup.

**What I checked**
- After pushing, checked the live site and the log page on my phone. Everything worked: the nav with five tabs, the background, the gradual blur and scrolling, the footer stars and caption, and the log page with its new progress bar.

---

## 15. Moving to Claude Code

**Date:** 2026-10-11
**Summary:** Moved the project to Claude Code with a `CLAUDE.md` and `docs/` folder so the agent has persistent project context.

**What I asked for**
- Had the web chat write up everything it knew about the project into a handoff folder, then asked Claude Code to read it and flag anything that conflicted before changing files.
- Asked for the pros and cons of making `CLAUDE.md` and `docs/` public, based on what the course asks for.

**What changed**
- Added `CLAUDE.md` at the repo root. It holds the project's rules, how to run and check the site, and how to keep this log.
- Added `docs/` with the site guide, lessons learned, artifact plans, and to-do list.
- Asked Claude Code to replace my two-line `README.md` with a proper one: what the site is, its features, the tech, the folder layout, how to run it locally, and credits for the ported components.
- Fixed `.gitignore`. Its lines had leading spaces, so `.idea/` was never actually ignored.
- Claude Code checked the handoff notes against the real files and found a few that were out of date: they still said the font was Georgia, and that the progress bar's star spins with scroll position (it spins on a constant loop).

**Decisions**
- `CLAUDE.md` is public, since the course guide says the project copy lives at the repo root and is committed. It also shows how I direct the agent.
- `docs/PROJECT_CONTEXT.md` stays on my machine only. It has my grading and deadline notes, which don't belong on a public site. The rest of `docs/` is public.
- Private notes go in `CLAUDE.local.md`, which is gitignored.
- My general working preferences live in a `CLAUDE.md` in my `TCSS 490` folder, one level above this repo, so every artifact repo I create inside it loads them. It stays out of git.
- Claude Code adds new entries to this log in my voice, and I review them in the diff. It doesn't rewrite past entries without asking.

---

## 16. Unlocking the Artifact 2 card

**Date:** 2026-10-14
**Summary:** Pointed Claude Code at the finished `midi-companion` repo and unlocked its card on this portfolio.

**What I asked for**
- Told Claude Code to go check the `midi-companion` repo (a sibling folder, since it's deployed to Vercel) and update Artifact 2's card to match, since the site is live now instead of in progress.

**What changed**
- Claude Code read `midi-companion`'s README and confirmed the live link (`midi-companion.vercel.app`) actually loads before using it.
- Card switched from `locked`/"In progress" to `live`/"Live", with the real link added and the toolkit pills replaced with the actual stack (TypeScript, Vite, Canvas 2D, Tone.js, Vercel, Claude Code), pulled from the README instead of guessed.
- The description was rewritten from the README's own wording.

**Left for me to finish**
- The reflection paragraph still says "Link and reflection coming soon." Claude Code would not write this in my voice, so I still need to write it myself, same as Artifact 1's.
- The card image is still the Oct 7 placeholder. I need to drop in a real screenshot.
- The card title still reads "MIDI Visualizer," while the repo and site call it "MIDI Companion." I haven't decided whether to rename it on the card yet.

---

## Where AI misread me, or I had to correct course

**Claude**
- **Jumped ahead:** built a three-theme comparison page before I understood GitHub Pages hosting. I said we were jumping the gun, so we stopped and learned hosting first.
- **Accent color:** using #0f172a as the accent would have made links and buttons nearly invisible, so it became the background color.
- **Card layout took three tries:** I asked for "two columns inside one, stacked." Claude read that as one narrower column, then gave me two cards per row with the image on top. I meant wide rectangles (image left, text right), two per row. I learned to describe the layout precisely.
- **Background shader:** the first version was too zoomed in, and it drifted in every direction. The original I liked spirals around the center, so Claude added zoom and swirl controls.
- **Pages it could not open:** it could not read the css reference pages or some course guides, so I had to paste or describe what I wanted.
- **Checking sources:** I asked Claude to double-check sources. It checked the assignment against the course site and the hosting steps against GitHub's docs, and it flagged what it could not verify instead of guessing.
- **Log page menu:** the first version of the log page listed "What I set out to build" in the Reflection part of the menu, so clicking it just scrolled back to the top. I asked for it to be a plain box and removed it from the menu.
- **Mobile fixes that did not work:** the `lvh` sizing and the oversized background layers did not fix the navy strip, which turned out to be the browser's own toolbar.

**ChatGPT**
- Twice (the card entrance and the first blur), it wrote code and then reversed itself in the same message, and ignored my instruction to stop. I found Claude clearer about exactly which part of the code to change.

**Gemini**
- Blurred the difference between the AI that builds the software and an AI called by the finished app. I questioned it, and then checked the real requirements on the course site.

**My own mistakes**
- Asked about naming the repo `kevlam.github.io`. It has to match my username, so it is `kevlam1.github.io`.
- Opened my account-level Pages settings instead of the repo's own Pages settings.
- Copied code fences (three backticks) from the chat into my HTML file.
- Described a change wrong: I asked for no tilt on cards 2-5 but meant not clickable.
- Pasted the blur fade code outside the script's wrapper, so it would have thrown an error. Pasted the Lenis CSS inside the `html{}` rule, where it would not apply. Moved both.

---

## Decisions and abandoned ideas

- Considered Tailwind or a framework. Chose plain HTML, CSS, and JavaScript.
- Considered making the repo private. Pages on a free account needs a public repo, and the site is public anyway.
- Started with a two-line divider and cut it down to one line.
- Dropped the idea of copying css shader code.
- Dropped a photo of myself from the intro.
- Dropped the constant orbiting stars in favor of click bursts.
- Dropped the blur on the header, since it did nothing.
- Not putting the whole game reference tool into Artifact 2, since three games is far more than the 8-12 hour scope.
- Log page: made "What I set out to build" a plain box instead of a collapsible one.
- Log page: dropped the wave background's mouse parallax and built-in grain.
- Log page: kept "Still to do" inside Reflection instead of giving it its own group. It is a one-line change if I want to split it out later.
- Mobile: removed the `lvh` and oversized-background attempts once I found the navy strip was the browser's toolbar.
- Removed the "Still to do" section from this log. Open items are tracked in `docs/TODO.md` instead, and this log only records what happened.

---

## Not yet verified

- Whether the blur and scrolling feel good on a slower computer, and whether the log page's wave background, loading animation, and menu animation run smoothly on one.
- Whether the Lenis script loads reliably from the CDN, and that nothing breaks without it.
- How the link preview looks when the site is shared on different platforms.
