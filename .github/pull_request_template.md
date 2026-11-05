## Summary

<!-- What this changes, in a few sentences. -->

## App

<!-- `apps/<app-name>/`, or "team docs" if this PR does not touch an app. -->

- Issue:
- Spec: `apps/<app-name>/docs/spec.md`
- Design: `apps/<app-name>/docs/design/`

## Kind

<!-- One line. A PR that mixes kinds uses the stricter gate. Any code change is a code PR. -->

- [ ] Code — Reviewer PASS, Tester PASS, and green CI on this head SHA
- [ ] Docs-only — Reviewer PASS and green CI
- [ ] Deploy-only — Reviewer PASS and green CI

## Gates

Nits never block. A `nit:` comment is not a PASS. Rules: `team/workflow.md`.

Head SHA:

- [ ] Reviewer PASS on this head SHA (`Reviewer PASS <sha>`), or still valid after a clean merge of `main`
- [ ] Tester PASS on this head SHA (`Tester PASS <sha>`), or still valid after a clean merge of `main` — code PRs only
- [ ] CI green on this head SHA (a SHA with no checks is not green)
- [ ] Owner said `merge #N` (PM merges with a merge commit; PM is the sole merger)

## Deploy and cost

<!-- For a deploy or any new resource. Leave these open when the PR does not deploy. -->

- [ ] No new cloud resources and no spend, or the owner already approved them
- [ ] Not a production deploy, or the owner already approved this production deploy
