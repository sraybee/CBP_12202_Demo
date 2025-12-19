# Step Naming Rules & Examples (CBP_12202_Demo only)

This minimal sheet shows four naming combinations using steps from `.cloudbees/workflows/cbp-12202-combined-workflow.yaml`.

1) StepName and ID Both Mentioned
   - Job: `deploy-staging`
   - Step: `Create Namespace` (id: `namespace`) — has both `id` and `name`; produces an output used by later steps
   - Reference: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L45)

2) StepName and ID None Mentioned
   - Job: `integration-test`
   - Step: anonymous `uses: ./actions/my-fallback-action` (no step `id`, no step `name`) — demonstrates UI fallback labeling
   - Reference: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L41)

3) Only StepName Mentioned
   - Job: `deploy-production`
   - Step: `Deploy to Production` — display `name` present; step invokes local action `./actions/deploy-app` (no step `id`)
   - Reference: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L57)
   - Action: [actions/deploy-app/action.yml](actions/deploy-app/action.yml#L1)

4) Only ID Mentioned
   - Job: `integration-test`
   - Step: id `example-only-id` (no `name`) — demonstrates a step referenced programmatically by `id`
   - Reference: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L39)

That's it — focused, CBP_12202_Demo–only examples for your demo.
