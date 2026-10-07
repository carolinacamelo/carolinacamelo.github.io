# Website Plan — Carolina Camelo

A personal website built with **Quarto** that brings together two sides of my work:

1. **Science**: research profile, projects, publications, experience.
2. **Illustration & Communication**: an image-led portfolio of scientific illustration, graphics, outreach and communication projects.

The site should read as *one person, one voice*: a scientist who visualises and communicates science. It is also a key tool for my move toward scientific illustration / visual communication / science communication roles, so the portfolio should be the strongest part.

---

## 1. Goals

| Goal | What success looks like |
|---|---|
| Show my portfolio | A hiring manager can see my best 6–10 pieces in under a minute, open any piece large, and read the story behind it. |
| Establish scientific credibility | Research, publications and experience are easy to scan, with links to papers. |
| Make me easy to contact | Email / LinkedIn / ORCID / CV PDF reachable from every page. |
| Be easy for me to maintain | Adding a new illustration or paper means copying a folder or adding a few lines of YAML. No coding needed. |
| Look like *my* work | A visual identity that matches my illustration style, not a default template. |

**Audiences, in priority order:** (1) recruiters and editors in scicomm, illustration and publishing (e.g. journals, institutes, agencies); (2) scientists and collaborators; (3) the curious public.

---

## 2. Site map

```
Home (index)
├── Illustration & Communication   ← portfolio grid, filterable by category
│   └── [one page per project]     ← large images + short story (brief, process, outcome)
├── Science
│   ├── Research                   ← current & past projects, in plain language
│   ├── Publications               ← list with links (DOI / PDF)
│   └── Experience                 ← academic path, timeline-style
├── About                          ← bio, photo, what I offer, contact, CV download
└── (optional, later) Notes / Blog
```

**Navbar:** `Illustration & Communication · Science · About` + icons (email, LinkedIn, ORCID, Bluesky/Instagram if used).

**Homepage:** short intro line + portrait or a signature illustration, then two big "doors" into the two sections, then 3–4 featured portfolio pieces.

---

## 3. Folder structure

```
Website/
├── _quarto.yml              # site config: navbar, theme, footer
├── index.qmd                # homepage
├── about.qmd
├── illustration/
│   ├── index.qmd            # portfolio grid (Quarto listing)
│   └── projects/
│       └── 2026-embryo-cleavage-poster/
│           ├── index.qmd    # one project page
│           ├── cover.webp   # thumbnail shown in the grid
│           └── *.webp       # further images
├── science/
│   ├── index.qmd            # Science landing page
│   ├── research.qmd
│   ├── publications.qmd     # listing built from publications.yml
│   ├── publications.yml
│   └── experience.qmd
├── assets/
│   ├── img/                 # portrait, logo, favicon, social card
│   └── cv/carolina-camelo-cv.pdf
├── styles/
│   ├── theme.scss           # colours, fonts, custom styles
│   └── theme-dark.scss      # optional dark mode
├── .gitignore
├── CLAUDE.md
└── PLAN.md
```

Original, full-resolution artwork (Procreate, Illustrator, Affinity, TIFFs) stays **outside** the repo or in an ignored `_originals/` folder. Only web-sized exports go into the site.

---

## 4. Key technical choices

- **Quarto website project** (`project: type: website`). Pages are plain Markdown (`.qmd`), so no Python or R code is needed to run the site.
- **Portfolio = Quarto listing** (`type: grid`, `categories: true`) built automatically from each project folder's front matter (`title`, `date`, `image`, `categories`, `description`). Adding a piece means adding a folder.
- **Lightbox** (`lightbox: true`) so every image opens large on click; images on a project page can be grouped into a gallery.
- **Portfolio categories** (first pass): `Illustration`, `Infographic`, `Data visualisation`, `Outreach`, `Animation`, `Editorial`, `Poster`.
- **Publications** from a single `publications.yml` (title, authors, journal, year, DOI link), shown as a table or list listing, newest first.
- **Theme:** Bootswatch base (e.g. `litera` or `cosmo`) plus a custom `theme.scss` with my own palette and fonts (Google Fonts). Light mode first, dark mode optional.
- **Hosting:** GitHub repo + **GitHub Pages**, published with `quarto publish gh-pages` (simplest) or a GitHub Action later. Netlify is a fine alternative. Custom domain (e.g. `carolinacamelo.com`) once the site is ready.
- **No tracking cookies** by default. If I want visitor stats later, use something privacy-friendly (e.g. Plausible / GoatCounter).

