# Project Requirements: CESA–Commercial Banks Enforcement Integration

> **Template Origin**: Official | **ArcKit Version**: 4.9.1 | **Command**: `/arckit:requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v1.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | CESA–Banks Enforcement Integration (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-22 |
| **Last Modified** | 2026-04-22 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-22 |
| **Owner** | Programme Lead, CESA IT Department |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project Team, Architecture Team, CESA Programme Office, Commercial Bank Representatives |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-22 | ArcKit AI | Initial creation from `/arckit:requirements` command — derived from CESA-BANKS-BP.pdf | PENDING | PENDING |

## Document Purpose

This document defines the business and technical requirements for the automated enforcement data exchange between the Armenian State Enforcement Service (CESA) and commercial banks in Armenia. It establishes the requirements baseline for replacing the existing manual process with a real-time, X-Road-backed API integration. This document is the authoritative reference for all downstream design, procurement, testing, and bank onboarding activities.

---

## Executive Summary

### Business Context

The Armenian State Enforcement Service (CESA) currently processes enforcement actions against debtor bank accounts through a manual workflow: documents are prepared, reviewed, and physically or electronically dispatched to individual commercial banks [CBBP-C1]. Banks then manually apply account holds, execute fund seizures, or lift restrictions. This process introduces delays ranging from hours to days between the issuance of a legal enforcement order and its execution at the bank — creating material risk that assets may be dissipated before enforcement occurs.

The to-be state replaces this manual workflow with a fully automated, real-time API integration layer. All commercial banks licensed by the Central Bank of Armenia will be connected to CESA's enforcement system via X-Road — the national e-Government interoperability platform [CBBP-C2]. Enforcement actions (account blocking, fund collection, restriction lifting) will be initiated by a CESA officer and executed at the bank within seconds, with cryptographically signed confirmation returned in real time.

This project directly supports Armenia's digital government modernisation agenda and strengthens the practical enforceability of judicial and administrative decisions by making enforcement immediate, verifiable, and auditable.

### Objectives

- Replace manual enforcement document dispatch with real-time, API-based enforcement across all Armenian commercial banks
- Eliminate asset dissipation risk caused by delays in the existing manual process
- Establish a unified, legally non-repudiable enforcement channel with end-to-end audit trail
- Enable CESA officers to discover debtor accounts across all banks without manual bank-by-bank coordination [CBBP-C3]
- Create a scalable, standards-based infrastructure capable of onboarding all licensed commercial banks

### Expected Outcomes

- Enforcement execution time reduced from hours/days to under 5 seconds per bank
- Zero manual steps required to transmit and confirm enforcement orders for X-Road-connected banks
- 100% audit trail coverage for all enforcement actions, with cryptographic verifiability
- All Armenian commercial banks connected to the X-Road enforcement channel within 12 months of go-live
- CESA officer time spent on enforcement dispatch reduced by more than 80%

### Project Scope

**In Scope**:
- CESA Case Management System (enforcement API orchestration, case record management)
- CESA X-Road Security Server provisioning and configuration
- Bank-side X-Road enforcement API specification (block, collect, release, query)
- Bank X-Road Security Server integration requirements and certification process
- Account discovery (enquiry) across all X-Road member banks [CBBP-C3]
- Audit logging, case record management, and reporting
- CESA collection account integration for fund transfer destination

**Out of Scope**:
- Bank Core Banking System internal implementation (each bank is responsible for its own CBS adapter)
- Court/judicial case management systems (legal order generation is an upstream dependency)
- X-Road Central Server and CA management (operated by EKENG or successor body)
- Tax authority or customs enforcement integrations (separate initiative)
- Direct citizen-facing interfaces

---

## Stakeholders

| Stakeholder | Role | Organisation | Involvement Level |
|-------------|------|--------------|-------------------|
| CESA Leadership | Executive Sponsor | CESA | Decision maker |
| CESA Programme Manager | Programme Lead | CESA | Requirements owner |
| CESA Enforcement Officers | Primary End Users | CESA | Requirements input, UAT |
| CESA IT Department | Technical Owner | CESA | System implementation |
| Commercial Bank IT Leads | Integration Partners | Commercial Banks | API implementation, testing |
| Central Bank of Armenia (CBA) | Regulator / Coordinator | CBA | Bank onboarding oversight |
| EKENG (or successor) | X-Road Platform Operator | e-Gov Infrastructure | X-Road registration, OCSP |
| Ministry of Justice | Legal Authority | Government | Legal compliance review |
| Data Protection Authority (RA) | Regulatory Body | Government | Personal data oversight |

---

## Business Requirements

### BR-001: Real-Time Enforcement Execution

**Description**: The system must execute enforcement actions (account blocking, fund collection, restriction lifting) against debtor accounts at commercial banks in real time — confirmed within 5 seconds of order submission. [CBBP-C2]

**Rationale**: The existing manual process introduces delays of hours to days between legal order issuance and bank execution [CBBP-C1]. This window creates risk of asset dissipation and undermines the legal effectiveness of court orders.

**Success Criteria**:
- Enforcement order submitted by a CESA officer is confirmed by bank CBS within 5 seconds (95th percentile)
- Zero manual steps required in the transmission path between CESA IS and bank CBS
- Blocking functionality operates 24/7; collection and release operate during defined banking hours

**Priority**: MUST_HAVE

**Stakeholder**: CESA Leadership, Ministry of Justice

---

### BR-002: Automated Account Discovery

**Description**: Before issuing enforcement orders, CESA must be able to query all X-Road member commercial banks simultaneously to discover which institutions hold accounts for a specified debtor, identified by national SSN or tax ID. [CBBP-C3]

**Rationale**: Officers currently must know in advance which banks hold debtor accounts. Automated discovery enables complete enforcement across all bank relationships and prevents partial enforcement.

**Success Criteria**:
- Discovery query returns results from all registered banks within 30 seconds
- Results include account type, currency, status, and balance range (not precise balance — data minimisation)
- Discovery is available to all authorised CESA officers without bank-specific manual steps

**Priority**: MUST_HAVE

**Stakeholder**: CESA Enforcement Officers, CESA Leadership

---

### BR-003: Legal Non-Repudiation and Audit Trail

**Description**: Every enforcement action must be accompanied by a cryptographically signed, tamper-evident audit record that can be produced as legal evidence. [CBBP-C4]

**Rationale**: Enforcement actions have significant legal consequences. Neither CESA nor the bank should be able to deny that an enforcement action was issued or executed. Audit records may be required in court proceedings or regulatory reviews.

**Success Criteria**:
- All enforcement messages are digitally signed by the originating X-Road Security Server
- Audit logs are stored independently on both CESA and bank sides
- Any enforcement action's audit record can be retrieved and verified within 30 seconds
- Audit records are retained for the full legally required period (see DR-006)

**Priority**: MUST_HAVE

**Stakeholder**: Ministry of Justice, CESA Leadership

---

### BR-004: Unified Enforcement Platform for All Action Types

**Description**: All enforcement action types — account blocking, fund collection, and restriction lifting — must be managed through a single, unified CESA system, eliminating the current fragmented bank-by-bank, action-by-action manual process. [CBBP-C1]

**Rationale**: The existing process involves different workflows and document formats for each enforcement type and each bank. A unified platform reduces officer training burden, process errors, and inconsistency. [CBBP-C5]

**Success Criteria**:
- Single CESA officer interface for all enforcement action types
- Consistent API contract across all banks (no bank-specific workarounds in CESA IS)
- Case management system tracks all enforcement actions against a case in a single unified record

**Priority**: MUST_HAVE

**Stakeholder**: CESA Enforcement Officers, CESA Programme Manager

---

### BR-005: Phased Bank Onboarding

**Description**: The system must support phased onboarding of commercial banks, allowing early-adopter banks to operate in real-time mode while others complete X-Road Security Server configuration, without disrupting the overall system. [CBBP-C5]

**Rationale**: It is not feasible to onboard all commercial banks simultaneously. The system must clearly distinguish X-Road-enabled banks from those requiring manual follow-up, and onboarding a new bank must require no core system code changes.

**Success Criteria**:
- System maintains a bank registry indicating X-Road onboarding status per bank
- Officers see clearly which banks are real-time enabled and which require manual action
- Adding a new bank to the X-Road enforcement channel requires configuration only, not code change

**Priority**: SHOULD_HAVE

**Stakeholder**: CESA Programme Manager, Central Bank of Armenia

---

### BR-006: CESA Officer Efficiency Improvement

**Description**: CESA enforcement officers must experience a measurable reduction in time and effort spent on enforcement document preparation and bank coordination. [CBBP-C1]

**Rationale**: The existing manual process is labour-intensive and error-prone. The investment in automation must deliver tangible efficiency gains quantifiable against the current baseline.

**Success Criteria**:
- Time to initiate and confirm a blocking order reduced by more than 80% vs. current manual process
- Zero manual document preparation required for X-Road enforcement actions
- Officers can manage at least 3 times more cases per day than under the current process

**Priority**: SHOULD_HAVE

**Stakeholder**: CESA Enforcement Officers, CESA Leadership

---

## Functional Requirements

### User Personas

#### Persona 1: CESA Enforcement Officer (Bailiff)

- **Role**: Processes enforcement orders on behalf of creditors; initiates account discovery, issues blocking/collection/release orders
- **Goals**: Execute enforcement orders quickly, completely, and with a verifiable audit trail; know the status of each action in real time
- **Pain Points**: Manual document preparation; uncertainty about which banks hold debtor accounts; slow bank response; no unified status view
- **Technical Proficiency**: Medium — comfortable with standard office and case management systems

#### Persona 2: CESA Supervisor / Departmental Head

- **Role**: Oversees enforcement caseload; reviews enforcement throughput and success rates; approves high-value collection orders
- **Goals**: Monitor enforcement throughput; ensure legal compliance; identify bottlenecks or failed actions
- **Pain Points**: No real-time visibility into enforcement status; reliance on officer-reported information
- **Technical Proficiency**: Medium

#### Persona 3: Bank Compliance Officer

- **Role**: Receives enforcement orders at the bank side; ensures CBS applies them correctly; manages disputes and exceptions
- **Goals**: Receive clear, authenticated, structured enforcement instructions; apply them accurately; return confirmation to CESA
- **Pain Points**: Manual review of enforcement documents; non-standard formats across senders; no structured API contract
- **Technical Proficiency**: Medium-High

#### Persona 4: CESA System Administrator

- **Role**: Manages CESA IS and X-Road Security Server; monitors integration health; manages bank onboarding in the registry
- **Goals**: Maintain high availability; monitor for failed transmissions; certify and onboard new banks
- **Technical Proficiency**: High

---

### Use Cases

#### UC-001: Account Discovery

**Actor**: CESA Enforcement Officer

**Preconditions**: Officer is authenticated; enforcement case is open with legal basis; debtor SSN or tax ID is known

**Main Flow**:
1. Officer selects "Discover Accounts" for a case
2. CESA IS broadcasts discovery query to all X-Road registered banks simultaneously
3. Each bank returns accounts held for the debtor (type, currency, status, balance range)
4. CESA IS aggregates results and presents a unified account overview
5. Officer reviews results and selects accounts for enforcement action

**Alternative Flows**:
- Alt 1a: Bank not X-Road registered — flagged as "Manual follow-up required" in results
- Alt 2a: Bank returns error — flagged as "Query failed" with retry option available

**Priority**: CRITICAL

---

#### UC-002: Issue Account Blocking Order

**Actor**: CESA Enforcement Officer

**Preconditions**: Account discovery completed; legal basis / court order reference available; officer has blocking authority

**Main Flow**:
1. Officer selects accounts to block and enters legal basis reference
2. System validates order inputs (legal reference present, accounts selected)
3. System transmits signed blocking order to each target bank via X-Road
4. Each bank CBS applies HOLD status and returns confirmation with bank reference and timestamp
5. CESA IS displays real-time confirmation per bank; case record updated

**Alternative Flows**:
- Alt 1a: Bank returns error — order flagged FAILED for that bank; retry available
- Alt 2a: X-Road transmission failure — officer alerted; manual fallback initiated

**Priority**: CRITICAL

---

#### UC-003: Issue Fund Collection Order

**Actor**: CESA Enforcement Officer

**Preconditions**: Target account(s) identified; collection amount specified; CESA collection account IBAN is configured

**Main Flow**:
1. Officer specifies amount (AMD) and target accounts
2. System transmits signed collection order to bank(s) via X-Road
3. Bank CBS checks available balance; transfers funds to CESA collection account
4. Bank returns collection result (amount collected, any shortfall)
5. CESA IS records outcome and notifies officer

**Alternative Flows**:
- Alt 1a: Partial funds — bank transfers available balance; shortfall flagged for follow-up
- Alt 2a: Zero balance — INSUFFICIENT_FUNDS returned; officer notified; account remains blocked

**Priority**: CRITICAL

---

#### UC-004: Lift Account Restrictions

**Actor**: CESA Enforcement Officer

**Preconditions**: Legal basis for restriction lifting exists (court order, full collection, correction); accounts to release identified

**Main Flow**:
1. Officer selects accounts to release and enters legal basis for release
2. System transmits signed release order to bank(s) via X-Road
3. Bank CBS removes HOLD status; normal account operation restored
4. Bank returns release confirmation with timestamp
5. CESA IS records release; enforcement action on case marked CLOSED

**Priority**: CRITICAL

---

### Functional Requirements Detail

#### FR-001: Account Discovery Broadcast

**Description**: The system must broadcast an account discovery query to all X-Road registered commercial banks simultaneously using the debtor's SSN or tax ID as the search key. [CBBP-C3]

**Relates To**: BR-002, UC-001

**Acceptance Criteria**:
- [ ] Given a valid debtor identifier, when a discovery query is submitted, then all X-Road registered banks receive the query within 3 seconds
- [ ] Given a bank response, when accounts are found, then account type, currency, status, and balance range are returned (not precise balance)
- [ ] Given a bank with no debtor accounts, when queried, then an empty result is returned — not an error

**Data Requirements**:
- Input: Debtor SSN or tax ID, case ID, legal basis reference
- Output: Per-bank list of accounts with type, currency, status, balance range
- Validation: Debtor identifier format validated before transmission

**Priority**: MUST_HAVE | **Complexity**: HIGH

---

#### FR-002: Account Blocking via X-Road

**Description**: The system must transmit a signed, structured account blocking order to a target bank's X-Road Security Server, carrying the legal order reference, affected account IDs, and CESA case ID. [CBBP-C2]

**Relates To**: BR-001, BR-003, UC-002

**Acceptance Criteria**:
- [ ] Given a blocking order, when transmitted, then the X-Road message is digitally signed by CESA Security Server
- [ ] Given a valid blocking order, when the bank CBS applies the HOLD, then confirmation includes bank reference, timestamp, and affected account IDs
- [ ] Given a successful blocking confirmation, when received, then the case record is updated within 1 second

**Priority**: MUST_HAVE | **Complexity**: HIGH

---

#### FR-003: Fund Collection via X-Road

**Description**: The system must transmit a fund collection order specifying the amount in AMD, source account, and CESA destination IBAN, and must correctly handle full, partial, and zero-balance outcomes. [CBBP-C2]

**Relates To**: BR-001, BR-004, UC-003

**Acceptance Criteria**:
- [ ] Given sufficient funds, when a collection order is received by the bank, then the full amount is transferred and confirmed
- [ ] Given insufficient funds, when a collection order is received, then the available balance is transferred and a shortfall is reported
- [ ] Given zero balance, when a collection order is received, then INSUFFICIENT_FUNDS is returned and no transfer is made

**Priority**: MUST_HAVE | **Complexity**: HIGH

---

#### FR-004: Restriction Lifting via X-Road

**Description**: The system must transmit a signed restriction release order to the bank, including the legal basis for release, and confirm removal of the HOLD status. [CBBP-C2]

**Relates To**: BR-001, BR-004, UC-004

**Acceptance Criteria**:
- [ ] Given a valid release order, when transmitted and accepted, then HOLD status is removed and confirmation returned
- [ ] Given a release confirmation, when received by CESA IS, then the enforcement action is marked RESTRICTIONS_LIFTED in the case record

**Priority**: MUST_HAVE | **Complexity**: MEDIUM

---

#### FR-005: Enforcement Case Record Management

**Description**: All enforcement actions (discovery, block, collect, release) must be recorded against the CESA case record with full status history, timestamps, bank references, and legal basis.

**Relates To**: BR-003, BR-004

**Acceptance Criteria**:
- [ ] Each enforcement action creates a timestamped audit entry in the case record
- [ ] The case record shows current enforcement status across all banks (per-bank status)
- [ ] Officers can retrieve enforcement history for any case without accessing raw system logs

**Priority**: MUST_HAVE | **Complexity**: MEDIUM

---

#### FR-006: Bank Registry Management

**Description**: The system must maintain a configurable registry of X-Road registered banks, their X-Road member identifiers, and their enforcement API onboarding status. [CBBP-C5]

**Relates To**: BR-005

**Acceptance Criteria**:
- [ ] Adding a new bank to the registry requires configuration only — no code change
- [ ] Banks can be in state: ACTIVE (X-Road enforcement enabled), ONBOARDING, or MANUAL_ONLY
- [ ] Discovery and enforcement messages are only sent to ACTIVE banks

**Priority**: SHOULD_HAVE | **Complexity**: LOW

---

#### FR-007: Enforcement Status Dashboard

**Description**: CESA supervisors must be able to view real-time enforcement throughput, action success/failure rates, and outstanding failed actions across all cases and banks.

**Relates To**: BR-006

**Acceptance Criteria**:
- [ ] Dashboard shows enforcement actions per type in the last 24 hours
- [ ] Failed enforcement attempts are visible with bank ID, case ID, and error reason
- [ ] Dashboard data is no more than 60 seconds stale

**Priority**: SHOULD_HAVE | **Complexity**: MEDIUM

---

#### FR-008: Retry and Manual Fallback Handling

**Description**: The system must automatically retry failed X-Road transmissions using exponential backoff, alert officers when retries are exhausted, and provide a manual fallback option.

**Relates To**: BR-001, BR-005

**Acceptance Criteria**:
- [ ] Failed transmissions are retried automatically up to 3 times (delays: 1s, 3s, 9s)
- [ ] After 3 failed retries, the officer is notified with failure reason and bank identifier
- [ ] Officer can mark a failed action as MANUAL_FOLLOWUP, removing it from the automated retry queue

**Priority**: MUST_HAVE | **Complexity**: MEDIUM

---

#### FR-009: Bank Enforcement API Specification

**Description**: CESA must publish a standardised API specification (OpenAPI 3.0 or WSDL) defining the four enforcement endpoints that all X-Road member banks must implement. [CBBP-C2]

**Relates To**: BR-001, INT-003

**Acceptance Criteria**:
- [ ] All four API operations (query, block, collect, release) are fully specified in a published API specification document
- [ ] Banks must demonstrate implementation of all four endpoints to receive certification for X-Road enforcement integration
- [ ] API responses follow the agreed structured format with machine-readable status and error codes

**Priority**: MUST_HAVE | **Complexity**: HIGH

---

#### FR-010: Legal Reference Validation

**Description**: The system must validate that all enforcement orders include a valid legal basis reference (court order number, administrative decision reference) before transmission.

**Relates To**: BR-003

**Acceptance Criteria**:
- [ ] An enforcement order without a legal reference is rejected at submission with a clear error message
- [ ] Legal reference format is validated against configured patterns
- [ ] The legal reference is included verbatim in the X-Road message payload and in the CESA audit log

**Priority**: MUST_HAVE | **Complexity**: LOW

---

## Non-Functional Requirements

### Performance Requirements

#### NFR-P-001: Enforcement Order End-to-End Latency

**Requirement**: Account blocking orders must be confirmed (HOLD applied at bank CBS; confirmation received at CESA IS) within 5 seconds at the 95th percentile. [CBBP-C2]

**Load Conditions**:
- Peak concurrent enforcement operations: 50 simultaneous orders (to be validated with CESA operational data)
- Bank CBS processing time SLA: < 3 seconds (allowing 2 seconds for X-Road transport)

**Measurement Method**: Timestamp delta between CESA IS order submission and confirmation receipt, logged in audit record

**Priority**: CRITICAL

---

#### NFR-P-002: Account Discovery Latency

**Requirement**: Account discovery must return aggregated results from all X-Road registered banks within 30 seconds at the 95th percentile.

**Measurement Method**: Time from officer query submission to display of aggregated results in CESA IS

**Priority**: HIGH

---

#### NFR-P-003: Collection Order Processing

**Requirement**: Fund collection orders must be confirmed (transfer completed or failure reported) within 15 seconds at the 95th percentile.

**Priority**: HIGH

---

### Availability and Resilience Requirements

#### NFR-A-001: System Availability

**Requirement**: The CESA IS enforcement module and X-Road Security Server must achieve 99.9% availability (fewer than 9 hours unplanned downtime per year). Account blocking functionality must be available 24 hours a day, 7 days a week for time-critical enforcement. Collection and release operate during defined banking hours.

**Maintenance Windows**: Planned maintenance between 01:00 and 05:00 local time on weekdays, with 48-hour advance notice. Emergency maintenance with 2-hour advance notice.

**Priority**: CRITICAL

---

#### NFR-A-002: Disaster Recovery

**RPO (Recovery Point Objective)**: Maximum acceptable data loss = 1 hour

**RTO (Recovery Time Objective)**: Maximum acceptable downtime in a DR scenario = 4 hours

**Backup Requirements**:
- Case database: Continuous replication + daily full backup, retained for 90 days minimum
- X-Road audit logs: Daily backup, retained per legal retention schedule (DR-006)
- Backups encrypted at rest

**Priority**: HIGH

---

#### NFR-A-003: X-Road Channel Fault Tolerance

**Requirement**: The system must detect X-Road transmission failures within 10 seconds and initiate retry logic automatically (FR-008). Failure of a single bank's X-Road Security Server must not degrade enforcement against other banks.

**Priority**: CRITICAL

---

#### NFR-A-004: Graceful Degradation

**Requirement**: If the X-Road channel is unavailable for a specific bank, CESA IS must clearly indicate that bank as unreachable and allow officers to proceed with manual fallback for that bank, without any system failure or cascading effect.

**Priority**: HIGH

---

### Scalability Requirements

#### NFR-S-001: Bank Ecosystem Scale

**Requirement**: The system must support all commercial banks licensed by the Central Bank of Armenia (currently approximately 15 banks) without architectural changes. The design must accommodate up to 50 banks to future-proof the integration.

**Priority**: MUST_HAVE

---

#### NFR-S-002: Concurrent Enforcement Operations

**Requirement**: The system must handle at least 100 concurrent enforcement operations (across all banks and action types) without degradation to the latency targets in NFR-P-001.

**Priority**: HIGH

---

### Security Requirements

#### NFR-SEC-001: Mutual TLS Authentication

**Requirement**: All communication between the CESA X-Road Security Server and bank X-Road Security Servers must use mutual TLS (mTLS) with X.509 certificates issued by the X-Road Certificate Authority. No unauthenticated connections are permitted. [CBBP-C4]

**Priority**: CRITICAL

---

#### NFR-SEC-002: Message Signing and Non-Repudiation

**Requirement**: All enforcement messages transmitted via X-Road must be digitally signed by the sending Security Server (RSA-2048 or ECDSA-256 minimum). Signatures must be independently verifiable by either party without reliance on the other's systems. [CBBP-C4]

**Priority**: CRITICAL

---

#### NFR-SEC-003: Data Encryption at Rest

**Requirement**: All data stored in the CESA IS database — enforcement case data, debtor personal data, financial data — must be encrypted at rest using AES-256.

**Encryption Scope**:
- [ ] Database encryption at rest
- [ ] Backup storage encryption
- [ ] X-Road audit log storage encryption

**Priority**: CRITICAL

---

#### NFR-SEC-004: Role-Based Access Control

**Requirement**: CESA IS must implement RBAC with the following minimum roles: Enforcement Officer (initiate discovery and orders), Supervisor (view all cases, approve high-value collections), System Administrator (bank registry, system configuration), Auditor (read-only audit log access).

**Priority**: HIGH

---

#### NFR-SEC-005: Multi-Factor Authentication for Officers

**Requirement**: All CESA officers must authenticate to CESA IS using a minimum of username/password plus one additional factor (smart card, OTP application, or equivalent) before initiating any enforcement action.

**Priority**: HIGH

---

#### NFR-SEC-006: Bank-Side API Access Restriction

**Requirement**: Banks must restrict access to their enforcement API endpoints to the CESA X-Road Security Server certificate and registered IP range. No direct internet access to enforcement endpoints is permitted outside the X-Road protocol.

**Priority**: CRITICAL

---

### Compliance and Regulatory Requirements

#### NFR-C-001: Armenian Enforcement Law Compliance

**Requirement**: The system must implement all enforcement action types prescribed by the RA Law on Enforcement Proceedings and any implementing regulations issued by the Ministry of Justice. Legal order references must be carried in all enforcement messages. [CBBP-C4]

**Priority**: CRITICAL

---

#### NFR-C-002: Comprehensive Audit Logging

**Requirement**: All enforcement actions must be logged with full context: Who (officer identity and role), What (action type, parameters, legal basis), When (UTC timestamp to millisecond precision), Where (system component, case ID), Legal basis (court order reference), Result (success/failure/partial), Bank reference (confirmation ID returned by bank).

**Log Retention**: Minimum 10 years from the date of the enforcement action, or the statutory period defined by RA enforcement law — whichever is longer.

**Log Integrity**: Audit logs must be stored in a tamper-evident format (cryptographic hash chaining or equivalent immutable storage).

**Priority**: CRITICAL

---

#### NFR-C-003: Personal Data Protection (RA Data Protection Law)

**Requirement**: Processing of debtor personal data (SSN, tax ID, account information, balance range) must comply with the RA Law on Personal Data Protection. Data minimisation must be applied: only the minimum data necessary for enforcement is transmitted.

**Data Minimisation Controls**:
- Discovery returns account existence, type, and balance range only — not precise balances
- Debtor SSN is transmitted only over encrypted, authenticated X-Road channels
- Debtor personal data is not retained beyond case closure plus the applicable statutory period

**DPIA Required**: Yes — large-scale processing of personal financial data under legal compulsion.

**Priority**: CRITICAL

---

#### NFR-C-004: X-Road Governance Compliance

**Requirement**: CESA and all participating banks must comply with the X-Road membership agreement and security policy as defined by the Armenian e-Government Infrastructure operator. This includes certificate lifecycle management, Security Server version requirements, and audit log retention obligations.

**Priority**: HIGH

---

## Integration Requirements

### INT-001: X-Road Interoperability Platform

**Purpose**: X-Road serves as the message transport, security, and audit layer for all enforcement communications between CESA and commercial banks. [CBBP-C2]

**Integration Type**: Real-time synchronous API over X-Road 6 protocol

**Data Exchanged**:
- CESA → Bank: Enforcement orders (block, collect, release), account discovery queries
- Bank → CESA: Account lists (discovery responses), enforcement confirmations, error responses

**Authentication**: X-Road mTLS — X.509 certificates issued by the X-Road CA

**Message Format**: REST/JSON or SOAP/XML — to be agreed with the X-Road governance body

**Error Handling**: Signed structured error responses; retry logic in CESA IS (FR-008); all failures logged

**SLA**: End-to-end < 5 seconds for blocking orders (bank processing time governed by bank SLA agreement)

**Owner**: EKENG (Central Server); CESA owns its own Security Server; each bank owns its Security Server

**Priority**: CRITICAL

---

### INT-002: CESA Case Management System to CESA X-Road Security Server

**Purpose**: CESA IS must submit enforcement payloads to, and receive signed responses from, the CESA X-Road Security Server.

**Integration Type**: Internal service-to-service API (CESA IS client → CESA Security Server)

**Data Exchanged**: Enforcement request payloads; signed confirmation payloads; audit confirmations

**Authentication**: Internal mTLS or API key over isolated internal network segment

**Priority**: CRITICAL

---

### INT-003: Bank Core Banking System Enforcement API

**Purpose**: Each commercial bank must expose four enforcement API endpoints accessible via their X-Road Security Server, as specified by CESA. [CBBP-C2]

**Endpoints Required**:

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/enforcement/accounts` | GET | Account discovery — debtor account query |
| `/enforcement/block` | POST | Account blocking — apply HOLD |
| `/enforcement/collect` | POST | Fund collection — transfer to CESA account |
| `/enforcement/release` | POST | Restriction lifting — remove HOLD |

