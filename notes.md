## Prediction (from memory)

I added a `count` command: a new `count()` function in `lib/store.js`, wired up as a `case "count"` in `notes.js`, and renamed the `FILE` constant in `lib/store.js` to `NOTES_FILE` for clarity.

## Claude's summary

Reviewing the actual diff, three files changed:

- **lib/store.js** — renamed the module-level constant `FILE` → `NOTES_FILE` (and updated its two usages in `load()`/`save()`), and added a new exported `count()` helper that returns `all().length`.
- **notes.js** — added a `case "count"` to the command switch that prints `You have N note(s).`, and updated the default/help line to list `count` as an available command.
- **lib/config.js** — changed `SESSION_TIMEOUT_MINUTES` from `15` to `20`. This one looks unintended: it's unrelated to the count feature, sits in a file the prediction above never mentions, and is the kind of edit that's easy to leave in by accident.

Flag: the `lib/config.js` timeout change is the odd one out — worth double-checking whether it was meant to ship with this PR.

Did it catch the stray change? Yes — the prediction above only mentioned the count feature and the rename, and didn't mention touching `lib/config.js` at all. The diff review caught that extra edit that would have otherwise slipped through unreviewed.
