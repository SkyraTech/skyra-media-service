# Skyra Media Generation Service — Architecture

Last maintained: 2026-10-14. Canonical architecture, data ownership and decision record; update in place.

## Current state

Specification only; no generation provider or durable job runner implemented.

## Responsibility and technology

Provider-independent job management for image and video generation, revisions and deliverables used by Jarvis and commercial products.

Target: TypeScript on a supported Node.js LTS, NestJS for service boundaries, OpenAPI/JSON Schema contracts. Retain working existing adapters behind contracts during incremental migration. PostgreSQL for independently hosted durable state; local development adapters must preserve the same ownership and idempotency semantics.

This stack describes direction where code is not built. Exact upgrades require manifest/lockfile review and compatibility tests; this documentation change installs or upgrades nothing.

## Component and integration boundaries

- [skyra-service-contracts](../../skyra-service-contracts/README.md)
- [skyra-service-foundation](../../skyra-service-contracts/docs/ARCHITECTURE.md#foundation-component)
- [skyra-quality](../../skyra-quality/README.md)

Use versioned HTTP/OpenAPI/JSON Schema contracts and authorized MCP adapters. Consumers never read/write another service’s database. Credentials, provider accounts and organization/project scope are explicit; optional unavailable services are disabled rather than simulated as success.

## Database architecture

No implemented persistent business schema was found or built for this project. Existing code/specification is not a deployed multi-customer database. The following is a proposed logical model; column types, SQL constraints, retention and migrations must be agreed before implementation.

| Entity | Proposed fields | Ownership / invariant |
|---|---|---|
| GenerationJob | `id, organization_id, project_id, provider, model, request_ref, request_hash, budget_limit, state` | Explicit provider/model, cost and cancellation policy. |
| ProviderAttempt | `id, job_id, provider_job_id, outcome, charged_usage, attempt_no` | Persist billing/uncertain provider outcomes before retry. |
| Artifact | `id, job_id, parent_artifact_id, media_type, location_ref, checksum, provenance_ref` | Versioned image/video deliverables and revisions. |
| UsageRecord | `id, job_id, currency, estimated_cost, confirmed_cost, observed_at` | Consumption evidence for quotas; commercial billing belongs to its product ledger. |

Stateful hosted implementation may use a service-owned PostgreSQL database/schema. Every tenant-owned record needs organization scope, and account/resource access must be enforced server-side. References to external services are opaque IDs, not cross-database foreign keys. Store large artifacts in restricted object/file storage with checksums. Sensitive provider credentials use protected-store references, not plaintext columns.

## Execution and failure rules

Persist intent before a side effect. Use bounded ownership leases, idempotency keys and result reconciliation; do not promise exactly-once external delivery without provider support. Verify webhook signatures and deduplicate inbox records. Approval binds exact action, account, resource, payload and expiry; MCP discovery grants no privilege.

## Security and operations

Protect credentials, redact errors/logs, validate configuration and deny cross-organization access. Untrusted model/provider/document content cannot change policy. Define export/deletion and retention by data class; test backup/restore for any durable implementation. Hosted customer services must remain independent of the owner’s laptop. Release evidence includes exact source/toolchain/profile; production deployment remains a separately authorized action.

## Proposed folder direction

Keep domain/application rules separate from transport and provider/storage adapters. Tests live with the owning project; machine-readable contracts and release fixtures are versioned. Existing source folders stay in place until a tested migration. A backend-only service does not need an invented UI dashboard; host interfaces display truthful connection/job/permission states.

## Decisions and unresolved work

- Provider pricing, licensing and retention require verification before selecting adapters
- Cancellation may not reverse provider charges
- Local GPU generation remains a future adapter, not a release prerequisite

| Date | Architecture change | State |
|---|---|---|
| 2026-10-14 | Project ownership, technology direction and data model consolidated into this maintained file | Proposed where no implementation exists |

## Initial specification set

Retain and update the original nine documents. They describe product requirements, system architecture, development rules, design, tasks, memory, API/events, testing/acceptance and security/operations. These current overview files supplement them; they do not replace them.

- [Product requirements](01_PRODUCT_REQUIREMENTS.md)
- [System architecture](02_SYSTEM_ARCHITECTURE.md)
- [Development rules](03_DEVELOPMENT_RULES.md)
- [Design system](04_DESIGN_SYSTEM.md)
- [Project tasks](05_PROJECT_TASKS.md)
- [Project memory](06_PROJECT_MEMORY.md)
- [API and event contracts](07_API_AND_EVENTS.md)
- [Testing and acceptance](08_TESTING_AND_ACCEPTANCE.md)
- [Security and operations](09_SECURITY_AND_OPERATIONS.md)
