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
- `/media` now uses the same self-hosted fonts (from `../assets/fonts/`); `/resume` still loads its own outside libraries.

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
  link to page sections. It spins slowly, can be dragged, pauses only while the mouse is over a card
  (not the whole strip), and turns a card to the front only for keyboard focus (a mouse click won't freeze it). Note: don't name a class `ring`;
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

## Media page theme (Nov 3, 2026)
`media/index.html` keeps its own layout and CSS but now matches the main site's dark + neon look.
- Colors are set in the `:root` block at the top of its `<style>`. The old variable names were kept
  (`--teal` now holds the neon green `#c8ff2e`, `--navy` is the dark background, `--card` is the card color),
  so nothing else in the page had to change.
- Fonts: Inter and Stack Sans Headline, loaded from `../assets/fonts/` (no Google Fonts).
- The block marked `MAIN-SITE LOOK` at the end of its `<style>` adds the big headings, glassy nav,
  neon Contact button, rounded cards, and the neon scroll progress bar (`#scroll-progress`).

## Media page press kit (Nov 3, 2026)
Built for Qwoted journalists. Sections on `media/index.html`, top to bottom:
- **Deadline banner** (`.deadline-banner`, top of the hero): availability and "replies within 24 hours".
- **Fast Facts** (`.fast-facts`, under the hero): location, formats, reply time, clinical and policy focus.
- **Commentary Beats** (`#expertise`): the four beats from the press sheet.
- **Press Soundbites** (`#soundbites`): three quotes, each with a Copy Quote button.
- **Bios** (`#bio`): short and full bio, each with a Copy button. The full bio keeps
  `id="bioText"` and class `media-bio-text` (used by the search engine "speakable" data).
- Copy buttons all use one function, `copyText(id, button)`, in the script at the bottom.
- Only email and the contact form are offered (no phone number on purpose).

**Media sheet PDF:** `media/JoAnne-Andrea-Gomez-RN-Media-Sheet.pdf`, made from
`media/media-sheet.html` (hidden from search engines). If you change the bios or quotes on the page,
change them in `media-sheet.html` too, then rebuild the PDF by printing that page to PDF
(Letter size, no headers/footers) and check it is still one page.

## Story Desk in the media hero (Nov 3, 2026)
The hero on `media/index.html` is now a press-pack builder (`#story-desk`). The static topic tags and
the two hero buttons were replaced by five beat buttons (`.beat`, keyed by `data-beat`). Tapping one:
- shows the cleared quote for that beat in `#pack-quote` and the attribution line;
- rewrites the "Email JoAnne about this" link into a mailto with a subject line and a short
  fill-in-the-blanks body for that beat;
- "Copy quote + attribution" puts the quote and attribution on the clipboard;
- "Use the request form instead" jumps to `#contact` with the Topic and Inquiry Type already filled in.
The quotes, topics and subject lines live in the `BEATS` object in the page script. To change a quote,
edit it there (the Soundbites section further down has its own copy of the three original quotes).
Styles are in the `STORY DESK` block at the end of the `<style>`. On phones the beats go two across and
the buttons stack full width. People with "reduce motion" on get no swap animation.
