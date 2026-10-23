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
- [ ] Replace placeholder images and alt text on cards 4 and 5 as each artifact is finished. (Artifact 3 uses an animated CSS illustration instead of a photo; see `docs/SITE_GUIDE.md`.)
- [ ] When unlocking Artifacts 4 and 5, add `target="_blank" rel="noopener"` to every link that leaves the site. Artifacts 2 and 3 both missed this at first and had to be fixed afterward (log sections 24-25).
- [ ] A LinkedIn link, once Kevin has a real profile URL (uncomment the icon block in the footer).
- [x] Kevin retook `images/artifact-1.jpg`; it shows the new "Building optimized systems." headline. Its alt text still reads "Portfolio front page.", which is still accurate.
- [ ] Retake `images/image-link-preview.jpg` (1200x630). It still shows the old three-line headline in the old serif font. The `og:image:alt` meta tag on both pages describes that old screenshot, so update it when the image is replaced.
- [x] The redesign is merged to `main` and pushed (commit `3f2a5db`), and the local `redesign` branch is deleted. That merge also fixed the popup's "View Build Log" buttons, which used the footer link's gradient-text class (`log-link`); they are `build-log-link` now.
- [ ] After the redesign deploys, check the live site and `log.html` on a real phone and in Safari and Firefox. It was only tested in headless Chrome.
- [ ] Check the popups (all four photo cards and Artifact 3) and the Artifact 3 demo on a real phone, in Safari and in Firefox. Also try the demo's full screen button on a real phone and tablet (it is hidden on iPhone Safari by design, and only tested in headless Chrome). Container units (`cqw`) and `:has()` need a fairly current browser; only headless Chrome was tested.
- [ ] Older inline SVGs without `width`/`height`/`fill` on the tag (the progress-bar star and the footer GitHub icon) are sized by CSS and work, but break the hard rule in `CLAUDE.md`. Add the attributes if the site is touched again.
- [x] Added the progress bar to `log.html`. It re-measures on page-height changes (a `ResizeObserver` on `body`) so it adjusts when boxes open or close.

## Upcoming artifacts
- [ ] Artifact 2 (due Sun Oct 18): new repo, `CLAUDE.md`, log, first build with Claude Code. Read the Artifact 2 page and "Your First Session" again before starting. See `ARTIFACT_PLANS.md`.
- [ ] Read the Artifact 3, 4, and 5 pages before planning them.
- [ ] Read the written AI Policy page and "Your Course Access".
