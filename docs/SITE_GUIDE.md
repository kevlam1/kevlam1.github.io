# Site guide: how the portfolio is built

Values below were current when this was written. If the code disagrees, the code wins. Tell Kevin and fix this file.

## index.html

Single file: one `<style>`, then the HTML, then script blocks (each an IIFE with a comment banner).

**Head:** UTF-8, viewport, title "Kevin Lam | Portfolio", description, `theme-color` meta `#0f172a`.

**Body order:** `.intro-loader` (the opening animation), `<canvas id="bg">` (WebGL waves), `.gradual-blur` (layers built by script), `<header>` (fixed nav pill bar with five tabs plus the scroll progress bar), `<main>` (intro, divider, about, divider, artifacts, divider, side projects), `<footer id="connect">`.

**Sections:** `#intro` (a small label, the headline "Building optimized systems." as three `.word` spans, and the button; all are `.rise` with `--i` delays that start after `--intro-delay`), `#about`, `#artifacts`, `#side-projects`. `.divider` is a one-line glowing rule between sections. The footer has its own glowing top line (`footer::before`), a GitHub icon, a commented-out LinkedIn icon, "Built for TCSS 490, Autumn 2026.", and `a.log-link` pointing to `log.html` (drifting blue-to-white gradient text, tight white glow on hover). The link sits in `p.log-line` between two spinning `.log-star` SVGs (12px, loader glow, 5s per turn), with a faint `p.log-caption` ("build log") under it. `images/favicon.svg` is the star turned 45 degrees with its points on the corners, navy or white by color scheme, linked from both pages.

**Design tokens (`:root`):** `--bg #0f172a`, `--panel #1e293b`, `--line #334155`, `--text #e2e8f0`, `--muted #94a3b8`, `--accent #ffffff`, `--grain .13`, `--noise` (an SVG feTurbulence data URI), `--desc-lines 3`, `--card-h 300px`, `--gap 20px` (card grid gap, 12px at 900px and below), `--glow 122,162,255` (RGB for the blue glows), `--live` and `--progress` (status pill colors), `--ease`, and `--ornament` (the star-and-lines under each `h2`, an SVG data URI). Font: DM Sans from Google Fonts (weights 400 to 700) with Arial as the fallback, on both `index.html` and `log.html`. Everything is centered. Header background is `rgb(24,24,24)`.

### Card anatomy
```html
<div class="card-entrance" style="--card-i:0">          <!-- slide-in wrapper; delay uses --card-i -->
  <article class="card live" id="artifact-1">            <!-- live or locked -->
    <div class="media"><img src="images/artifact-1.jpg" alt="..."></div>
    <div class="card-body">
      <div class="meta"><span>label</span><span class="status live">Live</span></div>
      <h3>Title</h3>
      <p class="desc">Three lines of description.</p>
      <div class="toolkit"><span class="toolkit-pill">HTML</span>...</div>
      <p class="reflection">Hidden in the grid, shown in the popup.</p>
      <p class="links"><a class="hover-link" href="...">Visit ...</a></p>
    </div>
  </article>
</div>
```
- `live` cards: accent border, tilt, spotlight, click opens the popup. `locked` cards: dimmed, normal cursor, no popup, no keyboard focus.
- Rows match because `.desc` reserves three lines and `.toolkit` reserves two rows of pills. Placeholder cards carry a "Toolkit: TBA" pill for the same reason.
- `.card .reflection{display:none}` in the grid. The popup clones the card, adds `.modal-card` (and `.accent` if it was live), wraps the contents in `.modal-scroll`, and shows the reflection with a "Reflection" label.

