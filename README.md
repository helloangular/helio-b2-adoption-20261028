# helio-b2-adoption-20261028

Owned fixture repository of QA-guide worker B2 (227-case qualification, 28 Oct 2026). Nothing here deploys
an application; every job is synthetic evidence for Helio's adoption, follow-up and cancellation cases.

| Workflow | Trigger | Environment | Used by |
|---|---|---|---|
| `b2-observe.yml` | push (main, feature/**, excluded/**), schedule */15, pull_request, workflow_dispatch | `b2-observe-test` (no reviewers) | TC-220 observe-push/schedule, TC-221 pr/workflow-dispatch/branch-mismatch, TC-222, TC-224, TC-298 |
| `b2-govern.yml` | push (main, feature/**), schedule :07/:37, workflow_dispatch | `b2-govern-test` (Helio reviewer) — deploy job only while var `B2_GOVERN_ARMED=true` | TC-220 govern-existing-push/schedule, TC-222, TC-223, TC-298 governed |
| `b2-provider.yml` | Helio workflow_dispatch from `helio/workflow/<sha>` | `b2-provider-test`, `b2-provider-production` (Helio reviewer) | TC-10, TC-100, TC-101, TC-225–228, TC-283, TC-297 |
| `b2-matrix.yml` | push main (paths b2-matrix/**) | `b2-observe-test` | TC-221 unsupported-matrix |
| `b2-reusable.yml` (+ body) | push main (paths b2-reusable/**) | `b2-observe-test` | TC-221 unsupported-reusable |

Trigger files: a commit under `b2-observe/`, `b2-govern/`, `b2-matrix/` or `b2-reusable/` fires only that workflow.
Every commit is pushed together with its `helio/workflow/<sha>` tag (agents/b2/lane.py in helio-test).