**Standard**: OpenAPI 3.0 specification published by CESA; adopted by all banks as a participation condition

**Authentication**: X-Road Security Server (bank side) validates CESA request via X-Road certificate

**Bank SLA**: Bank CBS must process and respond to enforcement API calls within 3 seconds

**Priority**: CRITICAL

---

### INT-004: Central Bank of Armenia (CBA) Coordination

**Purpose**: CBA coordinates bank participation in the X-Road enforcement channel through its regulatory role, and may require aggregate enforcement reporting for systemic risk monitoring. [CBBP-C3]

**Integration Type**: Regulatory reporting (batch) — not real-time enforcement

**Data Exchanged**: Aggregate enforcement statistics; bank onboarding status notifications

**Note**: Detailed CBA integration design is subject to regulatory agreement. This requirement captures the dependency and ensures the architecture accommodates it.

**Priority**: SHOULD_HAVE

---

### INT-005: CESA Collection Account (Fund Transfer Destination)

**Purpose**: Bank fund collection orders must transfer funds to a designated CESA-controlled collection account, identified by IBAN.

**Integration Type**: Bank-to-bank transfer (bank internal — triggered by bank CBS on receipt of collection order)

**Data Exchanged**: Transfer amount (AMD), CESA collection IBAN, enforcement case reference