### How to unlock a finished artifact's card
1. Change `class="card locked"` to `class="card live"`.
2. Change the pill to `<span class="status live">Live</span>`.
3. Replace the description (about three lines), the toolkit pills, the reflection (Kevin's words), and add a `.links` paragraph with `hover-link`. For links that leave the site add `target="_blank" rel="noopener"`.
4. Replace the image and alt text (1200 by 900 works well; keep the important content near the center because crops differ by view).
5. Add a log entry. No JavaScript changes are needed, since the scripts select `.card.live` and `.card:not(.locked)` at load.
6. For a progress week, the card should show where he is so far. The only statuses today are Live and Coming soon. An "In progress" status may be needed. Ask Kevin.

### Scripts in index.html and their settings
| Script | What it does | Settings |
| --- | --- | --- |
| Gradual blur | 8 stacked backdrop-blur layers with soft gradient masks along the bottom edge. Fades out over the last 250px of scroll so the footer stays readable | `DIVS 8`, `MAX_BLUR 10`, `POWER 2.2`, `OVERSHOOT 48`, band 150px tall (100px at 640px and below), `FADE_DIST 250` |
| Tab navigation | Sliding highlight pill. Follows the section in view (probe at 40% of the viewport) and the bottom of the page. Pauses tracking for 1400ms after a click | `probe .4`, `1400` |
| Card tilt | `perspective` tilt plus a width grow, spotlight position via `--mx`/`--my` | `MAX_TILT 5`, `GROW_PX 16`, throttle 100ms |
| WebGL background | A custom shader of slow navy waves swirling around the center. Original code (a Shadertoy shader was the inspiration; its code was not copied). Pauses when the tab is hidden, a still frame for reduced motion, plain navy if WebGL is missing | `SPEED .05`, `ZOOM 3.2`, `SWIRL 2.3`, `SPIN .4`, `SCALE .7`, `FRAME_MS 29` |
| Card modal | Native `<dialog>`. Close button gets autofocus (the browser used to focus the "Visit" link and scroll the popup). Esc, outside click, and the close button all close it. Stops and restarts Lenis | fade 280ms |
| Card entrance | IntersectionObserver adds `.in-view` to each `.card-entrance` | `threshold .15` |
| Click stars | A burst of four-pointed stars on each click or tap. Moves into the open dialog so it is not hidden | `COUNT 7`, `SPEED [110,210]`, `SIZE [9,17]`, `LIFE [350,550]`, `GRAVITY 90`, `MAX 90` |
| Artifact 3 demo illustration | One animation shown two ways, both pure CSS and HTML (no video file), labeled "Illustration, not a recording". The popup (a clone of the card) shows `.demo-stage` flat: a video-style frame with a terminal window, a caption and a timestamp for each step, a scrubber, and a working full screen button, sized in `cqw` (container units) so it scales like a video. The card thumbnail shows the same frame tilted like the other cards' screenshots (no laptop): it sits on `images/Artifact Images Background.jpg`, and `.demo-video` gets one `matrix()` transform. Steps: the command types out one character at a time (`.demo-typed`, `steps(41,end)`), three staggered lines show the real parts of the tool (gather script, model, check script), then the real result numbers grow in as eased bars. The numbers must only ever come from a real run; re-check them in `readme-architect-out/` before changing. Default (and reduced motion) shows the finished frame with no animation | shared 12s loop (`demoTyping`/`demoScanning`/`demoResults` keyframes), bar percentages set per element via `--pct`, scrubber `demoScrub` |
| Lenis | Smooth wheel scrolling from jsDelivr (`lenis@1`). Routes `#` links through `lenis.scrollTo` with offset -70. Skipped for reduced motion | `lerp 0.1` |
| Scroll progress | A thin line under the header. Moves with `transform`, with a small glide. The star on its tip (`.progress-star`) spins constantly with a CSS animation, stopped for reduced motion | `GLIDE .14`; star size `--star 18px` and `3s` per turn are in the CSS |

The star path used everywhere is `M12 0C13 8 16 11 24 12C16 13 13 16 12 24C11 16 8 13 0 12C8 11 11 8 12 0Z` (24 by 24 viewBox).

### Responsive rules
- `.cards` is a CSS grid with two columns. The last card of an odd count is centered at half width. Above 900px each card is image-left (42%) and text-right.
- 900px and below (and short landscape phones): still two cards per row, image on top, smaller text and pills, titles reserve two lines so rows line up, bold titles. Image box uses `aspect-ratio 2.4 / 1` with the image absolutely positioned (this fixed an image that stayed large after rotating the phone). All card images are `object-fit: cover`, centered, so the square images are cropped to fit.
- 640px and below: the popup stacks the image above the text.
- 520px and below: compact nav tabs. 380px and below: tighter still.
- Short landscape phones (500px tall or less): the hero headline is sized by screen height so it fits.
- Performance note: soft radial glows behind whole sections made headless Chrome stall at 2560 by 1080, so there are none. Only the hero has a glow. Do not add large full-width glow layers.
- Opening (`.intro-loader`): 22 small stars fly in from random directions, distances, sizes and speeds, spiralling into a glowing center star on a near-black background, which then flashes. A `mask` iris (the registered `--iris` property) opens outward from the center and the hero text blurs in word by word. The stars are created by a small script right after the loader markup, which sets `--a` (angle), `--r` (distance in vmax), `--twist`, `--s` (size), `--dur` and `--delay` on each one, so the pattern is different on every load. Each star repeats its own flight until the flash. All timing hangs on `--intro-delay` (2s). It plays on every load. Reduced motion hides the overlay. Browsers that cannot animate `@property` should show the reveal as an instant switch (not tested). Avoid orbit-style (ellipse) rings: the first version looked like an atom symbol and was rejected.
- Gradient text (`.word`, and the log page's title) only paints inside its own box, so `.word` has `padding-bottom: .2em` with a matching negative margin. Without it the bottoms of g, p and y are sliced off. Check new gradient text with a zoomed screenshot.
- Card meta: `.meta` stacks the status pill above the label (`flex-direction: column-reverse`), so cards line up even when a label is long.
- The popup's "View Build Log" button is `.build-log-link` (hidden on the collapsed card). Do not reuse `.log-link`, which is the footer's gradient link.
- Popup layout: wide (up to 1080px, or 1120px for photo cards) with left-aligned text, "Built with" and "Reflection" labels. The status pill floats over the image corner, `.links` becomes buttons (the first link is the white primary button), and the body rises in with `modalIn`. Photo cards (a real `<img>` in `.media`, matched with `:has(.media > img)`): the screenshots are square, so on screens over 900px wide the image column is exactly `--sq` wide, the same value that caps the popup's height (`min(86dvh,600px,48vw)`), so the box is square by construction and nothing is cropped. The whole text column scrolls like a page and `.links` stays pinned at the bottom. At 900px and below (and on phones) the popup stacks: the whole popup scrolls, the image sits on top (a true square on phones, height-capped on tablets with a matching dark background and `object-fit: contain`), and `.links` is pinned. The Artifact 3 popup (matched with `:has(.demo-media)`) uses a 58/42 split so the video is wide. The status pill is `position: absolute` inside `.modal-scroll`, so nothing between them may have a transform, filter, or `will-change`, or the pill anchors to that element instead; the first block of the popup body therefore only fades (`modalFade`). Test the popup with animations ON as well as with reduced motion, and at phone, tablet, landscape-phone and laptop sizes.
- Demo full screen: the fullscreen icon in the Artifact 3 player bar is a real `<button class="demo-fs">`. A small script ("DEMO FULL SCREEN") listens on the document, because the popup is a clone of the card and clones do not keep their own listeners. It calls `requestFullscreen()` on `.demo-stage` (not on `.demo-video`), so the stage turns black and the video keeps its 16:10 shape with bars on any screen, with a 36px strip kept for the "Illustration, not a recording" label. The button's `aria-label` flips to "Exit full screen". If `document.fullscreenEnabled` is false (iPhone Safari cannot full-screen a page element) the script adds `no-fs` to `<html>` and the button is hidden. Because the group now holds a real control, `.demo-media` is `role="group"` and only its decorative parts are `aria-hidden` (`role="img"` or `aria-hidden` on the whole stage would hide or break the button). On a portrait phone fullscreen gains nothing; rotating the phone gives the bigger view. The other player icons (play, volume, menu) are still decoration only.
- Demo thumbnail tilt: the other cards' images were made in Photoshop (distort 20, rotate -10, scale 65% from 1920x1080) onto the background in `images/`. The tilted corners were measured from `artifact-1.jpg`, `artifact-2.jpg` and `side-project-1.jpg` against that background (1200x1200: top-left (105,465), top-right (870,336), bottom-right (1096,734), bottom-left (328,863)). Because the shape is a flat parallelogram, the frame is reproduced with `transform: matrix(.98582,-.16624,.45979,.82062,0,0)` on `.demo-video` (origin top-left; top edge = 776 units of 1200, left edge = 485 units for a 776 wide frame). The thumbnail's stage is a square as wide as the longer side of the box, centered, so it is cropped exactly the way `object-fit: cover` crops the photos, at every card size. If the Photoshop recipe or background changes, re-measure; do not guess. The thumbnail's copy of the full screen button is `visibility: hidden` so the card (itself a button) never contains a second control. The label is pinned to the visible corner and shortens to "Illustration" in narrow crops (container query).
- Popup has an inner scroller (`.modal-scroll`) so the card's grain layer does not scroll away.

## log.html

Loads `log.md` with `fetch('log.md', {cache:'no-cache'})`, renders it with `marked@12` (jsDelivr, gfm and breaks on), and builds the page in the browser.

- Title area: everything before the first `##`. Then Expand all and Collapse all buttons.
- `STATIC_TITLES`: titles matching `/^what i set out to build$/i` become an always-open plain card and stay out of the menu.
- `GROUPS`: the first rule that matches wins. Numbered titles (`/^\d+\./`) go under "The build"; everything else under "Reflection". The comment in the file shows how to give a section its own group.
- Collapsible boxes use `details.log-section` with a Web Animations API open and close (height, padding, border, and opacity animate together). Instant for reduced motion.
- Contents menu: a plain JavaScript port of the React Bits Branched Menu (SVG branches, drawn accent line, marker, folding groups). Visible at 1100px and wider. At 1360px and wider the log is centered and the menu sits at the left edge. It follows scroll position, jumps to a section on click, and drops in and unfolds on load. License terms for that component were not checked.
- Background: a plain WebGL2 port of the React Bits Gradient Waves (raymarched waves). Recolored to the navy palette and made quiet. `CFG` holds the settings (`horizonColor #0f172a`, `waveColor #243b6b`, `crestColor #b6c4dc`, `speed .2`, `opacity .55`, `steps 60`, `scale .5`, `fps 30`). Mouse parallax and the shader's built-in grain were removed.
- Loader: a glowing four-pointed star spinning inside dashed rings. The spinning parts are HTML elements so the browser keeps them turning while the page builds. `MIN_SHOW 1000` ms minimum, fades out before rendering. If loading fails it shows a message and a GitHub link.
- Header: same bar as the portfolio, with a hover pill. Links to `index.html` and to `log.md` on GitHub.
- Scroll progress: the portfolio's bar and spinning star, copied (CSS after the top-bar rules, script at the bottom, `GLIDE .14`). A `ResizeObserver` on `body` re-measures when the page height changes, so the bar glides to the right spot as boxes open and close. If either page's bar changes, change both.
- Cards slide in on scroll with the same easing as the portfolio.
- Styling matches the portfolio (`--glow`, `--ornament`, gradient title, glass section cards). Bold-only lines (`p > strong:only-child`) render as small dotted labels, and `.section-body > p:has(> br)` styles the Date and Summary callout. That callout matches any top-level paragraph with a line break, so keep **Date:** and **Summary:** on two lines in `log.md`, and avoid other line breaks in top-level paragraphs.
- The contents menu (`#toc`) hides its scrollbar (`scrollbar-width: none`) but still scrolls with the wheel or trackpad. Measured 15px of scrollbar before and 0px now.
- `log.html` still defines `:root`, `details.log-section`, and `.branched-menu::before` twice each (older code). Merge them only with the menu scripts in mind.

## log.md conventions
- Line 1 is `# Build log: Artifact 1 (Portfolio)`, then two bold tool lines (chat AIs, editor, host, stack).
- `## What I set out to build`, then `## 1.` to `## N.` build sections, then `## Where AI misread me, or I had to correct course`, `## Decisions and abandoned ideas`, `## Not yet verified`. (There is no "Still to do" section. Open items live in `docs/TODO.md`.)
- Use bold labels inside sections. Use `---` between sections (the page ignores them; GitHub shows them).
- Checklists use `- [ ]` and `- [x]`. They display read-only on the page.
- Everything is first person and in Kevin's voice.

## Deploy and hosting facts
- GitHub Pages, deploy from a branch: `main`, folder `/ (root)`. Settings live in the repo's own Settings, then Pages (not the account-level Pages page).
- The user-site repo name must match the username, so the URL stays `kevlam1.github.io`.
- Pages is case-sensitive. The site is public even if the repo were private.
- `.gitignore` should contain `.idea/` and `*.iml`. Do not commit IDE files.
