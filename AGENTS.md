# AGENTS.md

Rules for AI agents working in this repository. `CONTRIBUTING.md` is the source of truth for design tokens, HTML/SEO rules and Git flow; `opencode.json` loads it as a project instruction, so it is always in context.

## Project

Prototype e-commerce site for a French clothing brand (Maison Vérane). Five views: Home (`index.html`), Catalog (`catalogo.html`), Product, Cart, Checkout.

- **Stack:** plain HTML + Tailwind CSS v4 via the CDN script, pinned to an exact version with an SRI `integrity` hash (copy the `<script>` tag from `components/page-template.html`; never switch it back to `@4`). No JavaScript, no frameworks, no bundlers, no extra dependencies.
- **Shared components:** `components/navbar.html` and `components/footer.html` are copied unchanged into every page; pages inside `producto/` use `components/navbar-producto.html` and `components/footer-producto.html` (same markup, `../` links). Change them only through a dedicated PR.
- **Images:** local files in `assets/img/` (credits in `assets/img/CREDITS.md`). No hotlinked images.
- **Language:** page copy is Spanish (`<html lang="es">`); code, identifiers and comments are English.
- **Run locally:** `python3 -m http.server 8000`, then open `http://localhost:8000/index.html`.

## Subagents

Defined in `.opencode/agents/`. Invoke with `@name` or let the primary agent delegate.

| Agent | Use it for | Access |
|-------|-----------|--------|
| `frontend-developer` | Implementing or changing a view or component | Edits files, runs shell |
| `ui-ux-designer` | Design, usability and accessibility feedback on pages, CSS and screenshots | Read-only, `webfetch` |
| `code-reviewer` | Reviewing a PR, branch or diff before approval | Read-only; shell limited to `git`/`gh` read commands |

The two reviewers report findings; they never edit. Applying their feedback is `frontend-developer`'s job.

## Workflow for a view or change

1. Branch from an up-to-date `main`: `feature/<view>` (one branch per view or feature).
2. `frontend-developer` implements it, following `CONTRIBUTING.md`.
3. `ui-ux-designer` reviews every new or visually changed page at 375, 768 and 1280 px.
4. Fix the findings, in small commits.
5. Open a PR that says what it includes and how to test it.
6. `code-reviewer` reviews the PR and ends with a recommendation (approve, approve with comments, request changes).
7. The project owner approves and merges. `main` requires that approval.

## Rules

The hard limits below (merging, approving, force-push, push to `main`) are also blocked in `opencode.json` under `permission`. The rest is guidance.

- Never commit or push to `main`. Never force-push a shared branch.
- Agents never approve, merge or close PRs, and never change branch protection. Those are human decisions.
- Commits follow Conventional Commits, one logical change each (`feat(home): add hero`).
- Run the page in a browser before calling it done: no horizontal page scroll at 375 px, one `<h1>`, one `<main>`, no broken links or images.
- Keep changes in scope: do not touch another contributor's view or the shared components unless asked.
- Never commit credentials, tokens or `.env` files.
