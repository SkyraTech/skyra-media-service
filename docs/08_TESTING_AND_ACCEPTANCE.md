# Skyra Media Generation Service — Testing and Acceptance

Prepared: 2026-10-14. Status: proposed implementation baseline. User requirements are captured here; technical choices remain subject to implementation validation.

## Project acceptance matrix

| ID | Required outcome | Evidence status |
|---|---|---|
| AC-01 | Unsupported output requests fail before a paid provider call | Not executed |
| AC-02 | Retries cannot silently create additional paid generation jobs | Not executed |
| AC-03 | Output type/dimensions/duration match the selected contract or fail validation | Not executed |
| AC-04 | Every asset retains source brief, provider and revision lineage | Not executed |
| AC-05 | Generation completion never automatically implies publishing approval | Not executed |

## Requirement traceability

Each requirement must receive one or more concrete test IDs. The matrix above captures critical scenarios but does not imply exhaustive feature coverage.

| Requirement | Behavior to verify | Test mapping |
|---|---|---|
| FR-01 | Provider capability registry for image/video formats and supported edits | Unassigned; required before implementation completion |
| FR-02 | Versioned briefs, reference assets, generation jobs and revision lineage | Unassigned; required before implementation completion |
| FR-03 | Cost estimates, reservations, budget limits and actual usage recording | Unassigned; required before implementation completion |
| FR-04 | Asynchronous polling/webhooks with duplicate prevention | Unassigned; required before implementation completion |
| FR-05 | Preview/review states and validated output metadata | Unassigned; required before implementation completion |
| FR-06 | Separate approval for downstream publication | Unassigned; required before implementation completion |

## Test layers

- Unit: domain decisions, policy evaluation, state transitions, parsing and failure classification.
- Contract: input/output examples, error shape, consumer compatibility and event schemas.
- Integration: real isolated storage, adapter behavior, credentials scoping, retries and provider sandbox where available.
- End-to-end: authorized user workflow through actual boundaries; Playwright where a browser/UI is involved and Windows process tests for desktop launches.
- Recovery/security: crash between intent and dispatch, duplicate events, expired leases, denied scopes, cross-tenant attempts, stale approvals and secret redaction.

For package-only projects, independent consumer tests replace server/deployment tests. Provider tests must use approved test accounts; do not send messages, publish content or incur charges against arbitrary live users.

## Release gate

Record commit, tool/dependency versions, test command, environment, timestamps, result and artifact links. All required checks must pass or carry an explicitly reviewed exception. Track line and branch coverage separately; establish project thresholds from the first trustworthy baseline and protect critical paths with direct behavioral tests. A high coverage percentage alone is not acceptance.

Dependency and vulnerability findings are triaged by severity, exploitability and reachability. No unreviewed critical/high finding in the release scope. Active DAST requires an owned, explicitly selected target; baseline scans and active attacks are different operations. Quality runners must isolate untrusted code and cap runtime/resource usage.

No runtime tests were performed by this documentation pass. Future reports must distinguish simulated providers, local integration and production-like verification.
