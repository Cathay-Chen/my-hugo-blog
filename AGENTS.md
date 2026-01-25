# Repository Guidelines

## Project Structure & Module Organization
- `content/` holds site content (posts, pages). Use Hugo front matter and keep assets alongside content when needed.
- `themes/` contains the active Hugo theme and any theme customizations.
- `archetypes/` defines templates for new content types.
- `config.toml` is the main Hugo configuration.
- `resources/` and `public/` are Hugo-generated artifacts (cache/output); avoid manual edits.
- `node_modules/` and `package.json` are for CSS tooling (PostCSS/Tailwind).

## Build, Test, and Development Commands
- `hugo serve` runs the local dev server with live reload.
- `hugo` builds the site into `public/`.
- CSS tooling is managed via `postcss`, `tailwindcss`, and `autoprefixer` in `package.json`. If you need a custom pipeline, add scripts there and document them.

## Coding Style & Naming Conventions
- Content filenames in `content/` should be short, kebab-case (e.g., `my-first-post.md`).
- Prefer clear, sentence-case titles in front matter.
- Keep Markdown formatting consistent: 2 blank lines between major sections, no trailing whitespace.
- Any theme overrides should be small and localized to `themes/` or a project-specific override directory.

## Testing Guidelines
- No automated test framework is currently configured. Treat visual checks as the primary verification.
- Before a PR, run `hugo serve` and spot-check pages you modified.

## Commit & Pull Request Guidelines
- Commit messages in history are short and direct (e.g., `add post ...`, `update about me`). Follow this style.
- PRs should include: a concise summary, list of affected pages/paths, and screenshots or links to local preview for visual changes.
- Link related issues if applicable.

## Security & Configuration Tips
- Avoid committing secrets; use site params in `config.toml` for public configuration only.
- When updating themes or tooling, note version changes in the PR description.
