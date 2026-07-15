# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static personal academic homepage for Ulrik Sartipy (cardiac surgeon / researcher at Karolinska), served via GitHub Pages at http://ulriksartipy.github.io. Deployment is automatic: pushing to the `master` branch of `origin` (github.com/ulriksartipy/ulriksartipy.github.io) publishes the site. There is no build step, package manager, test suite, or local dev server — open `index.html` directly in a browser to preview.

## Layout

- `index.html` — the entire single-page site: header/contact, About, Education, **Selected publications** table (2015–), Projects (research program prose), and a link out to the full publications list.
- `content/publication_list.html` — the complete chronological publication list (`<ol reversed>` in `#list2`), newest first. This is a standalone page with its own `<head>` and Google Analytics tag; it references CSS via `../css/`.
- `css/` — `skeleton.css` + `normalize.css` (the Skeleton framework, do not edit), `academicons.css` (icon font for scholarly-profile links), and `custom.css` (site-specific overrides — edit this for styling).
- `js/site.js` — jQuery-based UI behavior: docked-navbar-on-scroll, smooth anchor scrolling, and the "More" nav popover. Loaded after jQuery 3.5.1 (CDN).
- `fonts/`, `images/` — academicons webfont files and profile photo / favicon.

## Editing publications — the key recurring task

Publications live in **two** independent places that must be kept consistent. Most commits to this repo are publication updates.

1. **Full list** — `content/publication_list.html`: add a new `<li>` at the **top** of the `<ol>` inside `#list2`. Follow the exact existing format:
   `Authors (with <strong>Sartipy U</strong> bolded). Title. Journal Year;Vol:Pages doi: DOI PMID: PMID <a href="https://www.ncbi.nlm.nih.gov/pubmed/PMID" class="uri">https://www.ncbi.nlm.nih.gov/pubmed/PMID</a>`
   Also bump the "updated YYYY-MM-DD" date in both the `#list-of-publications-updated-...` div id and its `<h3>`.

2. **Selected publications table** — `index.html` (`#selected_publ`): only major/high-profile papers go here. Each is a `<tr>` with five `<td>`s: citation (author list with `<b>Sartipy U</b>`), DOI/PubMed links + a Dimensions badge (`__dimensions_badge_embed__` span carrying `data-doi`), an Altmetric donut (`altmetric-embed` div with `data-doi`), an Editorial link (or ` - `), and a PlumX badge (`plumx-plum-print-popup` with `data-doi`). Copy an existing `<tr>` and replace the DOI/PMID/citation — every third-party badge is keyed off the DOI, so set it in all four places.

## External dependencies (all CDN, loaded at runtime)

jQuery, FontAwesome, academicons, and three citation-metrics widgets — Dimensions (`badge.dimensions.ai`), Altmetric (`d1bxh8uas1mnw7.cloudfront.net/assets/embed.js`), and PlumX (`cdn.plu.mx/widget-popup.js`). Badges render only when served over http(s) and resolve by DOI, so they will look empty when viewing a `file://` copy of a just-added entry — that is expected, not a bug.

## Conventions

- Author self-citations are bolded: `<b>Sartipy U</b>` in `index.html`, `<strong>Sartipy U</strong>` in `content/publication_list.html`.
- Match the surrounding two-space HTML indentation; note that a few existing rows use tab indentation — prefer the dominant two-space style for new content.
