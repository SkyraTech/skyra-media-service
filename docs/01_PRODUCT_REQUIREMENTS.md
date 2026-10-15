# Skyra Media Generation Service — Product Requirements

## Maintained specification — current status

Updated 2026-10-14. This is one of the nine initial project documents and must be retained and updated in place. Remove only redundant per-work reports; do not replace or delete the initial specification set.

Specification only; no generation provider or durable job runner implemented.

The following references hold the detailed current implementation; requirements and proposed designs below must not be read as already built:

- [Current architecture and database design](ARCHITECTURE.md)
- [Current functionality and implementation boundaries](FUNCTIONALITY.md)
- [Current milestone and verification summary](DEVELOPMENT.md)

Prepared: 2026-10-14. Requirement/design baseline. Use the maintained current-status section above to distinguish implemented work from planned work.

## Product overview

Provider-independent job management for image and video generation, revisions and deliverables used by Jarvis and commercial products.

## Problem and current baseline

Initial baseline: documentation-only project at the time of specification; current implementation status is stated above. No image/video generation worker or provider connection has been implemented in this folder.

Existing prototypes do not establish production readiness. The objective is a reusable, testable boundary with explicit ownership and verifiable outcomes.

## Target users and goals

Primary users: Skyra owner and authorized employees; consuming applications and delegated agents act under those users' scoped identities. Commercial customers use separately branded products rather than inheriting internal Jarvis privileges.

Success means the capabilities below pass recorded acceptance checks, survive expected failures and expose enough evidence for a human to review the result.

## Core requirements / MVP

- **FR-01:** Provider capability registry for image/video formats and supported edits
- **FR-02:** Versioned briefs, reference assets, generation jobs and revision lineage
- **FR-03:** Cost estimates, reservations, budget limits and actual usage recording
- **FR-04:** Asynchronous polling/webhooks with duplicate prevention
- **FR-05:** Preview/review states and validated output metadata
- **FR-06:** Separate approval for downstream publication

## Boundaries

This project delivers its declared capabilities only. No automatic production release, account creation, purchase or broader permission is implied by an AI plan. Article-dashboard implementation, ERP, Skyra Platform and QR changes are outside this documentation initiative. Future local models and hosted Jarvis must preserve the same authorization contracts.

## User journey

An authorized caller selects a capability and resource scope, submits validated input, receives either a result or a durable job reference, follows progress and retrieves evidence. Policy may require an exact-action approval before execution. Failures present recovery guidance without claiming success.

## Acceptance and unresolved decisions

See [testing](08_TESTING_AND_ACCEPTANCE.md) for release evidence and [tasks](05_PROJECT_TASKS.md) for implementation sequence.

- Provider pricing, licensing and retention require verification before selecting adapters
- Cancellation may not reverse provider charges
- Local GPU generation remains a future adapter, not a release prerequisite
