## Oct 6: Look and feel

**What I asked for**
- Showed Claude a reference portfolio (dark background, lime accent, big headline, section nav) and said I liked its layout, colors, and animation.
- Asked for changes: no photo of me, everything centered, Georgia serif font, and a load animation where each row of text fades in from below, one after another.
- Asked for a grainy background texture, then for the green to be replaced with #0f172a and its variants.

**What changed**
- Claude wrote a first plain HTML/CSS version with five card placeholders and the staggered fade-in on the intro.
- Added a grain effect (an SVG noise image tiled over the page and over each card) with a strength setting I can adjust.
- Recolored the site to a navy theme. #0f172a would have been nearly invisible as an accent on a dark page, so it became the base background and lighter slate shades are used for text, borders, and accents.

**Where Claude misread or I had to correct course**
- Claude built a three-theme comparison page before I understood how GitHub Pages hosting works. I said we were jumping ahead, so we stopped and learned hosting first.
- I asked about naming the repo `kevlam.github.io`. It has to match my username, so it is `kevlam1.github.io`.

## Oct 6: Interactive touches

**What I asked for**
- A tilt effect on the Artifact 1 card (it is the only active card): it should grow by a few pixels when my cursor is over it.
- A spotlight glow that follows the cursor inside that card.
- An animated sliding highlight on the top navigation bar.
- I gave Claude ideas and references for each effect.

**What changed**
- Card 1 tilts toward the cursor (about 10 degrees at most), grows about 4px, and shows a soft white spotlight that follows the mouse.
- The nav is now a pill-shaped bar with a highlight that slides to the clicked link. I also had it follow the section on screen as I scroll, which goes a step beyond the tutorial.
- All of these motion effects are turned off for visitors whose system is set to reduce motion.

**Decisions**
- Only card 1 gets the hover effects for now. I will extend them to other cards as I finish those artifacts.
- No Tailwind. I considered it, but its browser-based version is meant for development, and plain CSS kept the site simple.
- No Next.js or Vercel. The course deploy guide covers them, but a plain HTML site needs no build step.

**Not yet verified**
- I have not tested the effects on a phone or a small window. To check after pushing: tilt strength, spotlight visibility, and whether the nav highlight tracks scrolling correctly.

## Still to do
- Replace the placeholder name text and headline with my own wording.
- Write my About section.
- Write my own ideas for cards 2-5.
- Confirm the footer link to this log works on the live site.
- Final check in a private window and on my phone, then submit the link on Canvas.

## Oct 6: Adding more elements and fixes
- Wrote my About section from my own details (Computer Science and Systems senior, likes building usable tools and optimization, learning AI in my workflow).
- Added GitHub and LinkedIn icon links to the footer.
- IntelliJ flagged two CSS warnings; both are false alarms because JavaScript sets those values at runtime.
- Added another to the top bar and renamed works header to artifacts.
- Added another section that includes my projects outside the course.
- Added "Side Projects" and "Connect" sections and a bigger tilt/grow on card 1.
- Reviewed the file with Claude and found a deleted spotlight rule, a nav tab that couldn't activate, and leftover colors from the old theme.
- Found a formatting error: stray code-fence markers in the HTML file made IntelliJ flag an error. Removed them.