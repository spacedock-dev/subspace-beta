# Subspace beta

Subspace opens one Markdown file in a native terminal review and returns a
neutral, invocation-bound Review v1 result to the same agent session.

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

The optional transport is `auto`, `zellij`, `ghostty`, `apple-terminal`,
`direct`, or `inline`.

Subspace reports feedback and non-binding advice. The invoking workflow decides
what to do with the result.

## License scope

Apache-2.0 covers only the public plugin and skill integration files in this
repository. Subspace product source is private and is not included. The
released subspace-tui binary is not licensed under Apache-2.0.
