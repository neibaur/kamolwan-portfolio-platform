# AGENTS.md

Guidance for AI coding agents working in this repository.

## Repository Purpose

This is the source repository for [kamolwan.com](https://kamolwan.com), Kamolwan (Joy) Paramee's Hugo Blox portfolio. It is a static Hugo portfolio site, not a Python dashboard, Astro app, or monorepo. Keep changes lightweight and appropriate for a personal accounting and finance portfolio.

Production is generated from this repo and deployed by GitHub Actions to `kamolwan/kamolwan.github.io`, which serves `kamolwan.com`.

## Branch Policy

- `main` is the production trunk branch. Treat it as always deployable.
- `dev` is only for experiments and should not be assumed to represent production.
- Prefer trunk-based development with small, atomic commits.
- Keep unrelated content, layout, dependency, and workflow changes in separate commits.

## AI Agent Working Rules

1. Inspect existing files before modifying.
2. Make the smallest safe change.
3. Preserve existing behavior unless asked to change it.
4. Do not overwrite user work without checking diffs.
5. Keep generated files minimal.
6. Avoid premature abstractions.
7. Do not invent external credentials, services, APIs, or paid tooling.
8. Add TODOs only when useful and specific.
9. Update documentation when setup, behavior, standards, or structure changes.
10. Never commit secrets.
11. Do not remove or simplify custom shortcodes, layouts, or structure unless explicitly instructed.
12. Prefer small, scoped changes over large refactors.

## What To Edit

- Authored content lives in `content/` and `data/authors/me.yaml`.
- Site configuration lives in `config/_default/`.
- Local Hugo Blox overrides live in `layouts/`.
- Local styles and media live in `assets/`.
- Public static downloads live in `static/uploads/`.

Do not edit generated output or vendored dependencies:

- `public/`
- `resources/`
- `.hugo_build.lock`
- `hugo_stats.json`
- `node_modules/`
- `_vendor/` unless explicitly updating Hugo Blox modules

## Hugo Blox Notes

This site uses Hugo Blox plus local custom shortcodes and partials. Do not replace or remove custom shortcodes such as:

- `display_list`
- `bio_grid`
- `landing_anchor`
- `sidebar_button`
- `sidebar_title`

These shortcodes are intentional portfolio building blocks. Preserve them when rewriting copy or moving content.

## Local Validation

For preview:

```bash
hugo server --disableFastRender
```

For a production-style build:

```bash
hugo --gc --minify
```

On Windows, if Hugo cannot access the default user cache, use a repo-local absolute cache path:

```powershell
hugo --gc --minify --cacheDir "$PWD\.hugo-cache"
```

Do not add Python, Astro, database, service-worker, or dashboard-style tooling unless the user explicitly asks for it. Prefer Hugo-native or small Node-based tooling only when it directly improves this static portfolio.

## Content Standards

- Keep portfolio content factual, current, and specific to Joy's accounting, bookkeeping, tax preparation, and business operations background.
- Remove or quarantine Hugo Blox starter/demo content that dilutes the personal brand.
- Use `_drafts/` for archived starter material that should not build into the public site.
- Keep public pages focused on biography, experience, education/certifications, projects, publications, events, and contact paths.
- Do not publish placeholder projects, template posts, sample talks, or sample slides.

## Deployment Context

Production deploys are cross-repo:

1. This repo is built by GitHub Actions.
2. Generated output from `public/` is pushed to `kamolwan/kamolwan.github.io`.
3. `kamolwan/kamolwan.github.io` serves `kamolwan.com`.

Any deployment or workflow change must account for that cross-repo publishing model.

## Definition of Done

A task is complete when:

- Hugo builds locally with `hugo --gc --minify`.
- Local validation commands (if defined) complete successfully.
- Generated output is not committed.
- No secrets are committed.
- Custom shortcodes and Hugo Blox overrides are preserved.
- Content changes are factual, current, and portfolio-specific.
- Documentation is updated when setup, behavior, standards, or structure changes.
- Changes are small, atomic, and reviewable.

## Agent Operations Rails

These rails apply to every AI agent working in this repository and match the
`neibaur-labs/agent-ops` contract. Where another section of this file is
stricter, the stricter rule wins.

- **Commits, not merges.** Agents may commit and push their own work to feature
  branches. Agents never push to `main`, and never merge, approve, or close pull
  requests.
- **Protected paths: agents edit, the maintainer commits.** Agents may edit
  agent-instruction files (`AGENTS.md`, `CLAUDE.md`, and similar), `.github/**`,
  `LICENSE`, and skill directories, but the maintainer commits and pushes those
  changes. The agent keeps them out of its own commits, hands off the exact
  `git add`, `git commit`, and `git push` commands, waits for the maintainer's
  commit, then continues the task.
- **Dependencies.** Agents may add, upgrade, or remove dependencies when a task
  needs it. They make and verify the change, then wait for the maintainer's
  explicit authorization or hand off the commit. Keep dependency changes in
  their own commit, and list each one in the PR description with an exact
  version verified against a current source.
- **Pull request size.** One concern per pull request, or two when they are
  tightly coupled. There is no line cap; the ceiling is 20,000 changed lines,
  excluding lockfiles and generated files.
- **Secrets.** Agents never read, print, or commit secret-bearing files.
- **Labels.** Label agent-assisted pull requests `ai-assisted` and include
  `Co-authored-by` trailers.
