# Apps

Each app the team builds lives in `apps/<app-name>/`. How the team works lives in [`team/`](../team/workflow.md), not inside the app folder.

## Start an app

1. Pick a folder name: lowercase letters, digits, and hyphens, such as `apps/invoice-bot`. A name that starts with `_` is reserved.
2. Copy `apps/_template/` to `apps/<app-name>/`.
3. Replace the placeholders in `README.md` and `docs/spec.md`.
4. PM opens an issue for the owner's requirement and links this folder.
5. Follow [the workflow](../team/workflow.md) from the spec onward.

`apps/_template/` is the starter copy. It is not an app and it is not deployed.

## Folder

```text
apps/<app-name>/
  README.md            what the app is
  docs/spec.md         BA: spec and acceptance criteria
  docs/design/         UI: wireframes and design notes
  docs/user-guide.md   Docs: after the first production deploy
  src/                 Dev: implementation
```

`docs/user-guide.md` is not part of the template. Docs adds it after deploy.

## Pull requests

The repo gates apply to app work.

- Changes under `src/`, tests, or dependencies are code pull requests: Reviewer PASS, Tester PASS, and green CI on the same head SHA.
- Spec, design, and the user guide are docs-only: Reviewer PASS and green CI.
- Release and hosting changes with no behavior change are deploy-only: Reviewer PASS and green CI.

Nits never block. PM merges with a merge commit only after the owner says `merge #N`. A head SHA with no GitHub checks is not green. See [team/workflow.md](../team/workflow.md).
