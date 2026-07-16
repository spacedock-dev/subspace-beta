# Subspace beta

Subspace opens one Markdown file in a native terminal review and returns a
neutral, invocation-bound Review v1 result to the same agent session.

Install the binary with Homebrew:

```sh
brew install spacedock-dev/tap/subspace-beta
```

Then invoke `subspace:r docs/design.md`. Claude uses
`/subspace:r docs/design.md`; Codex uses `$subspace:r docs/design.md` or the
skill picker. The optional transport is `auto`, `zellij`, `ghostty`,
`apple-terminal`, `direct`, or `inline`.

Subspace reports feedback and non-binding advice. The invoking workflow decides
what to do with the result.
