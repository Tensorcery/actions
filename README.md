# actions

Shared CI steps of Tensorcery projects, as composite actions. A project calls
one by path and version:

```yaml
- uses: Tensorcery/actions/python/release@v1.0.0
```

| Path | What it does |
|---|---|
| `python/prepare-release` | bumps the version by commitizen on `release/v<next>` and opens the PR |
| `python/release` | on the default branch: when `v<version>` has no tag, builds, publishes to PyPI, creates the GitHub release and its tag |

Composite actions, not reusable workflows: their steps run inside the
caller's job, so PyPI's Trusted Publishing sees the caller's workflow, which
it requires.

## Versions

One version for the whole repository, a tag `vX.Y.Z` that never moves.
Callers pin the full version; Dependabot proposes the next one.

The paths and the inputs are the interface:

- a new action or a new optional input is minor;
- a fix inside an action is patch;
- a path renamed or removed, an input renamed or made required is major.

A path is `<ecosystem>/<purpose>/action.yml`, and stays where it is.

## Releasing this repository

Merge into `main` through a PR, then tag the merge commit:

```bash
gh release create vX.Y.Z --target main --generate-notes
```
