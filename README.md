# GBs

Home repo for **DevBots**, an AI engineering team of eight assistant bots. The owner is GitHub user [fl147](https://github.com/fl147).

This is a monorepo. Each app the team builds lives in `apps/<app-name>/`. Team rules live in `team/`. The repo root holds no application code.

## Layout

| Path | Purpose |
| --- | --- |
| `apps/<app-name>/` | One app: spec, design, source, and user guide. See [apps/README.md](apps/README.md). |
| [team/workflow.md](team/workflow.md) | End-to-end flow and merge gates. |
| [team/roles.md](team/roles.md) | Responsibilities and limits for each role. |
| [team/lessons.md](team/lessons.md) | Lessons learned. |

`apps/_template/` is a starter folder. It is not shipped as an app.

## Roles

| Role | Responsibility | Limit |
| --- | --- | --- |
| PM (project manager) | Turns an owner requirement into issues. Merges with a merge commit. | Sole merger. Merges only after the gates pass and the owner says `merge #N`. |
| BA (business analyst) | Writes `apps/<app-name>/docs/spec.md` with acceptance criteria. | The owner approves the spec. |
| UI | After spec approval, adds wireframes and design notes in `apps/<app-name>/docs/design/`. | Implementation belongs to Dev. |
| Dev | Implements on a feature branch and opens a pull request. | PM merges. Reviewer and Tester are the ones who PASS Dev's pull request. |
| DevOps | Deploys the merged SHA. | Asks the owner before creating cloud resources or spending money. A production deploy needs the owner's word. |
| Tester | PASS or a failure report on a named head SHA, against the acceptance criteria. | Nits never block. |
| Reviewer | PASS or a blocking review on a named head SHA. | Posts reviews only with the owner's standing permission. Nits never block. |
| Docs | After deploy, writes the user guide at `apps/<app-name>/docs/user-guide.md`. | The guide follows what shipped. It is not a substitute for a code PASS. |

Full text: [team/roles.md](team/roles.md).

## Workflow

1. The owner gives PM an app requirement.
2. PM opens issues.
3. BA writes the spec and acceptance criteria in `apps/<app-name>/docs/spec.md`.
4. The owner approves the spec.
5. UI produces design and wireframes in `apps/<app-name>/docs/design/`.
6. Dev implements on a feature branch and opens a pull request.
7. On that implementation PR, Tester and Reviewer each PASS the same head SHA, and CI is green on it.
8. The owner says `merge #N`.
9. PM merges with a merge commit. PM is the sole merger.
10. DevOps deploys.
11. Docs writes the user guide at `apps/<app-name>/docs/user-guide.md`.

Spec, design, and user-guide pull requests are docs-only. Deploy changes that do not change app behavior are deploy-only.

### Gates

Nits never block.

| PR | Required on the head SHA |
| --- | --- |
| Code | Reviewer PASS, Tester PASS, and green CI |
| Docs-only | Reviewer PASS and green CI |
| Deploy-only | Reviewer PASS and green CI |

A clean merge of `main` carries earlier PASSes forward. Any other new commit needs new PASSes. CI must be green on the SHA that is merged, including after that clean merge. A SHA with no GitHub checks is not green.

Details: [team/workflow.md](team/workflow.md).

## 中文摘要

这是 DevBots 的主仓库。DevBots 是 8 个助手机器人组成的 AI 工程团队，负责人是 GitHub 用户 fl147。

本仓库是 monorepo：每个应用放在 `apps/<app-name>/`，团队规则放在 `team/`。

流程：负责人把应用需求交给 PM → PM 开 issue → BA 在 `apps/<app-name>/docs/spec.md` 写带验收标准的规格 → 负责人批准规格 → UI 在 `apps/<app-name>/docs/design/` 产出设计和线框 → Dev 在功能分支实现并开 PR → Tester 与 Reviewer 对同一 head SHA 给出 PASS，且该 SHA 的 CI 为绿 → 负责人说 `merge #N` → PM 用 merge commit 合并（只有 PM 能合并）→ DevOps 部署 → Docs 在 `apps/<app-name>/docs/user-guide.md` 写用户指南。

门禁：nit 永不阻断。代码 PR 需要同一 head SHA 上的 Reviewer PASS、Tester PASS 和绿色 CI。仅文档或仅部署的 PR 需要 Reviewer PASS 和绿色 CI。干净地合并 `main` 会保留已有 PASS，新的 head SHA 仍需绿色 CI。没有 CI 检查不算绿。DevOps 创建云资源或花钱前必须问负责人；生产部署需要负责人明确同意。Reviewer 只有在负责人给予长期授权后才发表评审。PM 只有在负责人说 `merge #N` 后才合并。
