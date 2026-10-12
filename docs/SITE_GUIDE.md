# Site guide: how the portfolio is built

Values below were current when this was written. If the code disagrees, the code wins. Tell Kevin and fix this file.

## index.html

Single file: one `<style>`, then the HTML, then script blocks (each an IIFE with a comment banner).

**Head:** UTF-8, viewport, title "Kevin Lam | Portfolio", description, `theme-color` meta `#0f172a`.

**Body order:** `<canvas id="bg">` (WebGL waves), `.gradual-blur` (layers built by script), `<header>` (fixed nav pill bar with five tabs plus the scroll progress bar), `<main>` (intro, divider, about, divider, artifacts, divider, side projects), `<footer id="connect">`.

**Sections:** `#intro` (staggered `.rise` hero with `--i` delays), `#about`, `#artifacts`, `#side-projects`. `.divider` is a one-line glowing rule between sections. The footer has its own glowing top line (`footer::before`), a GitHub icon, a commented-out LinkedIn icon, "Built for TCSS 490, Autumn 2026.", and `a.log-link` pointing to `log.html` (drifting blue-to-white gradient text, tight white glow on hover). The link sits in `p.log-line` between two spinning `.log-star` SVGs (12px, loader glow, 5s per turn), with a faint `p.log-caption` ("build log") under it. `images/favicon.svg` is the star turned 45 degrees with its points on the corners, navy or white by color scheme, linked from both pages.

**Design tokens (`:root`):** `--bg #0f172a`, `--panel #1e293b`, `--line #334155`, `--text #e2e8f0`, `--muted #94a3b8`, `--accent #ffffff`, `--grain .13`, `--noise` (an SVG feTurbulence data URI), `--desc-lines 3`, `--card-h 300px`. Font: DM Sans from Google Fonts (weights 400 to 700) with Arial as the fallback, on both `index.html` and `log.html`. Everything is centered. Header background is `rgb(24,24,24)`.

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
| Lenis | Smooth wheel scrolling from jsDelivr (`lenis@1`). Routes `#` links through `lenis.scrollTo` with offset -70. Skipped for reduced motion | `lerp 0.1` |
| Scroll progress | A thin line under the header. Moves with `transform`, with a small glide. The star on its tip (`.progress-star`) spins constantly with a CSS animation, stopped for reduced motion | `GLIDE .14`; star size `--star 18px` and `3s` per turn are in the CSS |

The star path used everywhere is `M12 0C13 8 16 11 24 12C16 13 13 16 12 24C11 16 8 13 0 12C8 11 11 8 12 0Z` (24 by 24 viewBox).

### Responsive rules
- 900px and below (and short landscape phones): two cards per row, image on top, smaller text and pills, titles reserve two lines so rows line up, bold titles. Image box uses `aspect-ratio 2.4 / 1` with the image absolutely positioned (this fixed an image that stayed large after rotating the phone).
- 640px and below: single-column cards in the grid, popup stacks image above text.
- 520px and below: compact nav tabs.
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