---

## 5. Image guidelines

- Export at **max 2000 px on the long edge** (thumbnails/covers ~1200 px), **WebP** (or JPEG at quality ~80). Aim for **< 400 KB** per image.
- Covers in a **consistent aspect ratio** (e.g. 4:3 or 1:1) so the grid looks tidy.
- **Alt text for every image** (what it shows and why it matters), for accessibility and search.
- Watermark: optional, small. A visible credit line in the caption is usually enough.
- **Rights check before posting:**
  - Figures published in journals: check the licence (CC-BY is fine with citation; otherwise ask the publisher or show a cropped/redrawn version).
  - Unpublished data (e.g. EM images, segmentations, cadherin results): **check with the PI before showing.**
  - Client or institute work (e.g. ISTA Communications): confirm I may show it, and credit the client.

---

## 6. Content checklist (what I need to gather)

**About / general**
- [ ] Short bio (1 sentence for homepage, ~150 words for About)
- [ ] Professional portrait photo
- [ ] "What I do / what I offer" lines (illustration, figures, graphical abstracts, outreach, editing…)
- [ ] CV as PDF
- [ ] Links: email, LinkedIn, ORCID, Google Scholar, social accounts

**Science**
- [ ] Plain-language summary of the current postdoc project (Phallusia embryo cell–cell adhesion & geometry), with one image I'm allowed to show
- [ ] PhD project summary
- [ ] Publication list with DOIs
- [ ] Education & positions (Biochemistry BSc/MSc → PhD → ISTA postdoc, Heisenberg group)
- [ ] Talks, posters, awards, teaching, service (e.g. Postdoc Association, Postdoc Retreat 2026 co-organiser)

**Illustration & Communication** (per piece)
- [ ] 6–10 strongest pieces to start (quality over quantity)
- [ ] For each: title, year, category, client/context, tools used
- [ ] 2–4 sentence story: *the brief → my approach → the outcome*
- [ ] Optional process images (sketch → final), which recruiters love
- [ ] Cover image + full-size images, exported per the guidelines above
- [ ] Communication work without images (courses, job shadowing at ISTA Communications, outreach events) can go on a project page or the About page

---

## 7. Phases

| Phase | What | Done when |
|---|---|---|
| **0. Setup** | Install Quarto + VS Code (or Positron), create GitHub repo, `git init`, add `.gitignore` | `quarto preview` shows a blank site |
| **1. Skeleton** | `_quarto.yml`, navbar, all pages as placeholders, listing for portfolio and publications | Every link works, with placeholder content |
| **2. Visual identity** | Palette, fonts, logo/monogram, favicon, homepage layout | Site looks like *me*, on desktop and phone |
| **3. Portfolio** | First 6–10 projects with covers, stories, lightbox | Portfolio grid is complete and filterable |
| **4. Science** | Research text, publications YAML, experience timeline | Science section complete |
| **5. About & polish** | Bio, CV, contact, social card image, page descriptions (SEO), alt text check, link check | Ready for feedback |
| **6. Feedback** | Show to 2–3 people (a scientist, a designer/communicator, someone outside science) | Notes addressed |
| **7. Launch** | Publish to GitHub Pages, connect custom domain, add link to LinkedIn/ORCID/email signature | Site is live |
| **Ongoing** | Add new pieces as they're made; review once a month | — |

---

## 8. Open decisions

- [ ] **Domain name**: e.g. `carolinacamelo.com`, `.art`, `.science`? (check availability; ~€10–20/year)
- [ ] **Hosting**: GitHub Pages (free, recommended) vs Netlify
- [ ] **Homepage emphasis**: portfolio-first (recommended for the job search) vs equal weight
- [ ] **Language**: English only, or also a Portuguese version later?
- [ ] **Blog/Notes section**: now, later, or never?
- [ ] **Contact**: plain email link (simplest) vs a contact form (needs a service like Formspree)
- [ ] **Visual identity**: palette and fonts, ideally derived from my own illustrations
