# Workflow

End-to-end process for every app in this repo. Responsibilities and limits are in [roles.md](roles.md). The short version is in the root [README](../README.md).

The owner is GitHub user [fl147](https://github.com/fl147).

## Flow

1. **Requirement.** The owner gives PM an app requirement.
2. **Issues.** PM opens GitHub issues with the repo templates and names the folder, `apps/<app-name>/`.
3. **Spec.** BA writes the spec, including acceptance criteria, in `apps/<app-name>/docs/spec.md`.
4. **Spec approval.** The owner approves the spec by commenting on the spec pull request. Merging that pull request still waits for the docs-only gate and `merge #N`.
5. **Design.** UI produces wireframes and design notes in `apps/<app-name>/docs/design/`, matching the approved spec.
6. **Implementation.** Dev implements on a feature branch and opens a pull request that links the issue, the spec, and the design.
7. **Implementation gate.** On the implementation pull request, Tester and Reviewer each PASS that same head SHA, and CI is green on that SHA.
8. **Merge order.** The owner says `merge #N`, where N is the pull request number.
9. **Merge.** PM merges with a merge commit. PM is the sole merger.
10. **Deploy.** DevOps deploys the merged SHA. Production, new cloud resources, and any spend need the owner's word first.
11. **User guide.** Docs writes the user guide at `apps/<app-name>/docs/user-guide.md`.

The spec, the design, the implementation, and the user guide each land through a pull request. PM merges one only when that PR's gate is met and the owner has said `merge #N`.

UI starts design after the owner has approved the spec. Dev's implementation PR names the spec and the design it follows.

## Where work lives

| Work | Path |
| --- | --- |
| Spec and acceptance criteria | `apps/<app-name>/docs/spec.md` |
| Design and wireframes | `apps/<app-name>/docs/design/` |
| Implementation | `apps/<app-name>/src/` |
| User guide | `apps/<app-name>/docs/user-guide.md` |
| Team rules | `team/` |

Copy `apps/_template/` to start a new app. See [apps/README.md](../apps/README.md).

## Gates

Nits never block. A comment prefixed `nit:` is optional follow-up. Only a missing required PASS or CI that is not green holds a merge. A nit is not itself a PASS.

### PR kind

| Kind | What changed | Gate on the head SHA |
| --- | --- | --- |
| Code | App behavior, `src/`, tests, or dependencies | Reviewer PASS, Tester PASS, and green CI |
| Docs-only | Spec, design, user guide, team docs, or other documentation, and nothing else | Reviewer PASS and green CI |
| Deploy-only | Release, hosting, or infra only, with no app behavior change | Reviewer PASS and green CI |

A pull request that mixes kinds uses the stricter gate. Any code change makes it a code PR. Docs mixed with deploy, and no code, needs Reviewer PASS and green CI.

### PASS

A PASS is a comment on the pull request from that role:

```
Reviewer PASS <full 40-character sha>
Tester PASS <full 40-character sha>
```

The SHA is the head commit the PASS applies to.

- Reviewer PASS covers the change itself: correctness, fit to the spec and design, and risk.
- Tester PASS covers the acceptance criteria in `docs/spec.md`. It is required on code PRs only.
- The author of a pull request does not PASS that pull request.
- On a code PR, Reviewer PASS, Tester PASS, and green CI all refer to the same head SHA.

### Green CI

Green CI means every GitHub check on that head SHA has finished successfully. A pending check, a failing check, or a head SHA with no checks blocks the merge. Judge CI on the SHA that will be merged.

### Clean merge of main

A clean merge of `main` carries earlier PASSes forward. It is a merge of current `main` into the PR branch with no extra edits. The feature diff must be unchanged before and after (`git diff origin/main...<sha>`). The new head still needs green CI. Any other new commit drops earlier PASSes; Reviewer and Tester PASS the new head SHA.

### Merge

PM merges only when all of these are true:

- The gate for that PR kind is met on the head SHA. PASSes kept by a clean merge of `main` still count.
- CI is green on that head SHA.
- The owner has said `merge #N` for this pull request.

PM uses a merge commit (GitHub "Create a merge commit"). No squash and no rebase merge.

A production deploy, a new cloud resource, or spend still needs the owner's separate word. See DevOps in [roles.md](roles.md).

When a gate is missing, PM leaves the pull request open and names the missing gate.
