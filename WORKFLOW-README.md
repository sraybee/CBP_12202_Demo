# Step Naming Rules & Examples

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