**Requirement**: CESA must provide a valid Armenian IBAN for the collection account in all collection orders. The IBAN must be pre-registered with each bank as a known CESA account before go-live.

**Priority**: CRITICAL

---

## Data Requirements

### DR-001: Enforcement Case Record

**Description**: Central data entity tracking a debtor enforcement case from initiation to closure.

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| case_id | UUID | Yes | Unique case identifier | PK |
| debtor_ssn | String(20) | Cond. | Debtor national ID / SSN | Encrypted; mutually exclusive with debtor_tax_id |
| debtor_tax_id | String(20) | Cond. | Business tax ID | Encrypted; mutually exclusive with debtor_ssn |
| legal_basis_ref | String(100) | Yes | Court order / decision reference | Not null |
| status | Enum | Yes | Case lifecycle status | [OPEN, ACTIVE, CLOSED, SUSPENDED] |
| created_at | Timestamp | Yes | Case creation time | UTC, millisecond precision, indexed |
| created_by | UUID | Yes | CESA officer ID | FK to officer table |
| closed_at | Timestamp | No | Case closure time | UTC |

**Data Classification**: CONFIDENTIAL (personal data + legal records)

**Data Retention**: 10 years from case closure, or the statutory period defined by RA enforcement law — whichever is longer

---

### DR-002: Enforcement Order Record

