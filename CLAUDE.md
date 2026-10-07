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
science/experience.qmd
assets/img/, assets/cv/         # shared images, CV PDF
styles/theme.scss               # custom colours, fonts, styles
```

## Conventions

### Adding a portfolio piece

Create `illustration/projects/YYYY-short-slug/index.qmd`:

```yaml
---
title: "Short, descriptive title"
date: 2026-10-01
description: "One sentence shown on the grid card."
image: cover.webp            # grid thumbnail, in the same folder
image-alt: "What the image shows."
categories: [Illustration, Outreach]
client: "Who it was for (optional)"
tools: [Procreate, Illustrator]
---
```

Body structure: **The brief → My approach → The outcome**, plus images (with alt text and captions). Group images into a lightbox gallery with `{group="gallery"}`.

Allowed categories (keep this list consistent; extend it here first): `Illustration`, `Infographic`, `Data visualisation`, `Outreach`, `Animation`, `Editorial`, `Poster`.

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
