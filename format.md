# [Standard Title]

## 1. Architectural Baseline & Guardrails
High-level structural boundary (allowed regions, platforms, deployment topologies, managed vs. self-hosted).

## 2. Resource & Topology Matrix
Exact structural layout required (VPC placement, multi-AZ, redundancy models, supported instance tiers).

## 3. FinOps & Sizing Boundaries
* Cost controls, over-provisioning guardrails, capacity ceilings.
* Thresholds determining when to use serverless vs. provisioned resources.

## 4. Mandatory Metadata & Attribution (Tagging)
The exact keys and formats required for cost allocation, ownership, and lifecycle automation.

## 5. Drift & Operational Lifecycle
Backup lifecycles, deletion protection, auto-pause rules, and idle resource timeouts.

## 6. Prohibited Topologies & Anti-Patterns
Explicit deployment patterns, SKU sizes, or cross-boundary architectures that trigger compliance blocking.