**Description**: Each enforcement action (block, collect, release, query) issued against one or more accounts at one bank.

**Attributes**:

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| order_id | UUID | Yes | Unique order identifier |
| case_id | UUID | Yes | FK to enforcement case |
| action_type | Enum | Yes | [BLOCK, COLLECT, RELEASE, QUERY] |
| bank_xroad_id | String | Yes | Target bank X-Road member identifier |
| accounts | JSON Array | Yes | Target account identifiers |
| amount_amd | Decimal | Cond. | Collection amount — collection orders only |
| cesa_collection_iban | String | Cond. | Destination IBAN — collection orders only |
| legal_basis_ref | String | Yes | Court / administrative decision reference |
| status | Enum | Yes | [PENDING, SENT, CONFIRMED, PARTIAL, FAILED, MANUAL_FOLLOWUP] |
| transmitted_at | Timestamp | No | X-Road transmission timestamp |
| confirmed_at | Timestamp | No | Bank confirmation timestamp |
| bank_ref | String | No | Bank's confirmation reference number |
| error_detail | String | No | Error message if status is FAILED |

**Data Classification**: CONFIDENTIAL

**Data Retention**: Per case retention (DR-001)

---

### DR-003: X-Road Audit Log Entry

**Description**: Immutable record of each X-Road message exchange (both sent and received).

