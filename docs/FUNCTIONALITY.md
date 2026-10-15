# Skyra Media Generation Service — Functionality

Last maintained: 2026-10-14. This is the canonical project requirement/capability reference. Current implementation and planned work are explicitly distinguished.

## Product and users

Provider-independent job management for image and video generation, revisions and deliverables used by Jarvis and commercial products.

Users: Skyra owner and authorized employees; service consumers act under scoped user/project/account identity. Commercial products stay independent of internal Jarvis privileges.

## Current implementation

Specification only; no generation provider or durable job runner implemented.

## Required capabilities

- Provider capability registry for image/video formats and supported edits
- Versioned briefs, reference assets, generation jobs and revision lineage
- Cost estimates, reservations, budget limits and actual usage recording
- Asynchronous polling/webhooks with duplicate prevention
- Preview/review states and validated output metadata
- Separate approval for downstream publication

## Interface direction

The following interfaces are design proposals from the project baseline, not a guarantee of working endpoints. Existing prototype routes must be checked against their source before consumer integration.

| Proposed operation | Purpose |
|---|---|
| `POST /v1/media-jobs` | Validate capabilities and budget; return generation job ID |
| `GET /v1/media-jobs/{id}` | Return provider state and artifact references |
| `POST /v1/media-jobs/{id}/revisions` | Create a new version linked to source assets |
| `POST /v1/webhooks/{provider}` | Authenticate and reconcile provider completion |

## Acceptance requirements

- Unsupported output requests fail before a paid provider call
- Retries cannot silently create additional paid generation jobs
- Output type/dimensions/duration match the selected contract or fail validation
- Every asset retains source brief, provider and revision lineage
- Generation completion never automatically implies publishing approval

## Explicit boundaries and open decisions

- Provider pricing, licensing and retention require verification before selecting adapters
- Cancellation may not reverse provider charges
- Local GPU generation remains a future adapter, not a release prerequisite

A proposal, simulation or passing build does not authorize production release. Account connection, publication, money movement and employee/payroll actions obey their configured permission policies.

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
