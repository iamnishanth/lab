# lab

A collection of small, fun single-page web experiments. Public repo, served by GitHub Pages from the root of `main` at https://iamnishanth.github.io/lab/ (`.nojekyll` keeps Pages from running Jekyll).

## Structure

- `index.html`: the root page that lists every experiment.
- `favicon.svg`, `favicon.ico`, `apple-touch-icon.png`: the lab's icon (a flask), used by the root page. `favicon.svg` is the source; the `.ico` (16/32/48 px) and the 180 px apple-touch icon are rendered from it, so regenerate them after editing it.
- `<slug>/index.html`: one folder per experiment, e.g. `shirt-pants/`.
- `README.md`: has a table of experiments that must stay in sync with the root page.

## Rules for experiments

- One self-contained `index.html` per experiment: inline CSS and JS, no build step, no npm. Fonts from Google Fonts and pinned-version scripts from a CDN are fine.
- Put a "Back to the lab" link (`<a class="back" href="../">`) at the top of the page.
- Give the page an inline SVG `data:` favicon so it doesn't 404 on `favicon.ico`.
- Use relative links only. The site lives under `/lab/`, so a root-absolute path like `/foo` breaks on Pages.
- Make it work at phone width (390px) with no horizontal scroll, show visible keyboard focus, and respect `prefers-reduced-motion`.
- Each experiment can have its own visual identity. Use the frontend-design skill when designing a new one.

## Adding an experiment to the root page

1. In `index.html`, append an entry to the end of the `EXPERIMENTS` array: `path` (`'<slug>/'`), `title`, `blurb` (one sentence), `date` (`YYYY-MM-DD`), and `thumb`.
2. Add the thumbnail as an 88×88 inline SVG in `THUMBS`. Use a unique `clipPath` id per thumbnail, since they all share one document.
3. Entry numbers (001, 002…) come from array order, so never reorder or remove entries. Numbers are the experiment log.
4. Add a matching row to the table in `README.md`.

## Root page design

A lab notebook page: graph-paper grid, blue-black ink (`#1C2433`), a red margin line, and Bricolage Grotesque throughout. Keep changes within that look.

## Checking changes

Use `agent-browser` (load the agent-browser skill first). Serve the repo over HTTP rather than opening `file://`, because the folder links (`shirt-pants/`, `../`) open directory listings under `file://`:

```sh
python3 -m http.server 8000   # run in the background from the repo root

export AGENT_BROWSER_SESSION="$(agent-browser session id --scope worktree --prefix lab)"
agent-browser set viewport 390 844        # repeat at 1280 800 for desktop
agent-browser open http://localhost:8000/
agent-browser snapshot -i -u              # links and their URLs
agent-browser errors                      # page errors
agent-browser screenshot <path>.png
agent-browser close
```

Check the root page, the new experiment, and the links between them at desktop and 390px widths. After pushing, the Pages build status is at `gh api repos/iamnishanth/lab/pages/builds/latest -q .status`.
