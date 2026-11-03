# ProRN Inc. Website: How It Works

## Hosting
Plain static files served by GitHub Pages at prorninc.com (set by the `CNAME` file).
Pushing to the `main` branch updates the live site. There is no build step.

## Pages
- `index.html` — the main one-page site (story, forecast, budget, solutions, proposals, contact).
- `media/index.html` — media page (prorninc.com/media).
- `resume/index.html` — resume page (prorninc.com/resume).
- `sitemap.xml`, `BingSiteAuth.xml` — search engine files.

## Libraries (loaded from CDNs, nothing to install)
- Tailwind CSS (cdn.tailwindcss.com) for layout and spacing classes.
- Lucide icons (unpkg) and Font Awesome (cdnjs).
- Google Fonts: Inter (body text) and Stack Sans Headline (headings).

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
