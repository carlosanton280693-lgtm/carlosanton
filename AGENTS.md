# AGENTS.md

## Architecture

This is a single static HTML file (`index.html`) with inline `<style>` and `<script>` blocks — there is no build pipeline, bundler, or framework. `netlify.toml` publishes the repository root as-is.

The page behaves like a single-page app: all content sections ("Inicio", "Sobre mí", "Experiencia", "Skills", "Background", "Contacto") are `<div class="tab-pane">` elements that live in the DOM simultaneously. A small script toggles the `.active` class on the matching pane and nav link when a `.tab-link` element is clicked, so navigation never triggers a full page reload or changes the URL.

## Key directories/files

- `index.html` — the entire site: markup, CSS (design tokens in `:root`), and the tab-switching + particle-background JS.
- `netlify.toml` — static publish configuration (`publish = "."`).

## Conventions

- Design tokens (colors, fonts) are defined as CSS custom properties in `:root` at the top of the `<style>` block. Reuse those variables rather than hardcoding colors/fonts.
- Section IDs (`inicio`, `about`, `experience`, `skills`, `education`, `contact`) are referenced by `data-tab` attributes on nav links — keep these in sync if renaming a section.
- The hero particle animation respects `prefers-reduced-motion` and skips `requestAnimationFrame` looping when set.

## Non-obvious decisions

- No framework/build step was introduced despite the platform defaulting to templates, because the user supplied a complete, working static HTML page — wrapping it in a framework would have added complexity without benefit.
- Content is bilingual in labeling (Spanish tab names like "Inicio", "Sobre mí") while body copy is in English; this was preserved from the original request as-is.