**Attributes**:

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| log_id | UUID | Yes | Unique log entry ID |
| order_id | UUID | Yes | FK to enforcement order |
| direction | Enum | Yes | [SENT, RECEIVED] |
| xroad_message_id | String | Yes | X-Road protocol message ID |
| payload_hash | String(64) | Yes | SHA-256 of message payload |
| signature | String | Yes | X-Road digital signature (base64) |
| timestamp_utc | Timestamp | Yes | UTC, millisecond precision |
| result_code | String(10) | Yes | HTTP / X-Road response status code |
| chain_hash | String(64) | Yes | Hash of previous log entry (tamper-evidence) |

**Data Classification**: RESTRICTED (legal evidence)

**Data Retention**: 10 years (immutable, tamper-evident storage mandatory)

---

### DR-004: Debtor Account Discovery Record

**Description**: Account information returned by banks during discovery queries. Stored for the duration of the case.

**Attributes**:

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| discovery_id | UUID | Yes | FK to enforcement order (QUERY type) |
| bank_xroad_id | String | Yes | Reporting bank X-Road identifier |
| account_id | String | Yes | Bank-assigned account identifier |
| account_type | Enum | Yes | [CURRENT, SAVINGS, DEPOSIT, BUSINESS, OTHER] |
| currency | String(3) | Yes | ISO 4217 currency code |
| balance_range | Enum | Yes | [ZERO, LOW, MEDIUM, HIGH] — not exact balance |
| account_status | Enum | Yes | [ACTIVE, BLOCKED, FROZEN, CLOSED] |
| returned_at | Timestamp | Yes | Timestamp of bank response |

