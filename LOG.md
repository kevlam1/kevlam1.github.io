# Build log: Artifact 1 (Portfolio)

**Chat AI:** Claude (free web chat) | **Editor:** IntelliJ IDEA Ultimate | **Host:** GitHub Pages (`kevlam1.github.io`)
**Stack:** plain HTML, CSS, and JavaScript in a single `index.html`, no build step

## What I set out to build

A small front-end portfolio with a card for each of the five course artifacts. Only card 1 is real (it is this site). Cards 2-5 hold placeholders until I finish those artifacts. The site is also how I hand in every artifact, so it has to stay at one stable link all quarter.

---

## 1. Planning and hosting

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

**What I asked for**
- Showed Claude a reference portfolio (dark background, lime accent, big headline, section nav) and said I liked its layout, colors, and animation.
- Asked for: no photo of me, centered text, Georgia serif, and a load animation where each row of text fades in from below, one after another.
- Asked for a grain texture, then for the green to be replaced with #0f172a and its variants.

**What changed**
- Claude wrote a first version with five placeholder cards and the staggered fade-in on the intro.
- Added grain: an SVG noise image tiled over the page and over each card, with a strength setting I can adjust.
- Recolored to a navy theme. #0f172a would have been nearly invisible as an accent on a dark page, so it became the base background and lighter slate shades handle text, borders, and accents.

---

## 3. Interactive effects

**What I asked for**
- A tilt effect on the Artifact 1 card that also grows it a few pixels on hover.
- A spotlight glow that follows the cursor inside that card.
- An animated sliding highlight on the top nav bar.
- I gave Claude reference tutorials, which were written for React. Claude translated them to plain JavaScript and CSS.

