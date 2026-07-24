# Subspace beta

Subspace opens one Markdown file in a native terminal review and returns
feedback to the same agent session without implying approval authority.

## Install and start

Complete these steps in order.

1. Install the binary with Homebrew:

```sh
brew install spacedock-dev/tap/subspace-beta
```

2. Choose one agent host and install its plugin.

   For Claude:

```sh
claude plugin marketplace add spacedock-dev/marketplace
claude plugin install subspace@spacedock
```

   For Codex:

```sh
codex plugin marketplace add spacedock-dev/marketplace
codex plugin add subspace@spacedock
```

3. Start a new session in the selected host so the new plugin loads.

4. Review a Markdown file. In Claude, run `/subspace:r docs/design.md`. In
   Codex, run `$subspace:r docs/design.md` or select the skill from the picker.

Pass a terminal explicitly, for example
`$subspace:r docs/design.md tmux`, or omit it to detect the first live caller in
this fixed order: Zellij, tmux, Herdr, CMUX, Ghostty, then Apple Terminal. A
partial or broken higher-priority caller stops with a remedy; Subspace never
falls through or opens a second surface. The exact local candidate is
`0.10.0-beta.3`.

Supported host versions are [Zellij](https://zellij.dev/) 0.44.x,
[tmux](https://github.com/tmux/tmux/wiki) 3.2 or newer,
[Herdr](https://herdr.org/) 0.6.5, [CMUX](https://cmux.com/) 0.64.20 build 100,
Ghostty 1.2 or newer on macOS, and the system Apple Terminal. The invoking host
must grant permission before Subspace probes or launches the selected terminal.

Subspace reports ordered feedback, says when the review completed with no
feedback, or preserves an open continuation. Plain-file review never records a
Decision; an invoking workflow decides what to do with the feedback.

## Use the review

When the review pane opens, you read the Markdown on the left and attach
anchored comments that return to the agent session when you finish. The pane's
footer legend is the source of truth for the active keys; the current build
shows:

- Move through the file with the arrow keys or `j` and `k`. In findings, `n`
  and `p` step between anchored comments.
- Press `/` to search the file.
- Press `v` to select the span you want to comment on, then type your note in
  the comment editor.
- Press `Ctrl+y` to move focus between the file pane and the comment pane.
- The `include` toggle on a comment controls whether it is sent.
- Press `q` to finish. This closes the pane and delivers every included comment
  to the agent. It is the only key that submits.
- Press `Ctrl+o` to leave the review open instead, preserving it as a
  continuation you can return to.

The footer also shows `draft saved` as you work. That is autosave only; it does
not submit. Your feedback reaches the agent only when you finish with `q`. If
the keys in your build differ from the list above, trust the footer legend in
your own pane.

### Bring a hidden review pane back

The review opens as a pane inside your terminal multiplexer, so restoring it
after you switch away is a host action, not a Subspace one. In Zellij, press
`Ctrl+p` then `w` to toggle floating panes back into view. Other hosts use
their own pane-focus commands.

## Troubleshoot the binary

The plugin requires `subspace-tui` version `0.10.0-beta.3`. If the binary is
missing, run:

```sh
brew install spacedock-dev/tap/subspace-beta
```

If the binary is present but reports another version or invalid version output,
run:

```sh
brew upgrade spacedock-dev/tap/subspace-beta
```

If `brew` is unavailable, install Homebrew from `https://brew.sh`, then run the
appropriate command above and retry. The plugin only reports these remedies; it
never installs or upgrades the binary.

## Dogfood this checkout

Both local marketplaces resolve this canonical candidate plugin tree. Build the
matching exact-tip binary with the private validation skill, install from the
repository root, and start a new host session before testing discovery or
invocation:

```sh
# Codex: install and refresh same-version local source bytes
codex plugin marketplace add .
codex plugin add subspace@subspace-local

# Claude: initial install
claude plugin marketplace add ./ --scope local
claude plugin install subspace@subspace-local --scope local

# Claude: refresh same-version local source bytes
claude plugin uninstall subspace@subspace-local --scope local
claude plugin install subspace@subspace-local --scope local
```

An already-running session keeps its existing skill catalog. Claude's
`--plugin-dir ./plugins/subspace` is useful while editing, but it does not
replace the marketplace reinstall and fresh-session acceptance path.

## License scope

Apache-2.0 covers only the public plugin and skill integration files in this
repository. Subspace product source is private and is not included. The
released subspace-tui binary is not licensed under Apache-2.0.