**Data Classification**: CONFIDENTIAL (financial data)

**Data Retention**: Duration of case + 10 years

---

### DR-005: Personal Data Processing Register

| Data Element | Purpose | Legal Basis | Data Minimisation Applied | Retention |
|--------------|---------|-------------|--------------------------|-----------|
| Debtor SSN / National ID | Identify debtor accounts across banks | Legal obligation (enforcement law) | Transmitted only to X-Road registered banks; encrypted in transit and at rest | Case + 10 years |
| Debtor Tax ID | Identify business accounts | Legal obligation | Transmitted only when needed | Case + 10 years |
| Account IDs | Target enforcement actions | Legal obligation | Not exposed in discovery response (bank-internal reference only) | Case + 10 years |
| Balance range | Prioritise enforcement decisions | Legal obligation | Range returned — not precise balance (data minimisation) | Case + 10 years |
| Collection amount | Execute fund collection | Legal obligation | Minimum needed for specific collection order | Order record + 10 years |

**DPIA Recommended**: Yes — large-scale processing of personal financial data under legal compulsion. Engage Data Protection Authority before go-live.

---

### DR-006: Data Retention Schedule

| Data Type | Retention Period | Legal Basis | Storage Tier |
|-----------|-----------------|-------------|-------------|
| Enforcement case records | 10 years from case closure | RA Enforcement Law | Active → Archive |
| X-Road audit logs (CESA side) | 10 years from transaction date | Legal evidence requirement | Immutable archive |
| X-Road audit logs (bank side) | Per bank's legal obligations | X-Road membership agreement | Bank-managed |
| Officer authentication logs | 5 years | Security audit requirement | Secure archive |
| Discovery records | Duration of case + 10 years | Legal relevance | Case archive |
| Failed transmission logs | 2 years | Operational continuity | Archive |

---

## Constraints and Assumptions

