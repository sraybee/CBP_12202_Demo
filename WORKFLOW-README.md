# Step Naming Rules & Examples

- **Both `id` and `name` provided:** UI shows the explicit `name` (the human-friendly label).
  - **Example:** Job `build` → step `Generate Version` (id: `generate-version`, name: `Generate Version`). See [cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L13).

- **`id` provided, `name` not provided:** UI will show the action's internal name (if the referenced action defines a `name` in its `action.yml`); otherwise the UI will fall back to a computed label (action path or fallback).
  - **Example:** Test fixture workflow with `id` only (`repo-action-second-org-root`, `local-action`, etc.). See [dsl-engine-cli testdata workflow](dsl-engine-cli/internal/scm/git/testdata/repos/github.com-443/cloudbees-io/local-test/refs/heads/main/no-sha/.cloudbees/workflows/workflow.yaml#L15).

- **`name` provided, `id` not provided:** UI shows the provided `name` (this is the explicit, human-readable label shown in the step list).
  - **Example:** Job `integration-test` → step `Setup` and `Run Integration Tests` in the combined workflow (both steps have `name` but no `id`). See [cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L31) and [cbp-12202-combined-workflow.yaml](.cloudbees/workflows/cbp-12202-combined-workflow.yaml#L37).

- **Neither `id` nor `name` provided:** UI will show the action's internal name if the action defines one; if the action itself also lacks a name/id the UI shows a fallback label (often the action folder or a generated fallback).
  - **Example:** Workflow step that uses a local fallback action without a step `name` — see [cbp-12202-bug-fixed-test.yaml](../CBP-12202-Bug-Fixed-Testing/.cloudbees/workflows/cbp-12202-bug-fixed-test.yaml#L17) and its action [my-fallback-action/action.yml](../CBP-12202-Bug-Fixed-Testing/.cloudbees/my-fallback-action/action.yml#L1).

**Quick guidance**
- Use `name` when you want a clear, readable label for the UI.
- Use `id` when you need to reference step outputs (e.g., `steps.<id>.outputs.xxx`).
- If you provide both, `name` is used for display and `id` for programmatic references.

