# Step Naming Rules & Examples
## Use cases and concrete example step names from the local workflow

Note: steps that use container images (for example `uses: docker://alpine:3.21`) are inline container-run steps for demos and are not local reusable actions.

1) Build (both `id` + `name`)
   - Step name shown: Build Artifact (id: `build-artifact`)
   - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L17](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L17)

2) Integration test (`name` only)
   - Step name shown: Run Integration Tests
   - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L37](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L37)

3) Deploy to production (`name` shown, uses local deploy action)
   - Step name shown: Deploy to Production
   - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L57](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L57)

4) Cleanup staging (local action with `name`)
   - Step name shown: Cleanup Staging
   - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L54](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L54)

This file lists four demo use cases and the corresponding local action steps in the workflow. (Container-run steps like `uses: docker://alpine:...` are omitted.)

1) Deploy to staging
    - Step shown: Deploy to Staging
    - Action used: `./actions/deploy-app`
    - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L51](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L51)

2) Deploy to production
    - Step shown: Deploy to Production
    - Action used: `./actions/deploy-app`
    - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L57](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L57)

3) Cleanup test environment
    - Step shown: Cleanup Test Environment
    - Action used: `./actions/cleanup-test`
    - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L39](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L39)

4) Cleanup staging
    - Step shown: Cleanup Staging
    - Action used: `./actions/cleanup-staging`
    - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L54](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L54)

That's all — four local-action examples for your demo.