### Technical Constraints

**TC-001**: The interoperability backbone must be X-Road 6. Alternative messaging or API gateway platforms are out of scope for this project.

**TC-002**: Bank CBS API adapters are the responsibility of each commercial bank. CESA provides the API specification (FR-009); banks implement and self-certify their adapters against CESA's test suite.

**TC-003**: The X-Road Central Server, CA, and OCSP service are operated by EKENG (or successor body). CESA and banks are X-Road members; they do not operate the central infrastructure.

**TC-004**: All enforcement messages must be transmitted via X-Road. Direct bank API calls bypassing the X-Road Security Server are not permitted under this architecture.

---

### Business Constraints

**BC-001**: CESA cannot compel banks to onboard before they have completed their own IT readiness. Phased onboarding (BR-005) is mandatory; the system must support parallel X-Road and manual operation.

**BC-002**: Legal basis reference is mandatory for all enforcement actions. The system must not transmit enforcement orders without a validated legal reference (FR-010). This is a legal requirement, not a system policy.

**BC-003**: Fund collection orders transfer funds to a CESA-controlled collection account. Banks are not responsible for fund disbursement to creditors — that is CESA's internal process, out of scope for this project.

---

### Assumptions

**A-001**: X-Road is the designated interoperability platform for this integration, as evidenced by the to-be business process design [CBBP-C2].

**A-002**: EKENG (or successor) will register CESA and all licensed commercial banks as X-Road members as part of the programme.

**A-003**: Each commercial bank will deploy an X-Road Security Server as a condition of participation in the enforcement integration.

**A-004**: Banks will adopt the CESA-published enforcement API specification as a condition of their participation agreement (to be enforced via CBA regulatory direction or contractual agreement).

**A-005**: The Central Bank of Armenia will coordinate or mandate bank participation through its regulatory authority over licensed banks.

**A-006**: Network round-trip time between CESA and any bank X-Road Security Server is less than 500ms under normal operating conditions.

**A-007**: CESA will maintain a single collection IBAN per currency (AMD minimum) for fund transfer destinations, registered with all banks prior to go-live.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|--------------------|
| Enforcement execution time (block) | Hours to days (manual) | < 5 seconds | Go-live | System audit log timestamps |
| Banks connected (X-Road enforcement) | 0 | All licensed banks | 12 months post go-live | Bank registry count |
| CESA officer time per enforcement order | TBD (manual study) | > 80% reduction | 6 months post go-live | Before/after time study |
| Failed enforcement rate (technical) | N/A | < 0.5% | Ongoing post go-live | X-Road transmission log analysis |
| Audit trail completeness | N/A | 100% coverage | Ongoing | Audit log completeness verification |

### Technical Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Blocking order latency (p95) | < 5 seconds | APM telemetry |
| System availability | 99.9% | Uptime monitoring |
| X-Road message success rate | > 99.5% | X-Road audit log analysis |
| Discovery query latency (p95) | < 30 seconds | System telemetry |
| Audit log integrity | 100% (zero tampered records) | Hash chain verification |

---

## Dependencies and Risks

### Dependencies

| Dependency | Description | Owner | Impact if Delayed |
|------------|-------------|-------|-------------------|
| X-Road membership registration | CESA registered as X-Road member | EKENG | Blocks all integration testing |
| Bank X-Road Security Server deployment | Each bank deploys and configures their Security Server | Individual banks | Delays bank-specific go-live |
| CESA IS enforcement module development | API client and case management enhancements | CESA IT | Blocks integration testing |
| Bank CBS API adapter development | Each bank builds enforcement API adapter | Individual banks | Delays bank go-live |
| CBA regulatory direction | CBA directive for banks to participate | Central Bank of Armenia | Slows voluntary bank onboarding |
| Legal reference format standardisation | Court order reference format agreed | Ministry of Justice / CESA | Blocks FR-010 implementation |
| CESA collection IBAN pre-registration | IBAN pre-registered with all banks | CESA Finance / Banks | Blocks fund collection go-live |

### Risks

| Risk ID | Description | Probability | Impact | Mitigation |
|---------|-------------|-------------|--------|------------|
| R-001 | Banks reluctant to implement CBS API adapters without regulatory mandate | HIGH | HIGH | Engage CBA for regulatory directive; pilot with willing bank to demonstrate; phased approach allows progress |
| R-002 | X-Road message latency exceeds NFR-P-001 targets | MEDIUM | HIGH | Early performance testing with realistic payloads; enforce bank-side SLA in participation agreement |
| R-003 | Legal reference format not standardised — enforcement orders rejected | MEDIUM | HIGH | Agree format with Ministry of Justice in project initiation; validate against real court order samples |
| R-004 | Debtor SSN transmitted insecurely — personal data breach | LOW | CRITICAL | mTLS + payload encryption mandatory; independent security audit before go-live; no bypass permitted |
| R-005 | Bank CBS returns incorrect account data — wrong accounts blocked | LOW | CRITICAL | Mandatory bank certification testing before go-live; dispute resolution process defined; appeal mechanism in place |
| R-006 | X-Road Central Server outage causes enforcement channel unavailability | LOW | HIGH | Manual fallback maintained for all banks; DR plan covers X-Road dependency; SLA with EKENG |

---

## Requirement Conflicts & Resolutions

### Conflict C-001: Real-Time Availability vs. Phased Bank Onboarding

**Conflicting Requirements**:
- **NFR-A-001**: Enforcement must be available 24/7 with 99.9% uptime (implying all banks reachable)
- **BR-005**: Banks onboard in phases; not all banks will be X-Road ready at go-live

**Nature of Conflict**: Full real-time enforcement at 99.9% uptime is only achievable for banks that have completed X-Road onboarding. Non-onboarded banks cannot receive real-time orders — creating an inevitable gap.

**Resolution Strategy**: PHASE

**Decision**: NFR-A-001 applies to the X-Road channel and CESA IS itself — not to individual bank connectivity. Banks not yet onboarded are handled via manual fallback (BR-005). The SLA covers the system infrastructure, not the endpoint availability of individual banks.

