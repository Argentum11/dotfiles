# vscode settings

## Goals

- Prevent pasting colors and formatting from vscode
  - `editor.copyWithSyntaxHighlighting`
- Prevent using VS Code's own browser pane instead of your system browser
  - `workbench.browser.openLocalhostLinks`
- Autosave instead of manually saving the file
  - `files.autoSave`

## Apply

Merge these settings into VS Code's user settings file
(`~/.config/Code/User/settings.json` on Linux). Run from the root of this
repo:

```bash
mkdir -p ~/.config/Code/User
touch ~/.config/Code/User/settings.json
jq -s '.[0] * .[1]' ~/.config/Code/User/settings.json ./vscode/settings.json > /tmp/vscode-settings.json \
  && mv /tmp/vscode-settings.json ~/.config/Code/User/settings.json
```

### How it works

- `jq -s '...'` — the `-s` (slurp) flag reads all input files into a single
  JSON array instead of processing them one at a time. Given two files, that
  array is `[existing_settings, repo_settings]` — `.[0]` is your current
  `~/.config/Code/User/settings.json` and `.[1]` is this repo's
  `vscode/settings.json`.
- `.[0] * .[1]` uses jq's `*` object-merge operator: a shallow merge of the
  two objects.
  - Keys that exist only in your real settings → untouched, kept.
  - Keys that exist only in the repo's `settings.json` → added.
  - Keys that exist in both → the repo's value wins, overwriting the old one
    (not duplicated).
- The result is written to a temp file, then moved over the real settings
  file — avoids truncating/corrupting the original if something goes wrong
  mid-write (can't safely redirect `>` into the same file you're reading
  from).

Because the merge is idempotent, it's safe to re-run this command anytime
after pulling repo updates.
