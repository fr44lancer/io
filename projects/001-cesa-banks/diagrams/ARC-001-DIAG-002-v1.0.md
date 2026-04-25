# Architecture Diagram: Enforcement Error Handling, Retry, and Graceful Degradation

> **Template Origin**: Official | **ArcKit Version**: 4.9.1 | **Command**: `/arckit:diagram`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-DIAG-002-v1.0 |
| **Document Type** | Architecture Diagram |
| **Project** | CESA–Banks Enforcement Integration (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-22 |
| **Last Modified** | 2026-04-22 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-22 |
| **Owner** | Project Team, Architecture Lead |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project Team, Architecture Team, CESA Programme Office |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-22 | ArcKit AI | Initial creation from `/arckit:diagram` command — X-Road error handling, retry, and graceful degradation flow | PENDING | PENDING |

---

## Diagram

### Mermaid Sequence Diagram — Error Handling, Retry, and Graceful Degradation

```mermaid
sequenceDiagram
    autonumber
    actor Officer as CESA Officer
    participant CesaIS as CESA Case<br/>Management System
    participant XRoadSS as CESA X-Road<br/>Security Server
    participant BankA as Bank A<br/>X-Road SS
    participant BankB as Bank B<br/>X-Road SS
    participant CesaDB as CESA Database

    Officer->>+CesaIS: Issue blocking order [case_id, accounts[], legal_ref]
    CesaIS->>CesaDB: Create enforcement order, status: PENDING
    CesaDB-->>CesaIS: order_id confirmed

    rect rgb(255, 230, 230)
        Note over CesaIS,BankA: Bank A - Failure Path (FR-008, NFR-A-003)
        CesaIS->>+XRoadSS: BlockAccounts(order_id, bank=BankA, legal_ref)
        XRoadSS->>BankA: POST /enforcement/block
        BankA-->>XRoadSS: 503 Service Unavailable

        loop Retry 1-3, exponential backoff (1s, 3s, 9s)
            Note over XRoadSS,BankA: Auto-retry after backoff delay
            XRoadSS->>BankA: POST /enforcement/block [retry]
            BankA-->>XRoadSS: 503 Service Unavailable
        end

        XRoadSS-->>-CesaIS: TRANSMISSION_FAILED, 3 retries exhausted
        CesaIS->>CesaDB: Update order, BankA status: FAILED
        CesaIS-->>Officer: Alert - BankA blocking failed after 3 retries
    end

    rect rgb(230, 255, 230)
        Note over CesaIS,BankB: Bank B - Success Path, graceful degradation (NFR-A-004)
        CesaIS->>+XRoadSS: BlockAccounts(order_id, bank=BankB, legal_ref)
        XRoadSS->>+BankB: POST /enforcement/block
        BankB-->>-XRoadSS: 200 OK (bank_ref, blocked_accounts, timestamp)
        XRoadSS-->>-CesaIS: blocking_confirmation (bank_ref, timestamp)
        CesaIS->>CesaDB: Update case, BankB: CONFIRMED, bank_ref stored
        CesaIS-->>Officer: Bank B blocking confirmed
    end

    Officer->>CesaIS: Mark BankA as MANUAL_FOLLOWUP [case_id, bank=BankA]
    CesaIS->>CesaDB: Update order, BankA status: MANUAL_FOLLOWUP
    CesaIS-->>-Officer: BankA removed from retry queue, manual action required
```

**View this diagram**:

- **GitHub**: Renders automatically in markdown preview
- **VS Code**: Install Mermaid Preview extension
- **Online**: https://mermaid.live (paste code above)
- **Export**: Use mermaid.live to export as PNG/SVG/PDF

---

## Diagram Scope

This diagram covers the scenario where a CESA officer issues a blocking order against accounts held at multiple banks. It shows:

1. **Initial attempt failure** — Bank A's X-Road Security Server returns a 503 error
2. **Automatic retry** — CESA IS retries up to 3 times with exponential backoff (1 s → 3 s → 9 s)
3. **Failure notification** — Officer is alerted after retries are exhausted
4. **Graceful degradation** — Bank B succeeds independently; a single bank failure does not block enforcement against other banks
5. **Manual fallback** — Officer marks Bank A as MANUAL_FOLLOWUP, removing it from the retry queue

**Relationship to DIAG-001**: DIAG-001 (ARC-001-DIAG-001-v1.0) covers the full happy-path lifecycle (account discovery, blocking, collection, release) as a PlantUML sequence diagram. This diagram focuses exclusively on the error handling path not shown in DIAG-001.

---

## Component Inventory

| Component | Type | Technology | Responsibility | Evolution Stage | Build/Buy |
|-----------|------|------------|----------------|-----------------|-----------|
| CESA Case Management System | Application | Web application, REST APIs | Case record management; enforcement order orchestration; retry state machine | Custom (0.35) | BUILD |
| CESA X-Road Security Server | Boundary / Gateway | X-Road 6, mutual TLS | Secure message routing, digital signing, transmission failure detection (NFR-A-003) | Product (0.65) | BUY |
| Bank A / B X-Road Security Server | Boundary / Gateway | X-Road 6, mutual TLS | Bank-side secure message routing; exposes CBS enforcement API over X-Road | Product (0.65) | BUY (bank-owned) |
| CESA Database | Data store | PostgreSQL | Enforcement order state, retry counters, audit trail, MANUAL_FOLLOWUP records | Commodity (0.85) | USE |

**Evolution Stage Legend**: Genesis (0.0–0.25) | Custom (0.25–0.50) | Product (0.50–0.75) | Commodity (0.75–1.0)

---

## Architecture Decisions

### Key Design Decisions

**Decision 1**: Exponential backoff with a fixed retry cap (3 retries)

- **Context**: X-Road transmission failures may be transient (e.g., bank Security Server restart, network blip). Retrying immediately amplifies load on a struggling endpoint.
- **Decision**: CESA IS retries failed transmissions automatically up to 3 times with delays of 1 s, 3 s, and 9 s (exponential backoff, base 3) before declaring the order FAILED.
- **Rationale**: Exponential backoff gives the target time to recover without hammering it. A cap of 3 retries (total elapsed time ~13 s) stays within the 5-second SLA for the blocking path only when the bank responds quickly; it provides a reasonable recovery window for transient faults while not blocking the officer UI for an unreasonable period.
- **Consequences**: Officers may receive FAILED notifications within 13 seconds of a bank outage. The MANUAL_FOLLOWUP state must be operationally supported.

**Decision 2**: Per-bank failure isolation (graceful degradation)

- **Context**: With 15+ banks participating, a single bank's X-Road Security Server failure must not prevent enforcement against other banks.
- **Decision**: Each bank's enforcement action is handled independently. A FAILED status for one bank does not affect the outcome recorded for any other bank.
- **Rationale**: Legal enforcement obligations must be fulfilled as broadly as possible. Blocking enforcement against all banks because one is unavailable could constitute a legal failure and expose CESA to challenge.
- **Consequences**: The case record must track enforcement status per bank (not a single aggregate status). Officers need a per-bank view in the CESA IS dashboard.

**Decision 3**: MANUAL_FOLLOWUP as a terminal non-retry state

- **Context**: After 3 retries are exhausted, the system cannot know whether future retries will succeed, and indefinite automated retries risk creating inconsistent enforcement state.
- **Decision**: Officers explicitly mark exhausted orders as MANUAL_FOLLOWUP, which removes them from the automated retry queue and records the need for manual action in the case audit log.
- **Rationale**: Puts the legal responsibility back with the human officer, preserving the audit trail and ensuring that manual follow-up is traceable (BR-003).
- **Consequences**: Requires a clear UI affordance in CESA IS for officers to action failed orders. Operational SLA needed for how quickly officers must act on FAILED notifications.

### Technology Choices

| Technology | Purpose | Rationale | Evolution Stage |
|------------|---------|-----------|-----------------|
| X-Road 6 retry semantics | Transport-layer fault detection | X-Road Security Server detects connection failures within its protocol timeout window (contributing to the 10-second detection target in NFR-A-003) | Product (0.65) |
| PostgreSQL | Enforcement order state store | ACID transactions ensure retry counter and status updates are atomic; prevents double-retry under concurrent load | Commodity (0.88) |

---

## Requirements Traceability

| Requirement ID | Description | Coverage in This Diagram | Status |
|----------------|-------------|--------------------------|--------|
| FR-008 | Auto-retry failed X-Road transmissions — exponential backoff (1s, 3s, 9s), max 3 retries; alert officer on exhaustion; MANUAL_FOLLOWUP option | Loop block (retries 1–3), TRANSMISSION_FAILED message, officer alert, MANUAL_FOLLOWUP flow | ✅ |
| NFR-A-003 | Detect X-Road failures within 10 s; initiate retry; single bank failure must not degrade others | Retry loop + Bank B success path running after Bank A fails | ✅ |
| NFR-A-004 | Graceful degradation — bank unreachable: indicate clearly, allow officer to proceed with manual fallback, no cascade | Bank A FAILED + Bank B CONFIRMED shown independently; MANUAL_FOLLOWUP state | ✅ |
| BR-003 | Legal non-repudiation and audit trail — every action recorded | CesaDB updates at each state transition (PENDING → FAILED → MANUAL_FOLLOWUP; CONFIRMED) | ✅ |
| BR-004 | Unified enforcement platform — all action types managed through single CESA system | CesaIS orchestrates both failure and success paths | ✅ |
| UC-002 Alt 1a | Bank returns error — order flagged FAILED; retry available | Retry loop and FAILED status update | ✅ |
| UC-002 Alt 2a | X-Road transmission failure — officer alerted; manual fallback initiated | Officer alert + MANUAL_FOLLOWUP flow | ✅ |
| NFR-P-001 | Blocking order confirmed < 5 s (p95) | Diagram shows Bank B succeeding without Bank A delay; SLA applies per-bank | ⚠️ Bank A retry window (13 s) exceeds p95 target — SLA intended for successful paths only |

**Coverage Summary**: 8 requirements addressed | 7 fully covered ✅ | 1 partial ⚠️ (NFR-P-001 latency SLA applies to success path only) | 0 not covered ❌

---

## Integration Points

### External Systems

| External System | Interface | Protocol | Responsibility | SLA |
|----------------|-----------|----------|----------------|-----|
| Bank A X-Road Security Server | X-Road REST/SOAP API | HTTPS mTLS, X-Road signed | Exposes /enforcement/block; returns 503 in this scenario | 3 s response (per bank participation agreement) |
| Bank B X-Road Security Server | X-Road REST/SOAP API | HTTPS mTLS, X-Road signed | Exposes /enforcement/block; returns 200 OK with confirmation | 3 s response (per bank participation agreement) |

### APIs and Endpoints

| API | Endpoint | Method | Purpose | Authentication |
|-----|----------|--------|---------|----------------|
| Account Block | `/enforcement/block` | POST | Apply HOLD to specified accounts | X-Road mTLS + signed message |

---

## Data Flow

### Key Data Flows in This Diagram

| Data Element | Flow | Sensitivity | Notes |
|-------------|------|-------------|-------|
| `order_id`, `accounts[]`, `legal_ref` | CESA IS → X-Road SS → Bank X-Road SS | CONFIDENTIAL | Carried in signed X-Road message; legal_ref mandatory per FR-010 |
| `503 Service Unavailable` | Bank A → X-Road SS → CESA IS | Operational | Error code triggers retry counter increment |
| `bank_ref`, `timestamp` | Bank B → X-Road SS → CESA IS | CONFIDENTIAL | Confirmation reference stored as non-repudiation evidence |
| Enforcement order status | CESA IS → CESA DB | CONFIDENTIAL | State transitions: PENDING → FAILED, PENDING → CONFIRMED, FAILED → MANUAL_FOLLOWUP |

### PII Handling

| Component | PII Type | Legal Basis | Retention | Notes |
|-----------|----------|-------------|-----------|-------|
| CESA Database | Debtor identifiers in order record | Legal obligation (RA enforcement law) | Case + 10 years (DR-006) | Encrypted at rest (NFR-SEC-003) |
| X-Road SS audit log | Message metadata, order IDs | Legal obligation | 10 years (NFR-C-002) | Tamper-evident; bank-side logs independently held |

**DPIA Required**: Yes (recommended — large-scale processing of personal financial data under legal compulsion, per NFR-C-003)

---

## Security Architecture

### Security Zones

| Zone | Components | Security Level | Controls |
|------|------------|----------------|----------|
| CESA Internal | CESA IS, CESA DB | HIGH | RBAC (NFR-SEC-004), MFA for officers (NFR-SEC-005), audit logging (NFR-C-002) |
| CESA DMZ | CESA X-Road Security Server | HIGH | mTLS, message signing, IP allowlisting, rate limiting |
| Inter-network | X-Road channel | HIGH | TLS 1.3, X-Road signed payloads, OCSP validation |
| Bank DMZ | Bank X-Road Security Server | HIGH | Bank-side access restricted to CESA SS certificate (NFR-SEC-006) |

### Authentication

| Layer | Mechanism | Standard |
|-------|-----------|---------|
| Transport | Mutual TLS (X.509) | RFC 8446 (TLS 1.3) |
| Message | X-Road digital signature (RSA-2048 / ECDSA-256) | X-Road Protocol v4 (NFR-SEC-002) |
| Officer to CESA IS | MFA (smart card / OTP) | NFR-SEC-005 |

---

## Non-Functional Requirements Coverage

### Performance

| Requirement | Target | How Addressed |
|-------------|--------|---------------|
| NFR-P-001: Blocking order p95 latency | < 5 s | Bank B path shows direct success within 3 s bank SLA + < 2 s X-Road transport. Bank A retry window (max 13 s) is an exceptional path — p95 target applies to successful transmissions. |
| NFR-A-003: Failure detection | Within 10 s | X-Road SS detects connection timeout; retry loop begins immediately. Total retry window ≈ 13 s (1+3+9 s delays). |

### Availability and Resilience

| Requirement | Target | How Addressed |
|-------------|--------|---------------|
| NFR-A-003 | Single bank failure does not degrade others | Bank A failure path and Bank B success path are independent; no shared state or blocking dependency |
| NFR-A-004 | Graceful degradation for unreachable banks | FAILED status + MANUAL_FOLLOWUP state allows officer to proceed; CESA IS and other bank paths unaffected |

---

## Diagram Quality Gate

| # | Criterion | Target | Result | Status |
|---|-----------|--------|--------|--------|
| 1 | Edge crossings | 0 (sequence diagrams have no crossings) | 0 | PASS |
| 2 | Visual hierarchy | Failure path and success path clearly distinguished | `rect rgb(...)` blocks with contrasting red/green backgrounds | PASS |
| 3 | Grouping | Related messages grouped within rect blocks | Bank A failure path and Bank B success path each in own rect block | PASS |
| 4 | Flow direction | Top-to-bottom (inherent in sequence diagrams) | Consistent TB throughout | PASS |
| 5 | Relationship traceability | All arrows labelled with operation or result | All arrows carry meaningful labels; no unlabelled transitions | PASS |
| 6 | Abstraction level | Single level — system interaction sequence | Sequence only; no mixed C4 levels; no internal component details | PASS |
| 7 | Edge label readability | Labels concise, no overlap | Labels are short phrases; `autonumber` aids reference | PASS |
| 8 | Node placement | Fixed lifelines; failure bank adjacent to X-Road SS | BankA declared before BankB; XRoadSS is the shared intermediary between both paths | PASS |
| 9 | Element count | 6 lifelines vs 8 max | 6 / 8 | PASS |

All 9 criteria: **PASS**

---

## Linked Artifacts

| Artifact | Path |
|----------|------|
| Full lifecycle sequence diagram (PlantUML) | `projects/001-cesa-banks/diagrams/ARC-001-DIAG-001-v1.0.md` |
| Requirements | `projects/001-cesa-banks/ARC-001-REQ-v1.0.md` |
| Data Model | `projects/001-cesa-banks/ARC-001-DATA-v1.0.md` |
| Roadmap | `projects/001-cesa-banks/ARC-001-ROAD-v1.0.md` |
| Source Business Process | `projects/001-cesa-banks/external/CESA-BANKS-BP.pdf` |

---

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| CBBP | CESA-BANKS-BP.pdf | Business Process | `projects/001-cesa-banks/external/` | Existing and to-be BP swimlane diagrams covering enforcement lifecycle across RA commercial banks |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Description |
|-------------|--------|--------------|----------|-------------|
| CBBP-C2 | CBBP | Page 1 — TO-BE swimlane | Functional Requirement | TO-BE state shows enforcement transmitted via X-Road with real-time confirmation — retry and fallback are implied operational requirements for any real-time channel |

---

**Generated by**: ArcKit `/arckit:diagram` command
**Generated on**: 2026-04-22 GMT
**ArcKit Version**: 4.9.1
**Project**: CESA–Banks Enforcement Integration (Project 001)
**AI Model**: claude-sonnet-4-6
**Generation Context**: Derived from ARC-001-REQ-v1.0.md (FR-008, NFR-A-003, NFR-A-004, UC-002 alternative flows) and ARC-001-DIAG-001-v1.0.md (existing happy-path coverage). This diagram covers the error handling and graceful degradation scenario not present in DIAG-001.
