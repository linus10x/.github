# linus10x/.github

Account-wide defaults for every repository owned by [@linus10x](https://github.com/linus10x).

## What lives here

| Path | Purpose |
| --- | --- |
| `SECURITY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SUPPORT.md` | Default community health files. GitHub shows them in any repo that has no file of its own. |
| `ISSUE_TEMPLATE/`, `PULL_REQUEST_TEMPLATE.md` | Default issue forms and PR template. |
| `.github/workflows/reusable-*.yml` | Hardened reusable CI workflows that any repo can call. |
| `templates/` | Copy-in starters: a caller workflow, `dependabot.yml`, `CODEOWNERS`. |

## Workflow standards

Every workflow in this account should meet these rules (OpenSSF Scorecard and SLSA practice):

1. Pin every third-party action to a full commit SHA, with the version in a comment. Dependabot's `github-actions` ecosystem keeps the pins current.
2. Set `permissions: contents: read` at the top and widen only per job.
3. Set `timeout-minutes` on every job (the default is 360).
4. Use `concurrency` so a newer push cancels the older run.
5. Run CI on `pull_request` and on `push` to `main` only, never on every branch push.
6. Use path filters on optional workflows, but never on a required status check (a skipped workflow leaves the check pending).

## Calling a reusable workflow

```yaml
jobs:
  ci:
    uses: linus10x/.github/.github/workflows/reusable-python-ci.yml@main
    with:
      python-version: "3.12"
```

Pin `@main` to a commit SHA in repos where supply-chain risk matters.
