# Enterprise AI Governance Agent

    A policy-aware governance control plane for enterprise AI agents and models covering inventory, risk classification, permissions, privacy, auditability, evaluation evidence, and approval gates.

    ## Why this exists

    Evaluate AI systems and agents against enterprise policies and regulatory/control requirements, detect governance gaps, and produce actionable controls without autonomously granting privileges or bypassing human governance.

    This repository is intentionally scaffolded as a **production-oriented agent project**, not a prompt-only demo. It starts with a deterministic mock provider so the complete orchestration path can be executed locally before adding any commercial LLM.

    ## Core workflow

    inventory_ai_system -> classify_use_case_and_data -> map_policies_and_controls -> evaluate_identity_permissions_and_tool_access -> evaluate_privacy_security_and_data_handling -> evaluate_model_and_agent_risk -> check_evaluation_and_monitoring_evidence -> compute_governance_posture -> produce_remediation_and_approval_plan

    ## Specialized agents

    - `inventory_agent`
- `policy_mapper`
- `privacy_reviewer`
- `security_reviewer`
- `permissions_reviewer`
- `model_risk_reviewer`
- `audit_agent`
- `governance_judge`

    ## Planned tool adapters

    - `policy_loader`
- `identity_reader`
- `data_catalog_reader`
- `model_registry_reader`
- `eval_registry_reader`
- `audit_writer`

    ## Quick start

    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    pip install -e ".[dev]"
    enterprise-ai-governance run examples/sample_input.json --output out/result.json
    pytest
    ```

    Or:

    ```bash
    make setup
    make demo
    make test
    ```

    ## Safety defaults

    - Mock/dry-run behavior is the default.
    - External systems are accessed only through explicit adapters.
    - No production mutation should be added without an approval gate.
    - Facts, assumptions, hypotheses and recommendations should remain distinguishable in outputs.
    - Credentials must come from environment/secret stores, never source control.

    ## Codex implementation guide

    Start with [`SKILL.md`](./SKILL.md). It defines the mission, architecture, implementation sequence, acceptance criteria and guardrails Codex should follow.

    ## Repository layout

    ```text
    .
    ├── AGENTS.md
    ├── SKILL.md
    ├── config/
    ├── docs/
    ├── evals/
    ├── examples/
    ├── kubernetes/
    ├── prompts/
    ├── scripts/
    ├── src/ai_governance/
    ├── terraform/
    └── tests/
    ```

    ## Current state

    **Phase 1 core.** The typed harness validates configuration and domain inputs, writes an atomic checkpoint after every stage, supports idempotent resume by run ID, and emits redacted structured logs. The default CLI stores state under `out/state/`. `make demo`, `make test`, and `make lint` verify the runnable mock-provider implementation.