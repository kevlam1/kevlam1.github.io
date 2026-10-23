# Lessons learned (so they are not repeated)

## Pasting and editing mistakes
- Code fences (three backticks) copied from a chat ended up in `index.html` and made the editor flag `<!DOCTYPE html>`. Never leave fences in a source file.
- A block of CSS pasted inside a `<script>` tag produced 17 editor errors.
- The scroll progress bar was pasted twice (CSS and script), and the CSS for the star was missing, so the unsized SVG drew a huge black star over the page. Fix: replace the whole block at once and size inline SVGs directly.
- Blur-fade code pasted outside its script wrapper, and Lenis CSS pasted inside the `html{}` rule, both did nothing or threw. Check where a snippet goes before pasting.
- Deleting one rule from a block can leave a stray brace that breaks the next rule. Replace whole blocks.

## Performance
- `backdrop-filter` over an animated WebGL background re-renders every frame. Fixes: cap the background at about 30fps, remove blur from the header (its background was opaque anyway), throttle scroll handlers to once per frame, hide the blur when it is faded out.
- Spinning loader parts are HTML elements with `will-change: transform`, so they keep turning while the main thread is busy.
- Move things with `transform`, not `width`, in per-frame animation (the progress bar).

## Scrolling and layout
- `scroll-behavior: smooth` only smooths anchor jumps. Lenis smooths wheel scrolling, and must be stopped while a modal is open (`data-lenis-prevent` on the dialog plus `lenis.stop()`/`start()`).
- Animate a wrapper (`.card-entrance`), not the card, so the entrance does not overwrite the tilt transform.
- Cards that finish their entrance on page load show nothing when scrolled to. Trigger entrances with IntersectionObserver.
- A footer jumps when the page is empty during loading. Hold the page height open while the loader shows.
- An image's natural size can feed back into its container (the rotation bug). Put the image in a fixed aspect-ratio box with `position:absolute; inset:0`.
- A navy strip at the bottom of a phone is the browser toolbar collapsing. The same strip shows on google.com. `lvh` units and oversized background layers did not change it.
- In a popup, the browser autofocuses the first focusable element. Give the close button `autofocus` or the popup opens scrolled to the "Visit" link.
- Put the card's grain layer outside the scroll area (an inner scroller) so it does not scroll away.

## Phone testing on Windows
- `localhost` on a phone means the phone. Use the computer's IPv4 address (`ipconfig`).
- Same Wi-Fi network, cellular off.
- IntelliJ's built-in server had "Can accept external connections" grayed out. `python -m http.server 8000` in the project folder works. It only serves files and does not live-reload.
- Windows Firewall may need Private network access for Python.

## GitHub and hosting
- A user site repo must be named `<username>.github.io`. Any other name serves from a subpath and absolute paths break.
- The Pages settings that matter are in the repo's Settings, not the account page ("Verified domains" is for custom domains).
- Pages is case-sensitive. A case-only rename (`LOG.md` to `log.md`) may not register in git on Windows. Rename via a temporary name (`git mv LOG.md log-temp.md`, then `git mv log-temp.md log.md`) and confirm GitHub shows the lowercase name.
- Changes can take up to about 10 minutes to appear. Check in a private window.
- Keep `.idea/` out of the repo. Add `.gitignore`.

## Third-party code and licensing
- Shadertoy shaders carry a restrictive default license (CC BY-NC-SA) unless the author says otherwise. Write original shaders inspired by the look. Do not copy.
- React Bits components are React. For a no-build site, port the technique to plain JS. Their license terms were not checked, so check before reusing beyond a personal portfolio.
- Tailwind's in-browser (Play CDN) build is meant for development. It was not used.
- Pin CDN versions.

## CSS layout gotchas found while building the popups and the Artifact 3 demo
- `:nth-child()` counts every sibling, not just the type you mean. Three window dots in front of the lines made `.demo-bar:nth-child(1)` match nothing, so the result bars never filled in motion mode. Use `:nth-of-type()` or a class, and measure the computed result (`animationName`, width) instead of judging by eye.
- Flex items shrink by default. With `min-height: 0` on text blocks inside a fixed-height flex column, a narrower column squashed the description to one line and the next block painted over its overflow. Set `flex-shrink: 0` on blocks that must keep their content height and let the container scroll.
- A `position: sticky; bottom: 0` element inside a scroll container that has padding is inset by that padding. Put the bottom padding on the sticky element instead.
- Percent heights and aspect ratios on an auto-sized grid column can fight each other. Give the column an explicit size from one shared value (`--sq`) instead.
- Do not scope size rules with `vw` caps to all screen sizes: `48vw` collapsed the popup to 187px on a phone. Wrap them in a media query.
- Gradient text only paints inside its own box, so letters that hang below the line (g, p, y) get sliced off. Add bottom padding with a matching negative margin.
- A soft full-width glow behind whole sections made headless Chrome stall at 2560 by 1080. Keep big glows to the hero.
- A real control (a button) cannot live inside `aria-hidden` or inside `role="img"`: it becomes unreachable or is flattened into the image. Hide only the decorative parts and give the container `role="group"`.
- `requestFullscreen()` needs a real user gesture. In headless tests, call `Runtime.evaluate` with `userGesture: true`, or the click is silently refused.
- The popup is a clone of the card, so listeners attached to the card's own elements are not copied. Use one listener on `document` and `closest()`.
- To match a tilt made in Photoshop, measure it: compare the finished images with their shared background and find the corners of what changed. A flat parallelogram is one `matrix()`; no perspective maths needed.
- An element that fills a box the way `object-fit: cover` does can be made from a square stage sized `max(100cqw, 100cqh)`, centered. Percent positions inside it then stay fixed at every card size.

## Editor warnings that are false alarms
- CSS variables set by JavaScript at runtime (`--mx`, `--my`, `--fade`) show as unresolved. Defaults can quiet them.
- Classes created by scripts (`.gradual-blur-layer`, `.active`) show as unused.

## Accuracy habits
- Check pages and docs before answering. Say what could not be checked.
- Do not describe a feature a project does not have. Descriptions were corrected against the READMEs.
- Data Dragon, the League static data source, is documented as inaccurate in places (spell data, item stats), and can lag patches. Verify what is shown.
- Riot API: a development key is for testing and personal use, a public product needs a production key, and the key must stay out of a public repo.

## AI tool behavior observed
- Another chat AI repeatedly reversed its own code within a single message and ignored an instruction to stop. Another blurred the difference between the tool that builds software and an AI the finished app calls. The fix was to ask for exact placement, restate requirements, and check against the real course pages.
- Misreads in the Claude chat: built a three-theme comparison before Kevin understood hosting; read "two columns inside one, stacked" as one narrow column, then as image-on-top two-up, when Kevin meant wide rectangles (image left, text right), two per row; read "no tilt on cards 2 to 5" when Kevin meant "not clickable". Restate the layout before building.
