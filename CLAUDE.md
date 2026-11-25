# CLAUDE.md

Guidance for Claude (and any collaborator) working on this repository.

## What this is

Carolina Camelo's personal website, built with **Quarto**. Two main sections:

- **Illustration & Communication**: image-led portfolio of scientific illustration, graphics, outreach and communication work. This is the priority section; the site supports a move into scientific illustration / visual & science communication roles.
- **Science**: research profile (postdoc at ISTA, Heisenberg group, "Morphogenesis in Development"; ascidian *Phallusia* embryo cell–cell adhesion and geometry), publications, experience.

See `PLAN.md` for goals, site map, phases and open decisions. Keep `PLAN.md` up to date when decisions are made or phases finish.

## About the owner (how to collaborate)

- Carolina is a developmental cell biologist and illustrator, **not a web developer**. She is new to Python and to coding workflows.
- Explain steps in plain language. When she has to run a command, give the exact command and say what it does.
- Prefer solutions she can maintain herself: Markdown, YAML front matter, copying a folder. Avoid custom JavaScript, build tooling, or R/Python code in pages unless clearly worth it.
- She has a strong visual eye. Propose design options and let her choose; don't impose a generic look.

## Notes on the setup

- Only `.qmd` files become pages (`render: "**/*.qmd"` in `_quarto.yml`), so `PLAN.md` and `CLAUDE.md` are never published.
- Anything whose name starts with `_` is ignored by Quarto (e.g. `_project-template/`, `_originals/`).
- Yellow `::: {.todo}` boxes mark placeholder content; delete each box once its content is filled in. Before launch, search the repo for `TODO` (also in `_quarto.yml` links).
- Portfolio content came from Carolina's portfolio PDF (Sept 2026). Project text is her own wording; keep it that way unless she asks for edits.
- **Unpublished work is hidden with `draft: true`** in a project's front matter. `draft-mode: gone` in `_quarto.yml` means drafts are not built at all. Currently hidden until the authors agree: the three Kizenko et al. *Nature Genetics* review figures, Singaraju et al. (*NCB*, under revision), the Kapoor et al. epiboly schematic, and the Jovic ascidian stages. These draft folders are also listed in `.gitignore` so their images never reach the public GitHub repo; remove the line there when one is cleared. Only switch one to `draft: false` when Carolina confirms permission.
- **Do not publish the UC Santa Cruz science-writing course pieces** (feature pitch, news story, press release, LinkedIn post, Instagram carousel about the Coculla et al. *Science* 2025 fruit-fly study): the interviewed author asked that they not be shared publicly. They exist only in Carolina's application PDFs.
- The CV PDF (`assets/cv/carolina-camelo-cv.pdf`) is pages 2–3 of her job application. Never publish the cover letter or the references page (they contain other people's contact details).
- Reusable CSS classes in `styles/theme.scss`: `.hero`, `.doors` / `.door` (clickable cards; `.doors.three` for three columns), `.project-meta`, `.timeline` with `.when`, `.todo`.

## Commands

```bash
quarto preview          # live preview in the browser while editing (run from repo root)
quarto render           # build the full site into _site/
quarto publish gh-pages # publish to GitHub Pages (once set up)
quarto check            # verify the Quarto installation
```

## Structure

```
_quarto.yml                     # site config: navbar, theme, footer, site-wide options
index.qmd                       # homepage
about.qmd                       # bio, contact, CV
illustration/index.qmd          # portfolio grid (listing over projects/)
illustration/projects/<slug>/   # one folder per portfolio piece: index.qmd + images
science/index.qmd               # science landing page
science/research.qmd
science/publications.qmd        # listing built from publications.yml
science/publications.yml
path.qmd                        # "My path" (CV-style timeline), under the About menu
assets/img/, assets/cv/         # shared images, CV PDF
styles/theme.scss               # custom colours, fonts, styles
```

## Conventions

### Adding a portfolio piece

Copy the folder `illustration/_project-template/` into `illustration/projects/` and rename it `YYYY-short-slug`. Its `index.qmd` starts like this:

```yaml
---
title: "Short, descriptive title"
date: 2026-10-01
description: "One sentence shown on the grid card."
image: cover.webp            # grid thumbnail, in the same folder
image-alt: "What the image shows."
categories: [Illustration, Outreach]
featured: false              # true = also shown on the homepage (keep exactly 3 featured)
client: "Who it was for (optional)"
---
```

Body: images (`figure-1.webp`, `figure-2.webp`… with captions and alt text, grouped with `{group="gallery"}`), then the story (optionally as **The brief → My approach → The outcome**), then a `::: {.reference}` block with the citation/DOI link. Covers are 1200 × 900 px (4:3) with the artwork centred on white; the grid shows them uncropped.

Allowed categories (tags shown on cards; keep this list consistent; extend it here first): `Illustration`, `Infographic`, `Data visualisation`, `Outreach`, `Animation`, `Editorial`, `Poster`, `Volunteer`.

### Portfolio sections and the moving strip

- The portfolio page (`illustration/index.qmd`) has three sections, filled from each project's `portfolio-section:` field: `2d` (2D Illustration), `3d` (3D & Animation), `design` (Communication Design). The field can't be called `section` (reserved by Quarto).
- A section with no projects hides itself (CSS rule `.portfolio-section:not(:has(.quarto-grid-item))`). When the first `3d` piece is added, also uncomment the "3D & Animation" entry in the navbar menu in `_quarto.yml`.
- The moving strip at the top of the portfolio page shows every project with `showcase: true`. Template: `illustration/_filmstrip.ejs`; styles and speed in `styles/theme.scss` (`.filmstrip`). It stops on hover and is static for visitors with "reduce motion" on.
- `featured: true` is separate: the 3 pieces on the homepage.

### Adding a publication

Add an entry at the top of `science/publications.yml`:

```yaml
- title: "Paper title"
  author: "Camelo C, Coauthor A, Heisenberg CP"
  journal: "Journal name"
  date: 2026-01-01
  path: https://doi.org/xx.xxxx/xxxxx
```

### Images

- Web exports only: max 2000 px long edge (covers ~1200 px), WebP preferred, aim < 400 KB.
- Consistent cover aspect ratio across the portfolio grid.
- Every image needs meaningful alt text.
- Never commit full-resolution originals or source files (`.procreate`, `.ai`, `.psd`, `.afdesign`, `.tif`, `.czi`). Keep them in `_originals/` (git-ignored) or outside the repo.
- If an image is too large, offer to resize/convert it rather than committing it as-is.

### Content & rights

- **Do not publish unpublished research data** (EM images, segmentations, expression data, unpublished findings) unless Carolina confirms her PI has approved it.
- Journal figures: respect the licence (CC-BY → cite source; otherwise ask Carolina how to handle it).
- Client/institute work: credit the client; confirm permission to show it.
- Never invent publications, dates, affiliations, or project details. Use a clearly marked `TODO:` placeholder and ask.

### Writing style

- English, warm and clear, first person ("I").
- Science pages: plain language first, technical detail second. A non-specialist should understand the first paragraph.
- Short paragraphs; let the images carry the portfolio.

### Design

- Custom theme in `styles/theme.scss` on top of a Bootswatch base; colours and fonts defined as SCSS variables at the top of the file.
- Must work well on mobile. Check the grid and image pages at phone width.
- Accessibility: sufficient colour contrast, alt text, descriptive link text.

## Git

- Don't commit `_site/`, `.quarto/`, `_freeze/` (unless code execution is added later), `_originals/`, or `.DS_Store`.
- Small, descriptive commits (e.g. "Add 2026 embryo poster to portfolio").
- Ask before pushing or publishing.
