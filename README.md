# lab

Small web experiments, one page each. Live at https://iamnishanth.github.io/lab/

| # | Experiment | What it does |
|---|---|---|
| 001 | [Outfit color wheel](shirt-pants/) | Pick a shirt color; color theory suggests pants to match, then shoes for the pair. |

## Adding an experiment

1. Create a folder with an `index.html`, e.g. `my-thing/index.html`. Plain HTML, no build step.
2. Add a "Back to the lab" link (`href="../"`) at the top of the page.
3. Add an entry to the `EXPERIMENTS` array in the root `index.html` (and a thumbnail in `THUMBS`).
4. Add a row to the table above.

## Run locally

```sh
python3 -m http.server 8000
```

Then open http://localhost:8000.
