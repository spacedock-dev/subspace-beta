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
