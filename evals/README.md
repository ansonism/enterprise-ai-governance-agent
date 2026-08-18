# Evaluation plan

    Start with deterministic evals against the mock/fake adapters, then add provider-backed eval runs.

    Domain acceptance targets from `SKILL.md`:

    - Policy decisions cite the exact control/policy source supplied to the system.
- The agent never grants credentials or permissions.
- Missing evidence results in an explicit unknown/not-proven state.
- High-risk use cases require human approval in the workflow.
- Every run produces an immutable-style audit payload suitable for external persistence.

    Do not use an LLM judge as the sole source of truth for safety-critical or mechanically verifiable assertions.

Phase 1 eval cases are validated against the strict `EvalCase` contract. They declare required stages and findings, forbidden findings/actions, an expected risk range, and minimum evidence coverage. The suite runs deterministically with `MockProvider` and requires no network access or model judge.
