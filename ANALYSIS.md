# Initial Analysis — Portfolio Site (Jekyll)

Reference: [live site](https://gaborekg.github.io/lead-portfolio/) / [repo](https://github.com/afknapping/gabor-lead-portfolio)

## Reference site — what it is

- Single-page, one-scroll portfolio, no routing/pages beyond `index.html` + `legal.html`
- **Not Jekyll** — plain static HTML/CSS/JS, deployed via `gh-pages` with `.nojekyll`
- All content **hardcoded inline in `index.html`** — no data files, no templating, no build step
- Sections: header/nav → hero ("grow-sentence" intro) → Experience & Impact (5 entries) → Speaking (nested inside last entry) → Contact footer
- Each experience entry: company, role, dates, logo, one-line summary, `<details>` "Read the summary" reveal with Company / Key Outcomes / Scope (/ Speaking) blocks
- No projects section, no blog, no timeline view, no filtering

## Notable design/UX patterns worth reusing

- **Design tokens**: 6 CSS custom properties (`--bg`, `--text`, `--accent`, `--heading`, `--muted`, `--rule`) drive entire theme — swap the block, whole site re-themes
- Light/dark theme: mirrors `prefers-color-scheme` by default, manual override saved to `localStorage`, applied pre-paint (no flash), animated cross-fade on toggle
- Self-hosted **IBM Plex Mono** variable-weight font, typography tokens split into separate `typography.css`
- "Grow-sentence" progressive disclosure: inline `<button>` triggers reveal hidden `<span>` text — expands the narrative without a modal/page jump
- `<details>/<summary>` for per-entry expand, semantic + no-JS fallback
- Anchor links between sections (`#exp-beatsquares`) auto-open the target's `<details>` and scroll to it
- Accessible: `aria-expanded`, `visually-hidden` real `<h1>`, contrast-checked dark palette (AAA body text)
- Portrait doubles as the theme toggle (moon overlay animation) — playful, low-chrome UI control

## What's fundamentally different about the ask

- Needs to be **data-driven**, not hand-written HTML per entry — two distinct content types:
  1. **CV / professional experience** (roles, dates, companies — same shape as reference site)
  2. **Projects** (personal/freelance work, not tied to an employer)
- Needs a **merged timeline view** interleaving both datasets by date
- Needs **individual views** per dataset (CV-only, Projects-only)
- Needs a **blog**
- Must be **vanilla Jekyll on GitHub Pages** (no custom build pipeline, no JS framework, use what GH Pages' whitelisted plugin set supports)

## Proposed Jekyll data model

- `_data/cv.yml` — array of experience entries (company, role, start/end date, logo, summary, outcomes[], scope, tags)
- `_data/projects.yml` — array of projects (title, start/end date or single date, role, description, links, tags, cover image)
- Shared schema fields between both (`title`/`subtitle`, `date_start`, `date_end`, `summary`, `type: cv|project`) so they can be normalized into one sortable list in a Liquid include
- `_posts/` — standard Jekyll blog posts (date-prefixed `.md` files) for the blog collection
- Optional: `_projects/` as a real Jekyll **collection** instead of a data file if each project should get its own permalink/page (recommended if projects need detail pages, e.g. case studies)

## Proposed page/URL structure

- `/` — home/hero, short intro, maybe latest 2–3 timeline items + latest blog post
- `/timeline/` — merged CV + Projects, reverse-chronological, filterable by type via CSS/JS (no reload)
- `/cv/` — CV-only view (mirrors reference site's Experience & Impact section)
- `/projects/` — Projects-only view (grid or list)
- `/projects/<slug>/` — individual project detail page (if using a collection)
- `/blog/` — post index
- `/blog/<slug>/` — individual post (Jekyll default `_posts` permalink)

## Templating approach

- One Liquid include (`_includes/timeline-entry.html`) rendering either a CV or project entry from the normalized fields — reused across `/timeline/`, `/cv/`, `/projects/`
- Build the merged, sorted list either:
  - at build time via Liquid (`sort` + `concat` two arrays — fully static, zero client JS required), **or**
  - client-side by rendering both datasets to JSON and merging/sorting in a small vanilla JS file if interactive filtering/animation is wanted
- Recommend **Liquid-side merge for the base render** (works with JS disabled, fast, simple) + optional light JS just for type-filter toggling (no framework needed, same spirit as reference site's vanilla approach)

## Design language — keep vs. change

- **Keep**: token-driven theme system, light/dark toggle mechanic, monospace type choice (or pick own font), accessible expand/collapse pattern, minimal chrome
- **Change/extend**: needs a real nav (Home / Timeline / CV / Projects / Blog) since it's no longer one-page; needs a type indicator/badge per timeline entry (CV vs Project) with distinct accent or icon; blog needs its own list/detail layout not present in reference at all

## Open questions to resolve before building

- Do projects need individual detail pages (→ Jekyll collection) or is a list with expand-in-place enough (→ `_data/projects.yml`)?
- Should the merged timeline support filtering (CV only / Projects only / All) as a toggle, or is that redundant with having separate `/cv/` and `/projects/` pages?
- Blog: categories/tags needed? Comments (e.g. Giscus)? RSS feed (`jekyll-feed`, GH-Pages-whitelisted)?
- Reuse reference site's visual identity (IBM Plex Mono, orange/navy palette) or establish a new one?
- Domain/repo: deploy to `afknapping.github.io` root (user/org page) — confirms this repo is the target, single Jekyll site, no `baseurl` needed
