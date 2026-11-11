# AGENTS.md: Ishaan Marwaha ePortfolio

Personal ePortfolio for Ishaan K. Marwaha (Computer Engineering, Georgia Tech), built for ECE 1100 and
kept as a long-term, recruiter-facing site. It is hosted on **GitHub Pages**: every push to `main`
redeploys the live site within 1–2 minutes.

## Stack and structure

Plain static HTML and CSS. **There is no build step, framework, or generator.** Edit the `.html` files directly.

```
index.html          Home: hero welcome statement, Work Experience cards, Recent Projects cards, Publications
about.html          About Me narrative (left) + Education and Skills cards (right)
experience.html     One <section> per role (Medi-Loc, Bhasin Lab, ViTAL Lab, WhizLearning Kids)
projects.html       One <section> per project (RISC-V, TurboSentry, Fusor) + commented-out Discovery Project
resume.html         Resume shown as an image (assets/img/resume.png) + PDF download buttons
career-goals.html   Long-term vision + "Where I'm headed" card, 5-step roadmap, skills cards
contact.html        Email, LinkedIn, resume download, location
assets/css/style.css   Single shared stylesheet (all pages)
assets/img/            Images (jpg/png/svg)
assets/docs/Marwaha_Resume.pdf   The downloadable resume
```

Every page repeats the same `<header>` (nav), `<footer>`, and small nav-toggle `<script>`. There are no
includes, so **any change to the nav or footer must be made in every `.html` file.**

## Assignment requirements (do not break these)

The course requires: a welcome statement (Home), an About Me page, a resume that is easy to view **and**
download, a Career Goals page (aspirations plus steps to get there), and technical projects including a
**Discovery Project Feature**. The site must also keep **≥ 1000 words** total and **≥ 5 images**, with
outside images credited. Do not remove or rename these pages without being asked.

## Adding a new page or tab

1. Copy an existing simple page (e.g. `contact.html`) to keep the full `<head>`, header, footer, and script.
2. Set `<title>` to `Page Name | Ishaan Marwaha` and update the meta description.
3. The page header is the H1 only. **No eyebrow and no subtitle under it**, and the H1 text must exactly
   match the nav label:
   ```html
   <div class="page-head"><div class="container">
     <h1>Achievements</h1>
   </div></div>
   ```
4. Add the nav link to **all** pages, in the same position in each. Mark the current page with
   `aria-current="page"` on that page only. Current nav order:
   Home, About, Experience, Projects, Resume, Career Goals, Contact.
   (Planned: Achievements goes between Projects and Resume.)
5. If the nav gets crowded on desktop, raise the `@media (max-width: 820px)` breakpoint in `style.css`
   so it collapses to the Menu button sooner. Check that nothing wraps at roughly 900–1100px wide.

## Content patterns

### Detail section (Experience and Projects pages)
Sections alternate background: add `class="alt"` to every other `<section>`. Use a two-column layout
when there is an image, and `container prose` (single column) when there is not. Alternate the image side
(right, left, right…) on the Projects page.

```html
<section id="short-id" class="alt">
  <div class="container grid-2" style="align-items:center">
    <div>
      <span class="eyebrow">Aug 2026 – Present</span>
      <h2>Project or Organization Name</h2>
      <h3>The Problem</h3>   <!-- Projects use Problem / Process / Outcome headings -->
      <p>…</p>
      <h3>The Process</h3>
      <p>…</p>
      <h3>The Outcome</h3>
      <p>…</p>
    </div>
    <figure><img src="assets/img/name.jpg" alt="Descriptive alt text">
      <figcaption>Short caption.</figcaption></figure>
  </div>
</section>
```
Experience entries use the same shell, but put `<div class="meta">Role title</div>` under the H2, then one
short intro sentence and a `<ul>` of accomplishment bullets.

### Summary card (Home page grids)
```html
<article class="card">
  <h3>Name</h3>
  <div class="meta">Organization or role<span class="date">May 2025 – Present</span></div>
  <p>One-sentence summary.</p>
  <a class="more" href="experience.html#short-id">Read more →</a>
</article>
```
Cards sit in `<div class="grid-3">` (3 per row on desktop, stacked on mobile). The `.date` span keeps the
date on its own line with no extra gap. Do not use `<br>` or a new `<p>` for it.

### Other components
- Buttons: `btn btn-navy` (primary), `btn btn-line` (secondary), `btn btn-gold` / `btn btn-outline` (hero only).
- Narrow figures (small or square images): `<figure class="fig-narrow">`.
- Career Goals timeline: `<ol class="roadmap">` with `<li><span class="dot"></span><div>…</div></li>` items.
  It is horizontal on desktop and vertical on mobile.

## Style rules (settled with the owner)

- **Dates:** `Mon YYYY – Mon YYYY` or `Mon YYYY – Present`, with an en dash and spaces (`&ndash;` or `–`).
  Never use a hyphen. On detail sections the date is the only eyebrow (no category label such as "Research ·").
- **No skill tags or pills.** Mention tools and skills in the body text instead.
- **No subtitles** under page H1s, and no gray lead or intro sentences under Home page section headings.
- **Medi-Loc title:** "Co-Founder & Lead Developer" (Home and Experience). "Lead hardware developer" is
  acceptable in hardware-focused prose. Never use "CEO". The company is **Medi-Loc LLC** and the product is **Medi-Zero**.
- **Image credits:** any image not made by Ishaan gets a short credit in the caption, e.g.
  `Image: Pandey et al., <em>Journal of Sensors</em> (2022), <a href="https://doi.org/…">doi:…</a>`.
  Do not write a full MLA or APA citation.
- **Tone:** first person, professional, concise. Proofread everything; spelling and grammar are graded.
- **Do not invent facts** (dates, numbers, awards, tools used). If information is missing, ask the owner
  rather than writing placeholder text. Do not leave yellow `todo` boxes on published pages.
- **Privacy:** the location is "Atlanta, GA" only. Never add a street address.

## Images

- Save into `assets/img/` with short lowercase names (`fusor.jpg`). Resize to about 1200–1400px wide,
  using JPG for photos and PNG for screenshots or plots.
- Always write descriptive `alt` text.

## Updating the resume

Replace `assets/docs/Marwaha_Resume.pdf` (keep the filename), then regenerate the preview image:
```
pdftoppm -png -r 150 -singlefile assets/docs/Marwaha_Resume.pdf assets/img/resume
```

## Discovery Project Feature

It is commented out in `projects.html` (`<!-- DISCOVERY PROJECT FEATURE … -->`) until the project is done.
To publish it, uncomment it and keep it as the **first** section on the Projects page. Then replace every
`todo` / `todo-block` element with real content and swap `discovery-placeholder.svg` for a real photo.
Requirements: **≥ 400 words**, Problem / Process / Outcome / What I Learned & What's Next headings, and
**at least one photo or video taken by Ishaan**. Optionally add a card for it on the Home page.
Re-check the section-background alternation (`class="alt"`) after inserting it.

## Before committing

- Open the changed pages locally at desktop width and at phone width (about 390px). Check that there is
  no horizontal scrolling, no wrapped nav, and no dates breaking across lines.
- Confirm every link, anchor (`page.html#id`), and image path exists. Paths are case-sensitive on GitHub Pages.
- Search for `todo` and make sure none are visible (inside the Discovery comment is fine).
