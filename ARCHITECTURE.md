# ProRN Inc. Website: How It Works

## Hosting
Plain static files served by GitHub Pages at prorninc.com (set by the `CNAME` file).
Pushing to the `main` branch updates the live site. GitHub runs no build; the one compiled
file (`assets/css/site.css`) is built by hand and committed (see below).

## Pages
- `index.html` — the main one-page site (story, forecast, budget, solutions, proposals, contact).
- `media/index.html` — media page (prorninc.com/media).
- `resume/index.html` — resume page (prorninc.com/resume).
- `sitemap.xml`, `BingSiteAuth.xml` — search engine files.

## Libraries (self-hosted on index.html since Nov 3, 2026; no outside requests)
- `assets/css/site.css` — Tailwind CSS 3.4.17, compiled and minified. It only contains the
  classes `index.html` uses, plus the @font-face rules for the fonts below.
  **If you add a Tailwind class that the page didn't use before, rebuild it** from the repo folder:
  `npx tailwindcss@3.4.17 -c src/tailwind.config.js -i src/tailwind-input.css -o assets/css/site.css --minify`
  (source files: `src/tailwind-input.css`, `src/tailwind.config.js`).
- `assets/fonts/` — Inter (variable, body text) and Stack Sans Headline 400–700 (headings), from Fontsource.
- `assets/fontawesome/` — Font Awesome Free 6.4.0 (CSS + woff2 fonts). Loaded before site.css on purpose,
  so Tailwind's line heights win, as they did before.
- `assets/js/lucide.min.js` — Lucide icons 1.67.0. Note: Lucide has no brand logos, so the footer
  LinkedIn icon uses Font Awesome (`fa-brands fa-linkedin`).
- `/media` and `/resume` still load their own outside libraries; they were not changed.

## Accessibility notes
- The moving hero word is hidden from screen readers; a hidden full sentence
  ("We have the staffing, funding, and nursing ideas.") is read instead.
- The two wide tables sit in focusable, labeled regions so keyboard users can scroll them.

## Look and feel (Swash-style redesign, Nov 2026)
All theme styling lives in the `<style>` block in the `<head>` of `index.html`.
- **Theme layer:** recolors the existing Tailwind classes (white/slate/blue) into a dark
  background with neon green (`--neon: #c8ff2e`). The page markup was left as is, so
  content edits work the same as before. Colors are set once as variables in `:root`.
- **Kinetic hero:** "We have the ___ ideas." The middle word cycles through
  staffing, funding, nursing (script at the bottom of the page, element `#k-word`).
- **Scroll progress bar:** thin neon line at the top (`#scroll-progress`).
- **Scroll reveal:** sections fade up as they come into view. Only turns on when
  JavaScript runs, so the page still reads fine without it.
- **3D card ring:** in the Solutions section (`#ring-stage` / `.ring3d`). Six cards that
  link to page sections. It spins slowly, can be dragged, pauses on hover, and turns a
  card to the front when it gets keyboard focus. Note: don't name a class `ring`;
  Tailwind already uses that name and draws a blue outline.
- People who set "reduce motion" on their device get no spinning or animation.

## Contact form
Posts to Web3Forms (`api.web3forms.com/submit`) using the access key in the form.
The script at the bottom of `index.html` shows the success or error message.

## Page sections added Nov 3, 2026
- **Start here band** (`#start-here`, right under the hero): three action cards.
  Two link to the full proposals on the page (`#pool-implementation`, `#proposal-start`);
  the neon one links journalists to the media page request form (`/media/#contact`).
  Below them, "The 10-Second Version": a three-point executive summary.
- **Forecast data cards** (`.metrics` at the top of `#forecast`): six big-number cards.
  Each has the number, a label, and a short source line. Edit the text directly.
- **Budget tracker** (`#budget-tracker` inside `#budget-2026`): dated updates, newest first.
  To add an update: copy one `<li class="t-item">` block, paste it at the top of the list,
  change the date, title, text, and source link, then change the "Last updated" date.
  Only add entries with a real, linked source.
- **Media callout** (`.media-callout` in "Who Is Behind This"): sends journalists to `/media/#contact`.
