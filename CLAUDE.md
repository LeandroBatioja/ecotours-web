# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

EcoTours Web is a static eco-tourism website for Ecuador built with **Astro 5** and **TailwindCSS 4**. All content is in Spanish. The site showcases Ecuadorian destinations, eco-experiences, and a blog.

## Commands

| Command | Action |
|---------|--------|
| `npm run dev` | Start dev server at `localhost:4321` |
| `npm run build` | Build production site to `./dist/` |
| `npm run preview` | Preview production build locally |

No test framework is configured.

## Architecture

- **Static Site Generation (SSG)** — all pages pre-built at build time, no server-side rendering
- **File-based routing** via `src/pages/` (Astro convention)
- **Data layer** uses plain JS arrays in `src/data/` (destinos.js, experiencias.js) — no CMS or database
- **Dynamic routes** (`[slug].astro`) use `getStaticPaths()` to generate pages from data arrays
- **Blog posts** are Markdown files in `src/pages/blog/` using frontmatter + BlogPostLayout
- **Maps** use Leaflet.js with OpenStreetMap tiles loaded via CDN inline scripts in EcoMap component
- **Dark mode** is hardcoded on (`class="dark"` on html element) with `dark:` Tailwind variants

## Key Conventions

- **Layouts**: `BaseLayout.astro` (wraps all pages with Navbar/Footer) and `BlogPostLayout.astro` (extends BaseLayout with prose typography)
- **Custom colors**: `forest` (#1E7F43), `ecoBlue` (#1FA2B8), `ecoOrange` (#F59E0B) defined in tailwind.config.mjs
- **Font**: Inter via `font-sans`
- **Images**: External URLs (Unsplash placeholders), no local image optimization
- **TailwindCSS** is integrated via `@tailwindcss/vite` plugin in astro.config.mjs (not as an Astro integration)
- **TypeScript** strict mode via `astro/tsconfigs/strict`

## Adding Content

- **New destination**: Add object to `src/data/destinos.js` array with slug, title, location, hero, description, gallery, video, lat, lng
- **New experience**: Add object to `src/data/experiencias.js` array with slug, title, hero, gallery, video, description
- **New blog post**: Create `.md` file in `src/pages/blog/` with `layout: ../../layouts/BlogPostLayout.astro` frontmatter
