# Open work (as of Sunday Oct 11, 2026)

## Artifact 1
- [ ] Confirm the Artifact 1 portfolio link was submitted on Canvas (due Sunday Oct 11 at 11:59 PM). The weekly quiz, reflection, and group meeting minutes are separate deliverables due the same night.
- [ ] Confirm the repo shows `log.md` in lowercase on GitHub. The log page fetches that exact name.
- [ ] Push the latest `index.html`, `log.html`, and `log.md`, then check the live site and the log page in a private window and on a phone.
- [ ] Verify the scroll progress bar: it should be one thin line under the header with a small spinning star on its tip, no giant black star. The previous attempt pasted the code twice and omitted the star's sizing CSS.
- [x] Kevin checked the live site and log page on his phone (Oct 11) and everything worked. Previously open phone checks: nav fit with five tabs, background performance, gradual blur and Lenis feel, and the log page on a narrow screen.
- [ ] `log.md` has a few lines that no longer match the code. Section 13 mentions `OVERSHOOT = 120` and `clientWidth`/`clientHeight` leftovers, but the current files use `OVERSHOOT = 48` and `innerWidth`/`innerHeight`. Section 6 says one card per row on tablets, but phones and tablets (900px and below) show two per row now. The `theme-color` meta tag is not mentioned. Section 14 says the progress star spins with scroll position, but it now spins constantly. Ask Kevin before changing past entries. (The progress bar, footer link, and font are now logged in section 14.)
- [x] `.scroll-progress` was defined twice in `index.html`. The duplicate is removed.
- [x] Footer link: Kevin kept the `/log.html` text and added a small, faint "build log" caption under it, with a spinning star on each side.
- [x] Added Open Graph tags to both pages, using `images/image-link-preview.jpg` (1200x630).
- [ ] After deploying, check the link preview with a preview checker (for example LinkedIn's Post Inspector). Platforms cache previews, so a re-scrape may be needed.

## Site backlog (only when asked)
- [ ] Add an "In progress" status for progress-week cards.
- [ ] Replace placeholder images and alt text on cards 2 to 5 as each artifact is finished.
- [ ] A LinkedIn link, once Kevin has a real profile URL (uncomment the icon block in the footer).
- [x] Added the progress bar to `log.html`. It re-measures on page-height changes (a `ResizeObserver` on `body`) so it adjusts when boxes open or close.

## Upcoming artifacts
- [ ] Artifact 2 (due Sun Oct 18): new repo, `CLAUDE.md`, log, first build with Claude Code. Read the Artifact 2 page and "Your First Session" again before starting. See `ARTIFACT_PLANS.md`.
- [ ] Read the Artifact 3, 4, and 5 pages before planning them.
- [ ] Read the written AI Policy page and "Your Course Access".