**What changed**
- Card 1 tilts toward the cursor (up to 5 degrees, scaled to the card's size), grows 16px in width, and shows a soft spotlight that follows the mouse.
- The nav is a pill-shaped bar with a highlight that slides to the clicked link. I also made it follow whichever section is on screen as I scroll, which goes a step beyond the tutorial.
- All motion effects switch off for visitors whose system is set to reduce motion.

**Decisions**
- Only card 1 gets the hover effects for now. I will extend them to other cards as I finish those artifacts.
- No Tailwind. Its in-browser version is meant for development, and plain CSS kept things simple.

---

## 4. Content and sections

**What changed**
- Wrote my About section from my own details (Computer Science and Systems senior at UW Tacoma, likes building usable tools and optimization, learning to bring AI into my workflow).
- Added GitHub and LinkedIn icon links to the footer.
- Added more tabs to the top bar: Intro, About, Artifacts, Side Projects, Connect. Renamed "Work" to "Artifacts".
- Added a Side Projects section for things I build outside class.
- Drafted my Artifact 1 reflection with Claude's help and edited it to match what happened.

---

## 5. Visual polish

**What I asked for**
- Lines between the sections, a drop shadow under each card, an animated underline on the Artifact 1 link, and an animated background so the site is not bland.

**What changed**
- Dividers: one thin line that fades out at both ends, with a soft glow. Added a matching line above the footer.
- Soft drop shadows under every card, deeper on card 1 while hovered.
- Artifact 1 link: the text lifts slightly and a thick line sweeps out from the center.
- Background: a slow-moving navy wave pattern drawn by a small WebGL shader. I liked the look of Balatro's background shader, but it was much busier than I wanted, and Shadertoy code is licensed by default in ways that limit reuse and I could not check this one's terms. So Claude wrote an original shader instead of porting it.
- I asked for it to be busier and to swirl around the center like the original. Claude zoomed the pattern out, added a coordinate warp and a ripple layer, and added a twist around the screen center, with `ZOOM`, `SWIRL`, and `SPIN` settings I can tune.
- It pauses when the tab is hidden, shows a still frame when reduced motion is on, and falls back to plain navy if WebGL is unavailable.

---

## 6. Card layout

**What I asked for**
- More rectangular cards with an image slot for a picture of each artifact, and a reorganized text layout.

**What changed**
- Each card has an image slot on the left. The text on the right is ordered: label (artifact number and due date) with a Live / Coming soon pill, title, short description, reflection, link.
- Cards are two per row on wide screens, one per row on tablets, and the image moves on top on phones.
- Reflection text is hidden in the grid and shown in a popup (see next section).

---

## 7. Card popup

**What I asked for**
- When I pasted in my long reflection, the card looked comically large. I asked for every card to show everything except the reflection, and for a click to fade in a full card from the center of the screen over a blurred background, with the reflection included.

**What changed**
- Clicking a card opens a larger copy of it in a native `<dialog>` with a blurred, dimmed backdrop and a fade-and-scale-in. It closes with the × button, a click outside the card, or Esc.
- Clicking the link inside a card still follows the link instead of opening the popup.
- Cards can also be opened from the keyboard (Tab to focus, Enter or Space to open).

---

## 8. Reviews and fixes

- IntelliJ flagged two CSS warnings. Both were false alarms because JavaScript sets those values at runtime, and I added default values to quiet one of them.
- Claude reviewed the whole file and found a deleted spotlight rule, a nav tab that could not become active by scrolling, and leftover colors from the old theme.
- Stray code-fence markers (three backticks) from copying out of the chat made IntelliJ flag `<!DOCTYPE html>`. I removed them.
- A later review found the footer's base CSS rule missing, placeholder image paths with no files behind them, and a generic LinkedIn link. I re-added the footer rule and line.
- Pushed the first full version of the site to `main` for a live check, before filling in card ideas.

---

## Where Claude misread me or I had to correct course

- **Jumped ahead:** Claude built a three-theme comparison page before I understood how GitHub Pages hosting works. I said we were jumping the gun, so we stopped and learned hosting first.
- **Repo name:** I asked about `kevlam.github.io`. It has to match my username, so it is `kevlam1.github.io`.
- **Wrong settings page:** I opened my account-level Pages settings (verified domains) instead of the repo's own Pages settings.
- **Accent color:** using #0f172a as the accent would have made links and buttons nearly invisible, so it became the background color.
- **Card layout took three tries:** I asked for "two columns inside one, stacked." Claude read that as one narrower column, then gave me two cards per row with the image on top. I meant wide rectangles (image left, text right), two per row. I learned to describe the layout precisely.
- **Background shader:** the first version was too zoomed in, and it drifted in every direction. The original I liked spirals around the center, so Claude added zoom and swirl controls.
- **Pages Claude could not open:** it could not read the Shadertoy page or one of the course guides, so I had to paste or describe what I wanted.
- **Checking sources:** I asked Claude to double-check sources. It checked the assignment against the course site and the hosting steps against GitHub's docs, and it flagged things it could not verify instead of guessing.

---

## Decisions and abandoned ideas

- Considered building with Tailwind or a framework. Chose plain HTML, CSS, and JavaScript.
- Considered making the repo private. Pages on a free account needs a public repo, and the site is public anyway.
- Started with a two-line divider and cut it down to one line.
- Dropped the idea of copying the Shadertoy shader's code.
- Dropped a photo of myself from the intro.

---

## Not yet verified

- Testing on a phone and a small window: nav fit with five tabs, card layout, popup sizing, and background performance.
- Whether `LOG.md` displays well when linked from the live site's footer.
- Whether the footer line and glow show against the animated background.

---

## Still to do

- [ ] Write my own ideas for cards 2-5 (they still say "Idea: TBA").
- [ ] Replace the generic LinkedIn link with my profile URL, or remove it.
- [ ] Add real screenshots, or put the "Image coming soon" placeholders back on cards with no image file yet. Write real alt text.
- [ ] Optionally rewrite the intro headline and subtitle in my own words.
- [ ] Push the latest changes and check the live site in a private window and on my phone.
- [ ] Submit the link on Canvas by Sunday, Oct 11 at 11:59 PM.