# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is
This is a **GitHub profile README** repository (the special `achrafS133/achrafS133` repo). It is static content, not an application — there is no package manager, build system, or test suite. Contents:
- `README.md` — the profile page shown on GitHub.
- `achrafS133-dark_mode.svg`, `achrafS133-light_mode.svg` — hand-authored "Portfolio Stats" cards.
- `assets/data.png` — image used in the README.
- `.github/workflows/snake.yml` — GitHub Actions workflow that regenerates a contribution-snake SVG on a schedule. It only runs on GitHub Actions (needs `GITHUB_TOKEN`); it is not meant to be run locally.

### Preview / run (the dev loop)
Preview the README exactly as GitHub renders it using `grip` (installed by the update script):
```
python3 -m grip README.md 0.0.0.0:6419
```
Then open `http://localhost:6419/`. Notes:
- Use `python3 -m grip ...` rather than the bare `grip` command — the console script lives in `~/.local/bin`, which is not on `PATH`.
- grip live-reloads the browser when `README.md` changes, so the edit→preview loop is instant.
- grip renders by POSTing the markdown to GitHub's API, so it needs outbound network to `api.github.com`. Unauthenticated requests are rate-limited (60/hour); set `GRIP_ACCESS_TOKEN` (a GitHub PAT) if you hit limits.
- Many badges/stat cards in the README load remote images from third-party services (shields.io, vercel apps, etc.), so give the page a few seconds and expect some to be blank if egress to those hosts is blocked.
- View the SVG cards directly in a browser via `file:///workspace/achrafS133-dark_mode.svg` (and `..._light_mode.svg`).

### "Lint" / validation
There is no linter. The most useful check is validating the SVG cards are well-formed XML:
```
xmllint --noout achrafS133-dark_mode.svg achrafS133-light_mode.svg
```
