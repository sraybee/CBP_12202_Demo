# CBP-12202 Combined Workflow — Use Cases

**Overview:**
- This repository contains a combined CloudBees Automation workflow that consolidates useful steps and actions copied from three related repos: `CBP_12202_Testing`, `CBP-12202-Bug-Fixed-Testing`, and `CBP-27670-Testing`.
- The primary workflow file added is: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L1)

**Key jobs and use cases covered**
- **Build (artifact & version generation):**
  - Job: `build` — generates a deterministic `version` and an `artifact-name` as outputs. Useful for CI pipelines that need a reproducible build identifier and artifact metadata.
  - When to use: any push or manual run that needs to produce a build artifact for downstream testing or deployment.

- **Integration testing:**
  - Job: `integration-test` — runs integration tests against the produced artifact and performs cleanup via the `cleanup-test` action.
  - When to use: validate integration points (DBs, services, messaging) prior to promoting to staging.

- **Staging deployment + cleanup:**
  - Job: `deploy-staging` — creates a namespace, deploys using the local `deploy-app` action, then always runs `cleanup-staging` to tear down ephemeral resources.
  - When to use: smoke and acceptance testing in an ephemeral or shared staging environment.
  - Inputs & behavior: `deploy-app` accepts `environment`, `namespace`, `version`, `artifact`, `replicas`, and `log-level`.

- **Production deployment + smoke checks:**
  - Job: `deploy-production` — deploys to `production` (namespace set to `production`) using the same `deploy-app` action; followed by `cbp-12202-smoke` that performs lightweight sanity checks.
  - When to use: for manual or controlled production promotion after successful build & tests.

- **Cleanup actions:**
  - `cleanup-test` — stops test services, purges test data, and removes test resources. Refer to: [actions/cleanup-test/action.yml](actions/cleanup-test/action.yml#L1)
  - `cleanup-staging` — uninstalls application, deletes resources, deletes namespace and verifies cleanup. Refer to: [actions/cleanup-staging/action.yml](actions/cleanup-staging/action.yml#L1)

- **Fallback/test action:**
  - `my-fallback-action` — a small composite action used to exercise fallback behavior (copied from the bug-fixed repo). Refer to: [actions/my-fallback-action/action.yml](actions/my-fallback-action/action.yml#L1)

**Why these pieces were copied**
- `CBP_12202_Testing` provided reusable actions (`deploy-app`, `cleanup-test`, `cleanup-staging`) and sample workflows demonstrating staging/production flows — these map directly to CI/CD promotion scenarios.
- `CBP-12202-Bug-Fixed-Testing` provided a fallback action used to ensure UI/engine behavior for actions without explicit IDs/names.
- `CBP-27670-Testing` contributed the JFrog-download-style step (example of artifact retrieval from Artifactory) — if you need artifact downloads, that pattern can be reintroduced as a job/step using `cloudbees-io/jfrog-artifactory-download-file@v1`.

**Files added / copied**
- Workflow: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L1)
- Actions (local):
  - [actions/deploy-app/action.yml](actions/deploy-app/action.yml#L1)
  - [actions/cleanup-test/action.yml](actions/cleanup-test/action.yml#L1)
  - [actions/cleanup-staging/action.yml](actions/cleanup-staging/action.yml#L1)
  - [actions/my-fallback-action/action.yml](actions/my-fallback-action/action.yml#L1)
- Data examples (copied):
  - [data/PreProd.yaml](data/PreProd.yaml#L1)
  - [data/Prod.yaml](data/Prod.yaml#L1)

**Typical demo scenarios**
- Demo 1 — Full pipeline (manual): trigger `cbp-12202-combined-workflow` via workflow_dispatch to run `build` → `integration-test` → `deploy-staging` → `deploy-production` → `cbp-12202-smoke`.
- Demo 2 — Run only integration tests: run workflow and cancel/skip deploy jobs, or extract the `integration-test` job into a standalone workflow if desired.
- Demo 3 — Validate cleanup actions: run `integration-test` and let `cleanup-test` run `if: always()` to show teardown behavior even on failures.

**Notes & recommendations**
- The workflow references local actions using `uses: ./actions/<name>`; each action directory includes an `action.yml` file and uses simple Docker-based steps (alpine). These are safe for demos and intended as placeholders for real deployment tooling.
- For production-grade usage, replace `docker://alpine` placeholder steps with real deploy tooling (kubectl, helm, jfrog CLI, etc.) and add secrets/credentials in your secure store.
- Run a YAML linter or the CloudBees schema validator before importing into a production automation server — I validated structure statically but did not execute runtime validation.

If you want, I can:
- Commit these files to git locally (create a commit message and/or branch).
- Run a static YAML linter across the repo and report any schema/style issues.
- Replace placeholder `alpine` steps with example `kubectl` / `helm` commands using a small, documented template.

— Done by the automation assistant.
