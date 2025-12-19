# Step Naming Rules & Examples

## Use cases and concrete example step names from the local workflow:

1) Build (both `id`+`name`)
   - Step name shown: Generate Version
   - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L13](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L13)

2) Integration test (`name` only)
   - Step name shown: Run Integration Tests
   - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L37](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L37)

3) Deploy to staging (`id` + `name` for namespace step; deploy step uses local action)
   - Step name shown: Create Namespace (id: `namespace`) and Deploy to Staging
   - Workflow location: [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L51](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L51)

4) Fallback / unnamed action (neither `id` nor `name` on step)
   - Step name shown: fallback action label (engine fallback) — used to demonstrate UI fallback
   - Workflow location (demo): use `Cleanup Test Environment` which references local action at [.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L39](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L39)

That's it — this file is intentionally minimal for your demo.