**Impact on Requirements**: NFR-A-001 clarified to scope availability to the CESA IS and CESA Security Server; per-bank availability governed by individual bank SLA agreements.

---

### Conflict C-002: Data Minimisation vs. Enforcement Effectiveness

**Conflicting Requirements**:
- **NFR-C-003**: Personal data minimisation — transmit only what is strictly necessary
- **FR-001**: Account discovery must return enough information for officers to prioritise enforcement action

**Nature of Conflict**: Precise account balances are useful for prioritising collection (highest balance first) but transmitting exact balances during a discovery query exceeds minimum necessity under data minimisation.

**Resolution Strategy**: COMPROMISE

**Decision**: Discovery returns balance range (ZERO / LOW / MEDIUM / HIGH) rather than precise balances. This is sufficient for prioritisation without violating data minimisation. If precise balance is legally required for a specific enforcement type, a separate authorised balance query may be defined in a future phase.

---

## Timeline and Milestones

| Milestone | Description | Target Date |
|-----------|-------------|-------------|
| Requirements Approval | CESA sign-off on this document | TBD |
| X-Road Registration | CESA registered as X-Road member | TBD |
| API Specification Published | Enforcement API spec finalised and published for banks | TBD |
| Pilot Bank Integration | First bank completes X-Road integration and certification testing | TBD |
| CESA IS Development Complete | Enforcement module development and unit testing complete | TBD |
| Integration Testing Complete | End-to-end testing with pilot bank(s) on X-Road | TBD |
| Security Audit Complete | Independent security review of X-Road enforcement channel | TBD |
| Phased Go-Live | Initial certified banks live on real-time enforcement | TBD |
| Full Rollout | All licensed banks onboarded | 12 months post go-live |

---

## Approval

### Requirements Review

| Reviewer | Role | Status | Date | Comments |
|----------|------|--------|------|----------|
| PENDING | CESA Programme Manager | [ ] Approved | | |
| PENDING | CESA IT Lead | [ ] Approved | | |
| PENDING | Ministry of Justice Representative | [ ] Approved | | |
| PENDING | Central Bank of Armenia Representative | [ ] Approved | | |
| PENDING | Data Protection Authority Representative | [ ] Approved | | |

---

## Appendices

### Appendix A: Glossary

| Term | Definition |
|------|-----------|
| CESA | Armenian State Enforcement Service (Compulsory Enforcement Service of Armenia) — the national bailiff/enforcement authority |
| CBS | Core Banking System — the primary banking management platform at each commercial bank |
| X-Road | Open-source data exchange platform for secure inter-organisational communication; serves as Armenia's national interoperability platform |
| X-Road Security Server | The gateway component deployed by each X-Road member to send and receive digitally signed messages |
| HOLD | A status applied to a bank account preventing withdrawals, transfers, or new debits |
| Enforcement Order | A legally authorised instruction issued by CESA directing a bank to apply or lift an enforcement action |
| mTLS | Mutual TLS — both communicating parties authenticate each other using X.509 digital certificates |
| SSN | Social Security Number — Armenian national identity number used as a primary debtor identifier |
| AMD | Armenian Dram — the national currency of Armenia (ISO 4217: AMD) |
| EKENG | Enterprise Information Technologies Nonprofit Organisation — operator of the Armenian national e-Government infrastructure including X-Road |
| CBA | Central Bank of Armenia — the financial regulatory authority that licenses commercial banks |
| IBAN | International Bank Account Number — standardised format for bank account identification |
| Non-repudiation | A cryptographic property ensuring that a party cannot deny having sent or received a specific message |
| Data Minimisation | The principle of processing only the minimum personal data necessary for a specified purpose |

### Appendix B: Referenced Standards and Law

- X-Road Protocol 6 specification (x-road.global)
- OpenAPI 3.0 (API specification standard)
- ISO 4217 (Currency codes)
- X.509 v3 (Certificate standard)
- RFC 8446 (TLS 1.3)
- RA Law on Enforcement Proceedings (Հայաuտanи Հanrapetутyan Kanon)
- RA Law on Personal Data Protection
- EKENG X-Road membership agreement and security policy

---

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| CBBP | CESA-BANKS-BP.pdf | Business Process | `001-cesa-banks/external/` | Existing (AS-IS) and to-be business process swimlane diagrams for enforcement actions across RA commercial banks. Three pages covering manual current state and X-Road-based automated to-be flows for account blocking, fund collection, and restriction lifting. |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| CBBP-C1 | CBBP | Page 1 — AS-IS swimlane (left column) | Business Requirement | AS-IS process shows manual document preparation, review steps, and sequential dispatch to banks with no automated channel — source of hours-to-days enforcement delay |
| CBBP-C2 | CBBP | Page 1 — TO-BE swimlane (centre: globe icon) | Functional Requirement | TO-BE state shows enforcement actions (block, collect, release) transmitted via X-Road (globe icon represents the interoperability platform) with real-time confirmation flows in both directions |
| CBBP-C3 | CBBP | Page 2 — account discovery flow | Business Requirement | Separate discovery/enquiry process showing CESA querying banks and CBO via X-Road to identify debtor accounts and property before enforcement action is initiated |
| CBBP-C4 | CBBP | Pages 1–3 — all flows | Compliance Constraint | All process flows include explicit legal decision/order reference validation steps before any enforcement action is transmitted, indicating mandatory legal basis traceability throughout |
| CBBP-C5 | CBBP | Page 3 — departmental variant | Business Requirement | Departmental routing variant shows enforcement actions originating from different CESA departments/branches — confirming the need for a unified platform supporting multiple originating organisational units |

---

**Generated by**: ArcKit `/arckit:requirements` command
**Generated on**: 2026-04-22 GMT
**ArcKit Version**: 4.9.1
**Project**: CESA–Banks Enforcement Integration (Project 001)
**AI Model**: claude-sonnet-4-6
**Generation Context**: Requirements derived from CESA-BANKS-BP.pdf (3-page Armenian-language business process swimlane document) and the sequence diagram ARC-001-DIAG-001-v1.0.md. No stakeholder analysis, architecture principles, or risk register were available at time of generation — those documents are recommended next steps.
