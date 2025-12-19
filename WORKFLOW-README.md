# Step Naming Rules & Examples

1) StepName and ID Both Mentioned
    - Job: `build`
    - Step: `Get source code` (id: `checkout`) — uses `cloudbees-io/checkout@v1`
    - Location: [dsl-engine-cli/.cloudbees/workflows/workflow.yaml#L13](dsl-engine-cli/.cloudbees/workflows/workflow.yaml#L13)

2) StepName and ID None Mentioned
    - Job: `cbp-12202-test-job`
    - Step: anonymous uses `./.cloudbees/my-fallback-action` (no `id`, no `name`) — demonstrates UI fallback
    - Location: [CBP-12202-Bug-Fixed-Testing/.cloudbees/workflows/cbp-12202-bug-fixed-test.yaml#L15](CBP-12202-Bug-Fixed-Testing/.cloudbees/workflows/cbp-12202-bug-fixed-test.yaml#L15)

3) Only StepName Mentioned
    - Job: `deploy-production`
    - Step: `Deploy to Production` (uses local action `./actions/deploy-app`, no `id` on the step)
    - Location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L57](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L57)

4) Only ID Mentioned
    - Job: `job1` (testdata complex workflow)
    - Step: id `local-action` (uses local composite action, no `name` provided)
    - Location: [dsl-engine-cli/internal/scm/git/testdata/repos/github.com-443/cloudbees-io/local-test/refs/heads/main/no-sha/.cloudbees/workflows/workflow.yaml#L15](dsl-engine-cli/internal/scm/git/testdata/repos/github.com-443/cloudbees-io/local-test/refs/heads/main/no-sha/.cloudbees/workflows/workflow.yaml#L15)
