# Stakeholder Drivers & Goals Analysis: CESA–Commercial Banks Enforcement Integration

> **Template Origin**: Official | **ArcKit Version**: 4.9.1 | **Command**: `/arckit.stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers & Goals Analysis |
| **Project** | CESA-Banks Enforcement Integration (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-22 |
| **Last Modified** | 2026-04-22 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-07-22 |
| **Owner** | Programme Lead, CESA IT Department |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project Team, Architecture Team, CESA Programme Office, Commercial Bank Representatives, Ministry of Justice |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-22 | ArcKit AI | Initial creation from `/arckit:stakeholders` command — derived from ARC-001-REQ-v1.0 and CESA-BANKS-BP.pdf | PENDING | PENDING |

---

## Executive Summary

### Purpose

This document identifies all key stakeholders in the CESA–Commercial Banks Enforcement Integration programme, their underlying drivers (motivations, pressures, and concerns), how those drivers manifest into measurable goals, and the business outcomes that will demonstrate success. It provides the traceability foundation for requirements prioritisation, design decisions, communication planning, and governance.

### Key Findings

The dominant alignment across all stakeholders is the replacement of a manual, delay-prone enforcement process with a real-time X-Road integration — every primary internal stakeholder shares this goal [CBBP-C1]. The most significant tensions are: (1) CESA Leadership's desire for rapid deployment versus Commercial Banks' need for implementation lead time on Core Banking System adapters, and (2) the RA Data Protection Authority's data minimisation obligations versus enforcement officers' desire for precise account data to prioritise collection actions (a conflict resolved in the Requirements document via the balance-range compromise). [CBBP-C3]

### Critical Success Factors

- **CBA regulatory mandate or directive** — voluntary bank participation alone is unlikely to achieve full ecosystem onboarding within 12 months; CBA regulatory direction is the critical accelerant
- **Standardised legal reference format** — agreed between CESA and the Ministry of Justice before development begins; without this, FR-010 validation cannot be implemented
- **DPIA signed off by the RA Data Protection Authority** before go-live — large-scale processing of personal financial data under legal compulsion requires formal DPA engagement [CBBP-C4]
- **Pilot bank commitment** — at least one willing early-adopter bank completing X-Road Security Server deployment and CBS adapter development before the system goes live, validating the integration end-to-end

### Stakeholder Alignment Score

**Overall Alignment**: MEDIUM-HIGH

Internal CESA stakeholders are strongly aligned on the strategic direction. The primary friction points are external: commercial banks face real implementation costs and timeline pressures, and regulatory bodies (DPA) must be satisfied before go-live. The phased onboarding approach (BR-005) is the correct mechanism to manage this tension — it allows CESA to go live with willing banks while others complete readiness.

---

## Stakeholder Identification

### Internal Stakeholders

| Stakeholder | Role / Department | Power | Interest | Engagement Strategy |
|-------------|------------------|-------|----------|---------------------|
| CESA Leadership | Executive Sponsor | HIGH | HIGH | Steering committee; fortnightly status; escalation point for strategic decisions |
| CESA Programme Manager | Programme Lead | HIGH | HIGH | Day-to-day programme governance; requirements ownership; weekly |
| CESA Enforcement Officers (Bailiffs) | Primary End Users | LOW | HIGH | User research, UAT, early prototyping; sprint demos |
| CESA Supervisors / Departmental Heads | Middle Management | MEDIUM | HIGH | Dashboard access; change management briefings; monthly |
| CESA IT Department | Technical Owner and Builder | MEDIUM | HIGH | Architecture decisions; sprint ceremonies; daily collaboration |
| CESA System Administrators | Operations | MEDIUM | HIGH | Bank registry management; runbooks; release planning |

### External Stakeholders

| Stakeholder | Organisation | Relationship | Power | Interest |
|-------------|--------------|--------------|-------|----------|
| Central Bank of Armenia (CBA) | Financial Regulator | Coordinator / Potential Mandator | HIGH | HIGH |
| Ministry of Justice | Legal Authority | Legal framework owner | HIGH | HIGH |
| RA Data Protection Authority | Regulatory Body | Oversight; DPIA sign-off | HIGH | MEDIUM |
| EKENG (or successor) | e-Gov Infrastructure Operator | X-Road platform operator | MEDIUM | MEDIUM |
| Commercial Bank Leadership | Commercial Banks (all 15+) | Integration partners (institutional) | HIGH | MEDIUM |
| Commercial Bank IT Leads | Commercial Banks | Technical implementation partners | MEDIUM | HIGH |
| Bank Compliance Officers | Commercial Banks | Process owners for enforcement receipt | LOW | HIGH |
| Creditors / Claimants | External — enforcement beneficiaries | Indirect beneficiary | LOW | LOW |
| Debtors | General public / businesses | Affected parties | LOW | LOW |

### Stakeholder Power-Interest Grid

```text
                         INTEREST
             Low                          High
       ┌──────────────────────┬──────────────────────┐
       │                      │                      │
       │   KEEP SATISFIED     │   MANAGE CLOSELY     │
  High │                      │                      │
       │  • RA Data Protection│  • CESA Leadership   │
       │    Authority         │  • CESA Programme Mgr│
       │  • Commercial Bank   │  • Ministry of Justice│
       │    Leadership        │  • Central Bank (CBA) │
 P     │  • EKENG             │                      │
 O     ├──────────────────────┼──────────────────────┤
 W     │                      │                      │
 E     │       MONITOR        │   KEEP INFORMED      │
 R     │                      │                      │
  Low  │  • Creditors         │  • CESA Officers     │
       │  • Debtors           │  • CESA IT Dept      │
       │                      │  • Bank IT Leads     │
       │                      │  • Bank Compliance   │
       │                      │  • CESA Supervisors  │
       └──────────────────────┴──────────────────────┘
```

| Stakeholder | Power | Interest | Quadrant | Engagement Strategy |
|-------------|-------|----------|----------|---------------------|
| CESA Leadership | HIGH | HIGH | Manage Closely | Fortnightly steering; all strategic decisions |
| CESA Programme Manager | HIGH | HIGH | Manage Closely | Daily programme governance |
| Ministry of Justice | HIGH | HIGH | Manage Closely | Legal reference format agreement; go-live sign-off |
| Central Bank of Armenia | HIGH | HIGH | Manage Closely | Bank onboarding directive; aggregate reporting alignment |
| RA Data Protection Authority | HIGH | MEDIUM | Keep Satisfied | DPIA submission; pre-go-live consultation |
| Commercial Bank Leadership | HIGH | MEDIUM | Keep Satisfied | CBA alignment; participation agreement |
| EKENG | MEDIUM | MEDIUM | Keep Satisfied | X-Road membership registration; platform SLA |
| CESA Enforcement Officers | LOW | HIGH | Keep Informed | UAT; sprint demos; training |
| CESA IT Department | MEDIUM | HIGH | Keep Informed | Architecture reviews; sprint ceremonies |
| Commercial Bank IT Leads | MEDIUM | HIGH | Keep Informed | API specification; certification testing |
| Bank Compliance Officers | LOW | HIGH | Keep Informed | Process documentation; training materials |
| CESA Supervisors | MEDIUM | HIGH | Keep Informed | Dashboard access; monthly briefings |
| Creditors / Claimants | LOW | LOW | Monitor | Annual update; satisfaction survey |
| Debtors | LOW | LOW | Monitor | Privacy notice; rights information |

**Quadrant Interpretation:**

- **Manage Closely** (High Power, High Interest): Key decision-makers requiring active, frequent engagement
- **Keep Satisfied** (High Power, Low-Medium Interest): High-influence stakeholders who can block progress — needs periodic but substantive engagement
- **Keep Informed** (Low-Medium Power, High Interest): Engaged stakeholders who are directly affected by delivery — keep them updated and heard
- **Monitor** (Low Power, Low Interest): Minimal engagement; ensure legal obligations met

---

## Stakeholder Drivers Analysis

### SD-1: CESA Leadership — Eliminate Asset Dissipation Risk

**Stakeholder**: CESA Leadership (Executive Sponsor)

**Driver Category**: STRATEGIC + COMPLIANCE

**Driver Statement**: The current manual enforcement process introduces delays of hours to days between the issuance of a legal enforcement order and its execution at commercial banks. This window creates material risk that debtors can dissipate assets before accounts are frozen — directly undermining the legal and practical effectiveness of enforcement proceedings. [CBBP-C1]

**Context & Background**: Under the current AS-IS process, enforcement documents are manually prepared, reviewed, and dispatched to individual commercial banks. Banks then manually apply account holds. This is not a process optimisation problem — it is a structural gap in the legal enforcement system that exposes CESA to reputational and legal risk when assets cannot be recovered because enforcement came too late.

**Driver Intensity**: CRITICAL

**Enablers**:
- X-Road provides a ready-made, legally recognised interoperability platform for exactly this use case [CBBP-C2]
- Armenia's digital government modernisation agenda creates political and institutional support for this type of integration

**Blockers**:
- Banks have autonomy over their CBS implementation timelines; without CBA regulatory direction, onboarding is voluntary and slow
- The CESA IS enforcement module requires significant development before real-time transmission is possible

**Related Stakeholders**: Ministry of Justice (legal effectiveness), CESA Programme Manager (delivery accountability), Commercial Bank Leadership (participation)

---

### SD-2: CESA Enforcement Officers — Eliminate Manual Drudgery and Uncertainty

**Stakeholder**: CESA Enforcement Officers (Bailiffs) and CESA Supervisors

**Driver Category**: OPERATIONAL + PERSONAL

**Driver Statement**: Officers currently spend significant time on manual document preparation and sequential bank coordination, with no unified status view and no automated discovery of which banks hold debtor accounts. This creates both operational inefficiency and professional frustration — officers cannot manage their caseload effectively when they are doing administrative work that technology should handle. [CBBP-C1]

**Context & Background**: Per the AS-IS business process, officers must know in advance which banks hold debtor accounts and must dispatch documents individually. [CBBP-C3] There is no feedback loop on enforcement status short of following up manually with each bank. Officers working on high-volume caseloads are particularly affected. Supervisors cannot get real-time throughput visibility.

**Driver Intensity**: HIGH

**Enablers**:
- Automated account discovery (FR-001) eliminates the need for officers to know which banks to contact
- Real-time status dashboard (FR-007) gives supervisors immediate visibility
- A unified interface for all 4 enforcement action types (BR-004) reduces training burden

**Blockers**:
- Officers may resist if the new system is harder to use than the old one (even if more powerful)
- System downtime or bank-side failures must be handled gracefully to avoid officers preferring the old manual fallback

**Related Stakeholders**: CESA IT Department (system usability), CESA System Administrators (reliability)

---

### SD-3: CESA Programme Manager — Successful, Controlled Programme Delivery

**Stakeholder**: CESA Programme Manager

**Driver Category**: RISK + PERSONAL

**Driver Statement**: The Programme Manager is personally accountable for requirements quality, stakeholder alignment, and delivery outcomes. A high-profile failure in this programme — particularly one involving asset dissipation because the system was poorly designed or went live prematurely — would have serious professional and institutional consequences.

**Context & Background**: This is a legally and reputationally sensitive programme. The enforcement system directly supports judicial and administrative orders. Failures are not invisible — they result in debtors escaping enforcement, which is visible to the courts, creditors, and Ministry of Justice.

**Driver Intensity**: HIGH

**Enablers**:
- Phased onboarding (BR-005) limits early scope and allows learning before scaling
- Clear certification process for bank X-Road integration reduces surprise failures at go-live
- Independent security audit before go-live (planned milestone) provides professional cover

**Blockers**:
- Legal reference format not standardised in time (Risk R-003 from REQ)
- Bank CBS adapter quality below standard at certification testing
- DPA DPIA review taking longer than expected, delaying go-live

**Related Stakeholders**: CESA Leadership (accountability), Ministry of Justice (legal format), DPA (DPIA timeline)

---

### SD-4: CESA IT Department — Standards-Based, Maintainable Architecture

**Stakeholder**: CESA IT Department (Technical Owner and Builder)

**Driver Category**: STRATEGIC + OPERATIONAL

**Driver Statement**: The CESA IT team needs to build a system they can maintain, extend, and operate with confidence. A poorly architected solution that requires bespoke workarounds for each bank would be technically unsustainable. Adoption of X-Road — the national interoperability standard — eliminates per-bank custom code and creates a single, standards-based channel. [CBBP-C2]

**Context & Background**: CESA IT is responsible for owning the system post-delivery. They have a strong interest in ensuring the architecture is clean (one API spec, one integration pattern for all banks), that the bank registry is configuration-driven (FR-006), and that the system is observable and operable.

**Driver Intensity**: MEDIUM

**Enablers**:
- X-Road abstracts mTLS, message signing, and audit logging — CESA IS can focus on business logic
- Configuration-driven bank registry means adding new banks requires no code change (FR-006)
- OpenAPI 3.0 specification published to banks creates a clear contract

**Blockers**:
- X-Road Security Server operational complexity (certificate lifecycle, OCSP, version management)
- CESA IS development capacity and technical capability with X-Road integration patterns

**Related Stakeholders**: EKENG (X-Road platform), Commercial Bank IT Leads (API compliance)

---

### SD-5: Commercial Bank IT Leads — Implement with Minimal CBS Risk and Clear Specification

**Stakeholder**: Commercial Bank IT Leads

**Driver Category**: OPERATIONAL + RISK

**Driver Statement**: Bank IT leads must implement 4 new enforcement API endpoints against their Core Banking System without disrupting live banking operations. Their primary concerns are: (a) getting a clear, stable, fully-specified API contract from CESA so they do not have to re-implement; (b) having sufficient lead time; and (c) limiting their exposure to enforcement-related liability. [CBBP-C2]

**Context & Background**: Each bank must deploy its own X-Road Security Server and build a CBS adapter for the 4 enforcement endpoints. This is non-trivial work involving legal, compliance, IT, and operations teams at each bank. Banks that onboard early take on more risk; those that wait can learn from early adopters. Without a clear API specification published early (FR-009), banks cannot plan or estimate.

**Driver Intensity**: HIGH

**Enablers**:
- CESA publishing a complete OpenAPI 3.0 specification early (FR-009)
- A shared certification test suite that gives banks confidence before going live
- X-Road Security Server tooling that abstracts mTLS and signing from the CBS adapter

**Blockers**:
- Unclear or changing API specification during bank development
- Insufficient lead time (banks typically need 6-12 months for CBS changes)
- No clear CBA mandate, reducing internal priority allocation for bank IT teams

**Related Stakeholders**: CESA IT (specification quality), CBA (prioritisation mandate), EKENG (Security Server support)

---

### SD-6: Commercial Bank Leadership — Regulatory Compliance and Relationship Management

**Stakeholder**: Commercial Bank Leadership (institutional)

**Driver Category**: COMPLIANCE + RISK

**Driver Statement**: Commercial bank leadership is motivated primarily by regulatory compliance and avoiding sanctions from the Central Bank of Armenia. Participation in the CESA enforcement integration is likely to become a regulatory obligation; banks that delay or resist risk adverse CBA attention. A secondary driver is reputational — being seen to support legitimate enforcement of judicial orders. [CBBP-C5]

**Context & Background**: Banks are under CBA oversight and must maintain their operating licences. CBA has the regulatory authority to mandate participation in national interoperability initiatives. The business process document indicates that all CBA-licensed banks are expected to participate. [CBBP-C5]

**Driver Intensity**: MEDIUM (escalates to HIGH if CBA issues a directive)

**Enablers**:
- CBA formal directive or regulatory guidance mandating participation
- Clear participation agreement that defines bank obligations and CESA obligations symmetrically
- Liability protection — banks acting on duly signed, authenticated enforcement orders from CESA are legally protected

**Blockers**:
- Ambiguity about legal liability if bank CBS applies a block erroneously
- Implementation cost not recovered through any fee mechanism
- Unclear dispute resolution process for wrongful blocking

**Related Stakeholders**: CBA (mandate authority), Ministry of Justice (legal protection framework), CESA Programme Manager (participation agreement)

---

### SD-7: Central Bank of Armenia (CBA) — Financial System Stability and Coordinated Onboarding

**Stakeholder**: Central Bank of Armenia

**Driver Category**: COMPLIANCE + STRATEGIC

**Driver Statement**: The CBA has a dual interest: ensuring that the enforcement integration does not create operational or systemic risk for licensed banks (e.g., a badly designed enforcement message causing a CBS outage), while also coordinating bank participation to achieve the national policy objective of digital enforcement modernisation. Aggregate enforcement statistics (INT-004) will support CBA's systemic risk monitoring function.

**Context & Background**: CBA's mandate includes ensuring the safety and soundness of the financial system. A poorly implemented enforcement integration that causes CBS failures at multiple banks simultaneously would be a direct CBA concern. At the same time, CBA has the regulatory levers to accelerate bank onboarding far more effectively than CESA can through voluntary means. [CBBP-C3]

**Driver Intensity**: MEDIUM-HIGH

**Enablers**:
- CESA providing early briefings to CBA on technical architecture and risk controls
- Certification testing programme that CBA can point to as evidence of due diligence
- Aggregate reporting dashboard (INT-004) providing CBA with systemic view

**Blockers**:
- CBA not issuing a participation directive (leaving onboarding voluntary and slow)
- Concerns about bank CBS resilience under enforcement load without stress testing evidence

**Related Stakeholders**: CESA Leadership (programme relationship), Commercial Bank Leadership (supervised entities)

---

### SD-8: Ministry of Justice — Legally Effective and Non-Repudiable Enforcement

**Stakeholder**: Ministry of Justice

**Driver Category**: COMPLIANCE + STRATEGIC

**Driver Statement**: The Ministry of Justice is the legal authority setting the framework for enforcement proceedings in Armenia. Their driver is ensuring that digitally-transmitted enforcement orders are as legally defensible as paper originals — that non-repudiation is guaranteed, that legal basis references are carried in all messages, and that the audit trail can be produced as court evidence. [CBBP-C4]

**Context & Background**: All enforcement actions have significant legal consequences for debtors, creditors, and banks. Any ambiguity about whether an enforcement order was legitimately issued and properly received undermines the legal system. The X-Road message signing and tamper-evident audit log (E-003, DR-003) directly address this. Critically, the Ministry needs agreement on legal reference format (FR-010) before the system can go live.

**Driver Intensity**: HIGH

**Enablers**:
- X-Road digital signatures providing non-repudiation at the protocol level (NFR-SEC-002)
- Legal basis reference mandatory in all enforcement messages (FR-010)
- 10-year tamper-evident audit log accessible within 30 seconds (BR-003)

**Blockers**:
- Court order reference format not yet standardised — creates FR-010 implementation risk
- Questions about jurisdiction if a bank disputes receipt of an enforcement order

**Related Stakeholders**: CESA Leadership (institutional relationship), CESA Programme Manager (legal reference format agreement)

---

### SD-9: RA Data Protection Authority — Personal Data Compliance Under Legal Compulsion

**Stakeholder**: RA Data Protection Authority

**Driver Category**: COMPLIANCE

**Driver Statement**: The system processes debtor personal data (SSN, tax ID, account information, balance ranges) on a large scale, under legal compulsion — debtors have no practical ability to object. The DPA's driver is ensuring that CESA implements adequate safeguards, completes a DPIA, and does not collect more personal data than the minimum necessary for enforcement. [CBBP-C4]

**Context & Background**: This is one of the largest-scale personal financial data processing operations to be built in the Armenian government sector. The combination of breadth (all banks, all debtors in active enforcement), sensitivity (financial data under legal compulsion), and automation (no individual review at point of execution) triggers all DPIA thresholds. The DPA must be engaged before go-live, not after. NFR-C-003 captures the data minimisation requirements; the balance-range compromise in conflict C-002 of the REQ is a direct response to DPA-type concerns.

**Driver Intensity**: HIGH

**Enablers**:
- DPIA initiated early (before development begins, not after)
- Balance-range data minimisation already built into the data model
- Encrypted storage of debtor SSN/tax ID (AES-256 at rest)
- X-Road ensuring debtor SSN transmitted only to ACTIVE X-Road members over mTLS

**Blockers**:
- Late DPA engagement — DPA consultation takes time; starting late risks blocking go-live
- DPA requiring changes to the data model that are expensive to retrofit

**Related Stakeholders**: CESA Programme Manager (DPIA responsibility), CESA IT (technical controls)

---

### SD-10: EKENG — X-Road Platform Adoption and Member Ecosystem Growth

**Stakeholder**: EKENG (X-Road platform operator)

**Driver Category**: STRATEGIC + OPERATIONAL

**Driver Statement**: EKENG's mission is to operate and grow Armenia's national e-Government interoperability infrastructure. Adding CESA and all 15+ commercial banks as X-Road members represents a major expansion of the ecosystem. EKENG's drivers are: ensuring CESA and banks register correctly, maintaining platform SLAs under increased load, and demonstrating the platform's value in high-stakes use cases. [CBBP-C2]

**Context & Background**: The X-Road Central Server, Certificate Authority, and OCSP service are operated by EKENG. CESA and all banks are members; they do not operate central infrastructure. EKENG has a strong interest in successful integrations that demonstrate X-Road's value, but also bears risk if the platform experiences availability issues that disrupt enforcement actions.

**Driver Intensity**: MEDIUM

**Enablers**:
- CESA X-Road Security Server deployment and configuration support from EKENG
- Streamlined member registration process for commercial banks
- Platform capacity planning for enforcement load (50+ concurrent operations)

**Blockers**:
- Slow member registration process creating bank onboarding bottlenecks
- Platform performance under enforcement burst load not tested at scale

**Related Stakeholders**: CESA IT (Security Server deployment), Commercial Bank IT (member registration), CBA (coordination)

---

### SD-11: Bank Compliance Officers — Clear, Authenticated, Structured Enforcement Instructions

**Stakeholder**: Bank Compliance Officers

**Driver Category**: COMPLIANCE + OPERATIONAL

**Driver Statement**: Bank compliance officers currently receive enforcement documents in non-standard formats, review them manually, and must decide whether to apply the instruction. Their driver is receiving structured, authenticated enforcement orders that are unambiguous — so that they can apply them without manual review, are legally protected in doing so, and can return a verifiable confirmation to CESA. [CBBP-C1] [CBBP-C4]

**Context & Background**: Under the current manual process, bank compliance officers bear significant responsibility for interpreting and applying enforcement documents. Errors — whether applying a block to the wrong account or missing an order — create legal exposure for the bank. The X-Road-based system, with its signed messages and structured API responses, removes ambiguity and transfers the legal basis validation responsibility to CESA (via FR-010).

**Driver Intensity**: HIGH

**Enablers**:
- Digitally signed enforcement orders (NFR-SEC-002) — bank can verify authenticity without manual review
- Structured API contract (FR-009) with machine-readable status codes
- Clear dispute resolution process for wrongful blocking scenarios

**Blockers**:
- Current lack of structured API specification (FR-009 must be published early)
- No standardised dispute process for contested enforcement actions

**Related Stakeholders**: CESA IT (API spec quality), Ministry of Justice (legal protection for banks following signed orders)

---

## Driver-to-Goal Mapping

### Goal G-1: Deliver Real-Time Enforcement Execution within 5 Seconds

**Derived From Drivers**: SD-1, SD-2, SD-8, SD-11

**Goal Owner**: CESA Leadership (accountability); CESA Programme Manager (delivery)

**Goal Statement**: Deploy the CESA enforcement integration so that all 4 enforcement action types (account blocking, fund collection, restriction lifting, account discovery) are executed via X-Road and confirmed within 5 seconds (blocking, p95) and 15 seconds (collection, p95) for all X-Road ACTIVE banks, within 6 months of the pilot bank going live.

**Why This Matters**: Eliminates the hours-to-days asset dissipation window that undermines the practical effect of enforcement orders (SD-1). Removes manual effort from officers (SD-2). Provides the authenticated, structured channel bank compliance officers need (SD-11).

**Success Metrics**:
- **Primary Metric**: Blocking order end-to-end latency at p95 (target: < 5 seconds)
- **Secondary Metrics**:
  - Collection order confirmation latency at p95 (target: < 15 seconds)
  - Discovery query aggregated response time at p95 (target: < 30 seconds)
  - X-Road message success rate (target: > 99.5%)

**Baseline**: Current enforcement execution time: hours to days (manual dispatch and response)

**Target**: Blocking confirmed < 5 seconds (p95); collection confirmed < 15 seconds (p95); discovery results < 30 seconds (p95)

**Measurement Method**: APM telemetry — timestamp delta logged in E-003 (AuditLogEntry) between transmitted_at and confirmed_at in E-002 (EnforcementOrder)

**Dependencies**:
- Pilot bank CBS adapter developed, tested, and certified
- CESA X-Road Security Server deployed and EKENG-registered
- CESA IS enforcement module development complete
- NFR-A-003 fault detection within 10 seconds implemented

**Risks to Achievement**:
- Bank CBS processing latency exceeds 3-second SLA under load (Risk R-002 in REQ)
- Network round-trip between CESA SS and bank SS exceeds 500ms assumed budget (A-006 in REQ)

---

### Goal G-2: Enable Automated Account Discovery Across All Licensed Banks

**Derived From Drivers**: SD-1, SD-2, SD-7

**Goal Owner**: CESA Programme Manager

**Goal Statement**: Enable CESA officers to query all X-Road ACTIVE banks simultaneously for debtor accounts using SSN or tax ID within 30 seconds (p95), with results including account type, currency, balance range, and status, within 6 months of pilot launch.

**Why This Matters**: Eliminates the need for officers to know which banks hold debtor accounts (SD-2), enables complete enforcement across all bank relationships (SD-1), and provides CBA with systemic visibility once all banks are onboarded (SD-7).

**Success Metrics**:
- **Primary Metric**: Discovery query response time across all registered banks at p95 (target: < 30 seconds)
- **Secondary Metrics**:
  - % of X-Road ACTIVE banks responding to each query (target: 100% of ACTIVE banks)
  - Zero precise balances transmitted — balance_range enum only (data minimisation compliance)

**Baseline**: Officers must manually identify which banks to contact; no simultaneous broadcast capability

**Target**: Simultaneous broadcast to all 15+ ACTIVE banks, aggregated results within 30 seconds

**Measurement Method**: System telemetry on discovery query broadcasts; E-004 (DiscoveryRecord) completeness vs D5 (Bank Registry) ACTIVE count

**Dependencies**:
- Bank registry (D5) maintained with accurate ACTIVE/ONBOARDING/MANUAL_ONLY status
- All banks implementing the `/enforcement/accounts` GET endpoint (INT-003)

**Risks to Achievement**:
- Slow bank onboarding means discovery only covers a subset of banks initially
- Bank returns non-standard response format — rejected by CESA IS

---

### Goal G-3: Achieve Legally Defensible, Tamper-Evident Audit Trail

**Derived From Drivers**: SD-8, SD-3, SD-6, SD-11

**Goal Owner**: CESA Programme Manager (DPIA); CESA IT (technical implementation)

**Goal Statement**: Achieve 100% audit trail coverage for all enforcement actions — every X-Road message signed, logged with SHA-256 hash and chain_hash, and retrievable within 30 seconds — before the pilot bank goes live.

**Why This Matters**: Provides the non-repudiation required by the Ministry of Justice (SD-8) and the legal protection banks need when applying signed enforcement orders (SD-11). Protects the Programme Manager from challenge if an enforcement action is disputed (SD-3).

**Success Metrics**:
- **Primary Metric**: Audit trail completeness (target: 100% of enforcement orders have associated log entries)
- **Secondary Metrics**:
  - Hash chain integrity (target: 100% — no broken links on monthly verification run)
  - Audit log retrieval time for any enforcement action (target: < 30 seconds)
  - Log entries in WORM (immutable) storage from day one

**Baseline**: No digital audit trail; manual paper records with no cryptographic verifiability

**Target**: Every enforcement message logged with X-Road signature, SHA-256 hash, and chain link; 10-year immutable retention

**Measurement Method**: Automated hash chain verification run monthly; completeness check: count of log entries per enforcement order

**Dependencies**:
- WORM-capable storage provisioned and configured before go-live
- X-Road Security Server audit log integration with CESA IS (INT-002)

**Risks to Achievement**:
- WORM storage not provisioned in time (operational readiness gap)
- Hash chain integrity broken by database migration or upgrade

---

### Goal G-4: Onboard All CBA-Licensed Commercial Banks Within 12 Months of Go-Live

**Derived From Drivers**: SD-1, SD-6, SD-7, SD-10

**Goal Owner**: CESA Programme Manager; CBA (coordination)

**Goal Statement**: Onboard all CBA-licensed commercial banks (~15 banks) to X-Road ACTIVE status in the bank registry within 12 months of go-live, starting with at least 3 banks at initial launch.

**Why This Matters**: Until all banks are onboarded, enforcement coverage is incomplete — debtors with accounts at non-integrated banks are partially shielded (SD-1). CBA needs complete participation to achieve systemic oversight (SD-7). Banks need the programme to reach scale for the integration investment to be justified (SD-6).

**Success Metrics**:
- **Primary Metric**: Number of banks in ACTIVE status in D5 (Bank Registry) — target: all licensed banks by month 12 post go-live
- **Secondary Metrics**:
  - Banks at ONBOARDING status (in progress) — tracked weekly
  - Banks at MANUAL_ONLY (not yet started) — tracked weekly; target: 0 at month 12

**Baseline**: 0 banks X-Road enabled (all MANUAL_ONLY at programme start)

**Target**: 3+ banks at launch (month 0); all 15+ banks by month 12 post go-live

**Measurement Method**: Bank registry dashboard; monthly status report to CESA Leadership and CBA

**Dependencies**:
- CBA regulatory directive or participation mandate (critical enabler)
- API specification published early enough for banks to plan CBS adapter development (FR-009)
- Each bank deploying its own X-Road Security Server (bank responsibility, TC-002)

**Risks to Achievement**:
- Banks prioritise other IT programmes without CBA mandate (Risk R-001 in REQ)
- Bank CBS adapter quality below standard at certification testing, causing delays

---

### Goal G-5: DPIA Completed and DPA Sign-Off Received Before Go-Live

**Derived From Drivers**: SD-9, SD-3

**Goal Owner**: CESA Programme Manager (DPIA); CESA Leadership (accountable)

**Goal Statement**: Initiate the Data Protection Impact Assessment within 1 month of programme start, engage the RA Data Protection Authority before the detailed design phase, and receive formal DPA sign-off at least 2 months before planned go-live.

**Why This Matters**: Large-scale processing of personal financial data under legal compulsion triggers mandatory DPIA obligations. Failure to complete this before go-live exposes CESA to regulatory enforcement action from the DPA (SD-9) and creates programme risk for the Programme Manager (SD-3).

**Success Metrics**:
- **Primary Metric**: DPA formal sign-off received (binary: Yes/No)
- **Secondary Metrics**:
  - DPIA initiated by month 1 of programme
  - DPA consultation completed at least 2 months before go-live
  - Zero data protection violations post-launch

**Baseline**: DPIA not yet started (status: NOT_STARTED per ARC-001-DATA-v1.0)

**Target**: DPIA formally approved by DPA at least 2 months before pilot go-live

**Measurement Method**: Programme milestone tracking; DPA correspondence log

**Dependencies**:
- Data model (ARC-001-DATA-v1.0) finalised before DPIA can be completed
- DPA engagement requires formal submission; allow 6-8 weeks for DPA review

**Risks to Achievement**:
- DPA requires data model changes that are expensive to retrofit after development starts
- DPA review takes longer than anticipated, delaying go-live

---

### Goal G-6: Reduce Officer Enforcement Processing Time by More Than 80%

**Derived From Drivers**: SD-2, SD-1

**Goal Owner**: CESA Programme Manager; CESA Supervisors

**Goal Statement**: Reduce officer time spent per enforcement order (from case initiation to bank confirmation) from the current baseline to under 5 minutes of active officer effort (for X-Road ACTIVE banks), measured at 3 months post go-live.

**Why This Matters**: Directly addresses officer workload and frustration (SD-2). Enables officers to handle 3x more cases per day, improving overall enforcement throughput (BR-006).

**Success Metrics**:
- **Primary Metric**: Officer active effort time per enforcement order (target: < 5 minutes)
- **Secondary Metrics**:
  - Cases handled per officer per day (target: 3x baseline)
  - Officer satisfaction score (target: > 4.0 / 5.0 in post-launch survey)

**Baseline**: Requires time-motion study (TBD — to be conducted before go-live); estimated at 30-90 minutes per order for X-Road-equivalent actions under current manual process

**Target**: < 5 minutes active officer effort per X-Road enforcement order

**Measurement Method**: Pre-launch time-motion study establishing baseline; post-launch APM data on session duration per enforcement action; officer satisfaction survey at 3 months

**Dependencies**:
- CESA IS user interface must minimise clicks and input fields per order
- Officer training programme completed before go-live

**Risks to Achievement**:
- Poor UI/UX design that does not reduce officer effort relative to manual process
- Officers avoiding the system for familiar manual process (change resistance)

---

### Goal G-7: Implement Configuration-Driven Bank Onboarding (No Code Change)

**Derived From Drivers**: SD-4, SD-3, SD-10

**Goal Owner**: CESA IT Department

**Goal Statement**: Implement the bank registry (D5) and enforcement routing logic so that adding a new bank to the X-Road enforcement channel requires only a registry configuration change — no code change, no deployment — from the first development sprint.

**Why This Matters**: Makes the programme scalable to all 15+ banks without linear IT cost growth (SD-4). Reduces risk for the Programme Manager — bank onboarding does not create deployment risk (SD-3). Enables EKENG to onboard new X-Road members without CESA IS involvement (SD-10).

**Success Metrics**:
- **Primary Metric**: Time to add a new bank to the registry — target: < 1 hour (configuration only)
- **Secondary Metrics**:
  - Number of code deployments caused by bank onboarding — target: 0
  - Bank registry audit log completeness (all changes tracked)

**Baseline**: No bank registry exists; each bank would currently require bespoke code

**Target**: Configuration-only bank onboarding from day one of development

**Measurement Method**: Code review confirming no bank-specific code; registry change log review

**Dependencies**:
- FR-006 implemented in CESA IS from the first development sprint
- X-Road routing configuration format agreed with EKENG

**Risks to Achievement**:
- Edge cases in X-Road member ID formats requiring code handling
- CBS adapter quality variance between banks requiring bank-specific workarounds

---

## Goal-to-Outcome Mapping

### Outcome O-1: Real-Time Enforcement Confirmation — Asset Dissipation Window Eliminated

**Supported Goals**: G-1, G-6

**Outcome Statement**: Enforcement orders issued by CESA officers receive bank confirmation in under 5 seconds (p95 for blocking) and under 15 seconds (p95 for collection), versus the current hours-to-days, with at least 3 banks operational at launch.

**Measurement Details**:

- **KPI**: Enforcement order end-to-end latency (p95)
- **Current Value**: Hours to days (manual process baseline)
- **Target Value**: Blocking < 5 seconds; collection < 15 seconds; discovery < 30 seconds (all p95)
- **Measurement Frequency**: Continuous (per transaction); reported weekly
- **Data Source**: E-003 AuditLogEntry (transmitted_at to confirmed_at delta in E-002)
- **Report Owner**: CESA IT Operations

**Business Value**:

- **Financial Impact**: Reduction in unrecoverable enforcement losses caused by asset dissipation during the enforcement window; estimated significant financial improvement to debt recovery rate (baseline study required)
- **Strategic Impact**: Demonstrates Armenia's digital government modernisation; positions CESA as a benchmark for regional enforcement modernisation
- **Operational Impact**: Officers spend < 5 minutes per order vs hours currently; caseload capacity increases 3x
- **Legal Impact**: Non-repudiable proof of enforcement execution within seconds of issuance; eliminates bank claims of non-receipt

**Timeline**:

- **Phase 1 (Months 1-6)**: Pilot bank live; latency target met for pilot bank; system stable
- **Phase 2 (Months 7-9)**: 5+ banks onboarded; latency maintained under concurrent load
- **Phase 3 (Months 10-12)**: All 15+ banks; stress test at 100 concurrent operations confirms NFR-S-002
- **Sustainment (Year 2+)**: Annual latency and reliability review; capacity planning

**Stakeholder Benefits**:

- **CESA Leadership**: Statutory obligation to execute enforcement orders promptly — now demonstrably met
- **Ministry of Justice**: Enforcement orders executed within seconds of issuance; legally defensible audit trail
- **CESA Officers**: Immediate confirmation; no manual follow-up with banks
- **Bank Compliance Officers**: Automated, signed enforcement — no manual review required

**Leading Indicators** (early signals of success):
- Pilot bank CBS adapter certification test pass rates
- X-Road message round-trip times in staging environment
- Officer engagement in UAT sessions

**Lagging Indicators** (final proof):
- p95 latency sustained at < 5s over 90-day operational period post-launch
- Enforcement debt recovery rate improvement vs pre-launch baseline

---

### Outcome O-2: Complete Enforcement Coverage Across All Licensed Banks

**Supported Goals**: G-2, G-4

**Outcome Statement**: 100% of CBA-licensed commercial banks in X-Road ACTIVE status within 12 months of go-live; account discovery covers all banks simultaneously; no enforcement-relevant bank relationship outside the X-Road channel.

**Measurement Details**:

- **KPI**: Banks in ACTIVE status in D5 Bank Registry as % of all CBA-licensed banks
- **Current Value**: 0%
- **Target Value**: 100% (all CBA-licensed banks) by month 12 post go-live
- **Measurement Frequency**: Monthly
- **Data Source**: D5 Bank Registry; CBA licensed bank list
- **Report Owner**: CESA Programme Manager

**Business Value**:

- **Financial Impact**: Complete enforcement coverage eliminates the ability for debtors to shield assets in non-integrated banks; maximum possible recovery rate achieved
- **Strategic Impact**: Full digitalisation of enforcement channel; Armenia national interoperability platform (X-Road) demonstrably successful in financial sector
- **Operational Impact**: Officers have single-channel access to all bank accounts; no bank-specific manual fallback needed at steady state

**Timeline**:

- **Phase 1 (Months 1-6)**: 3+ pilot banks at ACTIVE; remaining at ONBOARDING or MANUAL_ONLY
- **Phase 2 (Months 7-9)**: 8+ banks at ACTIVE; discovery covers majority of Armenian banking assets
- **Phase 3 (Months 10-12)**: All 15+ banks at ACTIVE; 100% coverage achieved
- **Sustainment (Year 2+)**: New bank licensing triggers automatic onboarding pipeline

**Stakeholder Benefits**:

- **CESA Leadership**: Statutory mandate achievable — enforcement is complete, not partial
- **CBA**: Full systemic visibility into enforcement activity across all supervised banks
- **Creditors/Claimants**: Maximum recovery possible; no banks shielding debtor assets through lack of integration

**Leading Indicators**:
- Number of banks that have started X-Road Security Server deployment (ONBOARDING status)
- API specification adoption rate (banks requesting certification test suite)

**Lagging Indicators**:
- All banks in ACTIVE status (100%)
- Discovery query response rate: 100% of ACTIVE banks respond to every query

---

### Outcome O-3: Legally Defensible Enforcement Record

**Supported Goals**: G-3

**Outcome Statement**: 100% of enforcement actions covered by a cryptographically signed, tamper-evident audit trail retrievable within 30 seconds, with zero successful legal challenges to enforcement actions on procedural grounds.

**Measurement Details**:

- **KPI**: Audit trail completeness (%) and hash chain integrity (%)
- **Current Value**: 0% digital audit trail (paper records only)
- **Target Value**: 100% completeness; 100% chain integrity
- **Measurement Frequency**: Monthly automated hash chain verification; per-transaction completeness check
- **Data Source**: E-003 AuditLogEntry
- **Report Owner**: CESA IT Operations; CESA Legal (for any dispute)

**Business Value**:

- **Legal Impact**: Every enforcement action is independently verifiable by either party (CESA or bank) without reliance on the other's systems; non-repudiation removes the most common basis for procedural challenges
- **Operational Impact**: Audit records retrievable within 30 seconds — no more manual archive searches
- **Compliance Impact**: Meets RA enforcement law's audit obligations; provides evidence for courts and regulatory reviews

**Timeline**:

- **Phase 1 (Before go-live)**: WORM storage provisioned; hash chain genesis created; verified in staging
- **Phase 2 (Go-live)**: 100% completeness from day one — no enforcement action without an audit log entry
- **Sustainment**: Annual audit log integrity review; 10-year retention maintained

**Stakeholder Benefits**:

- **Ministry of Justice**: Court-admissible evidence of enforcement action timing and content
- **CESA Programme Manager**: Professional protection — every decision is documented
- **Bank Compliance Officers**: Proof that they applied a legitimately issued, authenticated order — legal protection

**Leading Indicators**:
- WORM storage configured and tested before go-live
- Hash chain integrity verified in staging environment

**Lagging Indicators**:
- 12-month period with zero broken hash chain links
- Zero successful procedural challenges to enforcement actions

---

### Outcome O-4: Regulatory Compliance — DPIA Approved, Zero Data Breaches

**Supported Goals**: G-5

**Outcome Statement**: DPIA formally signed off by the RA Data Protection Authority at least 2 months before go-live; zero personal data breaches in the 12 months following launch; all data minimisation controls verified operational.

**Measurement Details**:

- **KPI**: DPIA approval status; data breach count; data minimisation control audit pass rate
- **Current Value**: DPIA not started; no controls in place
- **Target Value**: DPA sign-off received; 0 breaches; 100% control pass rate
- **Measurement Frequency**: DPIA — one-time milestone; breach monitoring — continuous; control audit — quarterly
- **Data Source**: DPA correspondence; security monitoring; CESA IT security audit
- **Report Owner**: CESA Programme Manager (DPIA); CESA IT (breach monitoring)

**Business Value**:

- **Compliance Impact**: DPA sign-off grants legal authority to operate; without it, go-live is blocked
- **Reputational Impact**: Zero data breaches protects CESA's and the programme's credibility
- **Financial Impact**: DPA enforcement action for non-compliance carries financial penalties and programme shutdown risk

**Timeline**:

- **Month 1**: DPIA initiated
- **Month 3**: DPA consultation submitted
- **Month 5+**: DPA sign-off received (allowing 6-8 weeks for DPA review)
- **Go-live**: Data minimisation controls verified operational
- **Sustainment**: Quarterly privacy control audit; annual DPIA review

**Stakeholder Benefits**:

- **RA Data Protection Authority**: Proportionate, lawful data processing confirmed before operation begins
- **CESA Leadership**: Legal authority to operate confirmed; reputational risk mitigated
- **Debtors**: Personal financial data processed proportionately and with appropriate safeguards

**Leading Indicators**:
- DPIA initiated by month 1
- DPA consultation meeting confirmed

**Lagging Indicators**:
- DPA formal sign-off letter received
- 12-month operation with zero data breaches

---

### Outcome O-5: CESA Operational Efficiency — Officers Handle 3x Caseload

**Supported Goals**: G-6

**Outcome Statement**: CESA enforcement officers handling X-Road ACTIVE bank cases spend less than 5 minutes of active effort per enforcement order (vs estimated 30-90 minutes manual baseline), enabling 3x increase in cases managed per officer per day.

**Measurement Details**:

- **KPI**: Cases managed per officer per day; officer effort per enforcement order (minutes)
- **Current Value**: TBD (pre-launch time-motion study required)
- **Target Value**: < 5 minutes officer effort per order; 3x case throughput
- **Measurement Frequency**: Monthly (officer capacity metrics)
- **Data Source**: CESA IS session telemetry; supervisor reports; officer survey
- **Report Owner**: CESA Supervisors; CESA Programme Manager

**Business Value**:

- **Operational Impact**: 3x caseload capacity without additional headcount; enforcement backlog reduced
- **Morale Impact**: Officers spend time on judgement and casework rather than administrative dispatch; job satisfaction improvement
- **Financial Impact**: Same enforcement output with existing headcount; or reduced headcount over time if workforce planning allows

**Timeline**:

- **Pre-launch**: Baseline time-motion study completed
- **Month 3 post-launch**: Post-launch efficiency measurement; comparison to baseline
- **Month 6**: Target 80%+ reduction in officer effort confirmed
- **Sustainment**: Annual efficiency benchmark

**Stakeholder Benefits**:

- **CESA Enforcement Officers**: Reduced administrative burden; more time for complex casework
- **CESA Leadership**: Enforcement throughput increases without budget increase
- **Creditors/Claimants**: Faster resolution of enforcement cases; improved recovery timeline

**Leading Indicators**:
- UAT completion rate and officer satisfaction with new system
- Training completion rate before go-live

**Lagging Indicators**:
- 80%+ reduction in officer effort confirmed at month 3
- Officer satisfaction survey score > 4.0/5.0

---

## Complete Traceability Matrix

### Stakeholder → Driver → Goal → Outcome

| Stakeholder | Driver ID | Driver Summary | Goal ID | Goal Summary | Outcome ID | Outcome Summary |
|-------------|-----------|----------------|---------|--------------|------------|-----------------|
| CESA Leadership | SD-1 | Eliminate asset dissipation risk | G-1 | Real-time enforcement < 5 seconds | O-1 | Asset dissipation window eliminated |
| CESA Leadership | SD-1 | Eliminate asset dissipation risk | G-4 | All banks onboarded in 12 months | O-2 | 100% bank coverage |
| CESA Officers | SD-2 | Eliminate manual drudgery | G-1 | Real-time enforcement < 5 seconds | O-1 | Officers get instant confirmation |
| CESA Officers | SD-2 | Eliminate manual drudgery | G-6 | 80%+ officer time reduction | O-5 | 3x caseload capacity |
| CESA Officers | SD-2 | Automated discovery | G-2 | Discovery across all banks < 30s | O-2 | Complete enforcement coverage |
| CESA Programme Manager | SD-3 | Controlled delivery | G-5 | DPIA signed off before go-live | O-4 | Zero breaches, DPA approved |
| CESA Programme Manager | SD-3 | Controlled delivery | G-7 | Config-driven onboarding | O-2 | Banks onboard without deployment risk |
| CESA IT Department | SD-4 | Standards-based architecture | G-7 | Config-driven onboarding | O-2 | Scalable bank onboarding |
| Bank IT Leads | SD-5 | Low-risk CBS integration | G-7 | Clear API spec early (FR-009) | O-2 | Banks onboarded with clear contract |
| Bank Leadership | SD-6 | Regulatory compliance | G-4 | All banks onboarded in 12 months | O-2 | 100% bank coverage (regulatory) |
| CBA | SD-7 | Financial system stability | G-4 | All banks onboarded in 12 months | O-2 | CBA aggregate visibility |
| CBA | SD-7 | Systemic oversight | G-2 | Discovery across all banks | O-2 | Complete enforcement coverage data |
| Ministry of Justice | SD-8 | Legal non-repudiation | G-3 | 100% tamper-evident audit trail | O-3 | Court-admissible evidence |
| RA DPA | SD-9 | Personal data compliance | G-5 | DPIA approved before go-live | O-4 | DPA sign-off; zero breaches |
| EKENG | SD-10 | X-Road ecosystem growth | G-4 | All banks onboarded | O-2 | Platform demonstrates value |
| Bank Compliance Officers | SD-11 | Authenticated enforcement orders | G-3 | 100% signed audit trail | O-3 | Banks legally protected |
| Bank Compliance Officers | SD-11 | Clear structured instructions | G-1 | Real-time < 5 seconds via X-Road | O-1 | Automated enforcement receipt |

### Conflict Analysis

**Competing Drivers**:

- **Conflict C-1**: CESA Leadership (SD-1) wants rapid deployment to close the asset dissipation window as quickly as possible, but Commercial Bank IT Leads (SD-5) need 6-12 months to develop CBS adapters safely. Deploying before banks are ready achieves nothing.
  - **Resolution Strategy**: Phased onboarding (BR-005, G-7). Identify 1-2 willing early-adopter banks (champions) and work with them in parallel with CESA IS development. Pilot launch with those banks; scale to others once the integration is proven. CBA mandate (SD-7) accelerates the timeline for reluctant banks.

- **Conflict C-2**: RA Data Protection Authority (SD-9) requires data minimisation — specifically, only balance ranges returned in discovery — while CESA Officers (SD-2) would benefit from precise balances to prioritise high-value accounts for collection.
  - **Resolution Strategy**: Already resolved in ARC-001-REQ-v1.0 (Conflict C-002) — balance range enum (ZERO/LOW/MEDIUM/HIGH) is returned rather than precise balances. This satisfies DPA data minimisation while giving officers sufficient information to prioritise. If precise balance is legally required for a specific enforcement type, a separate authorised query may be defined in a future phase.

- **Conflict C-3**: CESA Leadership (SD-1) requires 24/7 enforcement availability, but Commercial Bank operations (SD-5, SD-6) operate during banking hours. Collection orders requiring CBS fund transfer cannot execute outside banking hours.
  - **Resolution Strategy**: Architecture separates enforcement action types by availability: blocking operates 24/7 (automated CBS hold does not require banking hours); collection and release operate during defined banking hours. NFR-A-001 is scoped accordingly. Officers are informed which action types are available outside banking hours.

- **Conflict C-4**: CESA Programme Manager (SD-3) wants clean programme boundaries (bank adapters are bank responsibility, TC-002), but Bank IT Leads (SD-5) have limited X-Road integration experience and will need support, creating pressure on CESA IT.
  - **Resolution Strategy**: CESA publishes the API specification (FR-009), a certification test suite, and reference integration guidance. EKENG provides X-Road Security Server onboarding support. Programme boundary is clear, but CESA provides tooling that reduces bank implementation effort.

**Synergies**:

- **Synergy S-1**: CESA Leadership's elimination of asset dissipation risk (SD-1) and Ministry of Justice's legal effectiveness goal (SD-8) are perfectly aligned — G-1 (real-time enforcement) and G-3 (audit trail) together satisfy both, creating a natural coalition.
- **Synergy S-2**: Bank Compliance Officers' desire for authenticated, structured orders (SD-11) aligns directly with CESA IT's goal of a standards-based X-Road integration (SD-4) — the same API specification solves both problems.
- **Synergy S-3**: EKENG's platform growth goal (SD-10) and CESA IT's standards-based architecture goal (SD-4) both benefit from maximum bank onboarding — both stakeholders are natural champions for G-4.
- **Synergy S-4**: The phased onboarding approach (G-7) simultaneously satisfies CESA Programme Manager's risk management (SD-3), Bank IT Leads' need for sufficient lead time (SD-5), and Bank Leadership's regulatory compliance pathway (SD-6) — it is a unifying solution across competing pressures.

---

## Communication & Engagement Plan

### CESA Leadership

**Primary Message**: The programme is delivering the digital foundation for effective enforcement — closing the asset dissipation window that undermines judicial orders — and it is being built with the governance controls (DPIA, audit trail, phased onboarding) that protect CESA's institutional reputation.

**Key Talking Points**:
- Asset dissipation risk is being eliminated through real-time X-Road enforcement (G-1)
- Programme is structured to succeed incrementally — pilot bank go-live before scaling to all 15+ banks
- Legal non-repudiation and audit trail (G-3) protect CESA from procedural challenges

**Communication Frequency**: Fortnightly steering committee; immediate escalation for CBA mandate or DPA issues

**Preferred Channel**: Steering committee briefing; written programme status report

**Success Story**: "We blocked a debtor's accounts at three banks simultaneously within 4 seconds of a court order being issued."

---

### Ministry of Justice

**Primary Message**: The system is being built to the highest legal standards of non-repudiation and audit — enforcement orders will be as legally defensible digitally as any paper process, and more so.

**Key Talking Points**:
- Legal basis reference mandatory in every enforcement message (FR-010)
- X-Road digital signatures enable non-repudiation at protocol level (NFR-SEC-002)
- Tamper-evident audit log retrievable within 30 seconds for court use (G-3)
- Legal reference format agreement needed from Ministry to enable FR-010 implementation

**Communication Frequency**: Monthly (or on-demand for legal reference format agreement)

**Preferred Channel**: Formal correspondence; face-to-face meeting for legal reference format

**Success Story**: "The audit log from the CESA enforcement system was admitted as evidence in a court dispute and confirmed the enforcement order was received and applied within 4 seconds."

---

### RA Data Protection Authority

**Primary Message**: CESA has designed data minimisation into the system's data model from the start and is committed to completing the DPIA and receiving DPA sign-off before any go-live.

**Key Talking Points**:
- Balance ranges (not precise balances) — data minimisation built into the API specification
- Debtor SSN/tax ID encrypted at rest (AES-256) and transmitted only to ACTIVE X-Road banks over mTLS
- DPIA initiated early; DPA consultation requested before detailed design is locked
- No go-live without DPA sign-off — this is a programme gate condition (G-5)

**Communication Frequency**: Formal DPIA submission at month 3; DPA review meeting at month 4-5

**Preferred Channel**: Formal regulatory submission; face-to-face consultation meeting

**Success Story**: "DPIA submitted, DPA concerns addressed in design, sign-off received — programme proceeded with full data protection authority approval."

---

### Central Bank of Armenia

**Primary Message**: The programme is designed to protect bank stability while achieving complete enforcement coverage — and CBA's participation mandate is the single most important enabler of full ecosystem onboarding within 12 months.

**Key Talking Points**:
- Certification testing programme ensures banks are ready before going live — no CBS instability risk
- Aggregate enforcement statistics (INT-004) will give CBA systemic risk visibility once all banks are ACTIVE
- CBA mandate or regulatory guidance would accelerate onboarding from voluntary to obligatory

**Communication Frequency**: Quarterly briefing; programme milestone notifications

**Preferred Channel**: Formal briefing; written programme status letter

**Success Story**: "All 15 CBA-licensed banks onboarded within 11 months of go-live — CBA directive was the decisive enabler."

---

### Commercial Banks (Bank IT Leads and Compliance Officers)

**Primary Message**: CESA will publish a complete, stable API specification early and provide a certification test suite — banks will know exactly what to implement, with adequate lead time.

**Key Talking Points**:
- OpenAPI 3.0 specification published before banks need to start development (FR-009)
- Certification test suite allows banks to self-validate before go-live — no surprises
- X-Road Security Server handles mTLS and signing — CBS adapter focus is business logic only
- Banks acting on signed, authenticated enforcement orders are legally protected

**Communication Frequency**: API specification release — immediate; monthly during bank adapter development; weekly during certification testing

**Preferred Channel**: Developer documentation portal; email; technical working group meetings

**Success Story**: "The certification test suite let us validate our adapter in 2 weeks — the integration was live the following month."

---

### CESA Enforcement Officers

**Primary Message**: This system is being built to make your job faster and simpler — account discovery in seconds, instant confirmation, and a unified interface for all enforcement action types.

**Key Talking Points**:
- No more manual bank-by-bank coordination — discover all accounts across all banks in one query
- Instant blocking confirmation — no more waiting hours to know if enforcement was applied
- You can focus on casework instead of administrative dispatch

**Communication Frequency**: Sprint demo every 2 weeks; change management briefings at key milestones; UAT participation

**Preferred Channel**: Team briefings; hands-on UAT sessions; training workshops

**Success Story**: "I blocked accounts at four banks simultaneously in 6 seconds — the old process would have taken me two hours of phone calls and paperwork."

---

## Change Impact Assessment

### Impact on Stakeholders

| Stakeholder | Current State | Future State | Change Magnitude | Resistance Risk | Mitigation Strategy |
|-------------|---------------|--------------|------------------|-----------------|---------------------|
| CESA Enforcement Officers | Manual document prep; sequential bank dispatch; hours per order | Automated broadcast; instant confirmation; < 5 minutes per order | HIGH | LOW | Early involvement in UAT; training; champion identification |
| CESA Supervisors | No real-time visibility; reliance on officer reports | Real-time dashboard (FR-007); instant status on all cases | MEDIUM | LOW | Dashboard demo; involvement in reporting design |
| CESA IT Department | No enforcement integration; general CESA IS maintenance | New X-Road integration component to build, operate, and maintain | HIGH | LOW-MEDIUM | Architecture review involvement; X-Road training; runbook development |
| CESA System Administrators | No bank registry; no X-Road Security Server | Bank registry management; X-Road SS operations; onboarding process | HIGH | LOW | Early involvement; operational runbook; EKENG support |
| Commercial Bank IT Leads | No enforcement API; manual document receipt | New CBS enforcement adapter (4 endpoints) + X-Road SS deployment | HIGH | MEDIUM-HIGH | Early API spec publication; certification test suite; technical support |
| Bank Compliance Officers | Manual enforcement document review and application | Automated, authenticated enforcement via X-Road; API confirmation | MEDIUM | LOW | Clear process documentation; training on new procedure |
| Commercial Bank Leadership | Enforcement received manually; no structured process | Regulatory obligation to implement and maintain enforcement API | MEDIUM | MEDIUM | CBA mandate; participation agreement with liability protection |

### Change Readiness

**Champions** (Enthusiastic supporters):
- CESA Enforcement Officers — directly motivated by workload reduction; will be visible advocates if UAT goes well
- CESA IT Department — professionally motivated by standards-based architecture; early design involvement will strengthen ownership
- Bank Compliance Officers — directly benefit from structured, authenticated orders; natural advocates within their banks

**Fence-sitters** (Neutral, need convincing):
- Commercial Bank IT Leads — supportive of the concept but concerned about implementation cost and lead time; a clear API specification published early is the decisive factor
- EKENG — supportive of platform growth but neutral on programme priority; more members strengthens their value proposition

**Resisters** (Opposed or skeptical):
- Commercial Bank Leadership — not opposed to the principle but reluctant to allocate IT budget without a CBA mandate; strategy: facilitate CBA directive; provide participation agreement with clear liability protection and implementation timeline flexibility
- Some individual CESA officers (initially) — may prefer familiar manual process; strategy: involve early in UAT, ensure UAT demonstrates clear time savings vs manual, champion program from respected colleagues

---

## Risk Register (Stakeholder-Related)

### Risk R-S1: Banks Decline to Onboard Without Regulatory Mandate

**Related Stakeholders**: Commercial Bank Leadership, Commercial Bank IT Leads, Central Bank of Armenia

**Risk Description**: Without a formal CBA regulatory directive or participation agreement with sufficient incentive, commercial banks may de-prioritise CBS adapter development, leaving the enforcement channel incomplete for 12+ months after go-live.

**Impact on Goals**: G-4 (all banks onboarded in 12 months) would be severely missed; G-2 (discovery coverage) would be incomplete

**Probability**: HIGH (without CBA mandate)

**Impact**: HIGH

**Mitigation Strategy**: Engage CBA early (month 1) to seek formal directive; frame as national digital infrastructure not optional add-on; identify champion banks willing to onboard early to demonstrate programme (volunteer approach for early adopters)

**Contingency Plan**: If CBA mandate is not forthcoming by month 3, adjust G-4 target timeline and present revised 18-month plan to CESA Leadership; activate phased onboarding with early-adopter banks while political pressure on CBA continues

---

### Risk R-S2: DPIA Review Delays Go-Live

**Related Stakeholders**: RA Data Protection Authority, CESA Programme Manager, CESA Leadership

**Risk Description**: DPA review takes longer than the planned 6-8 weeks, or DPA requires changes to the data model that require re-design and re-testing, pushing the go-live date beyond the planned programme schedule.

**Impact on Goals**: G-5 (DPIA signed off before go-live) — directly; G-1, G-4 — by delaying go-live date

**Probability**: MEDIUM

**Impact**: HIGH (go-live blocker)

**Mitigation Strategy**: Initiate DPIA in month 1 of programme (before development begins); request informal pre-submission consultation with DPA to identify any concerns early; ensure data minimisation controls (balance range, encrypted PII) are clearly documented in DPIA submission

**Contingency Plan**: If DPA requires data model changes, assess impact: if minor (e.g., additional access controls), implement in next sprint; if major (e.g., fundamental data flow change), escalate to CESA Leadership and re-plan timeline

---

### Risk R-S3: Legal Reference Format Not Agreed

**Related Stakeholders**: Ministry of Justice, CESA Programme Manager

**Risk Description**: Court order reference format not standardised with the Ministry of Justice before development begins, causing FR-010 validation implementation to be based on assumptions that may need to change after go-live.

**Impact on Goals**: G-3 (legal audit trail) — legal reference is mandatory in all enforcement messages; G-1 — orders without valid legal reference are rejected

**Probability**: MEDIUM

**Impact**: MEDIUM-HIGH (late format change requires re-testing)

**Mitigation Strategy**: Schedule a dedicated legal reference format agreement meeting with Ministry of Justice in month 1; document agreed format in requirements and share with banks; include format validation in certification test suite

**Contingency Plan**: If agreement is delayed, implement a flexible format validator (pattern-configurable) in month 2 so that the format can be updated by configuration; note this as a launch-dependency in programme plan

---

### Risk R-S4: Officer Change Resistance — Preference for Familiar Manual Process

**Related Stakeholders**: CESA Enforcement Officers

**Risk Description**: Officers continue using manual processes (phone calls, emails to banks) out of familiarity, distrust of the new system, or because the new system initially has a worse UX than expected, resulting in low adoption and unrealised efficiency gains.

**Impact on Goals**: G-6 (80%+ officer time reduction) — adoption-dependent; O-5 (3x caseload) — dependent on actual usage

**Probability**: LOW-MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**: Involve officers in UAT early and ensure UAT scenarios demonstrate clear time savings; identify officer champions in each CESA department; require CESA supervisors to mandate use of the new system for X-Road-enabled banks from go-live; post-launch satisfaction survey at month 3

**Contingency Plan**: If adoption is below 70% at month 3, conduct structured user research sessions to identify UX blockers; implement targeted fixes in the next sprint; consider supervisor-level reporting on system usage rates

---

### Risk R-S5: Bank CBS Adapter Quality Below Certification Standard

**Related Stakeholders**: Commercial Bank IT Leads, Bank Compliance Officers, CESA Programme Manager

**Risk Description**: One or more banks develop CBS adapters that pass basic functional testing but fail under edge cases (partial funds, zero-balance accounts, simultaneous requests), causing enforcement errors or system instability after go-live.

**Impact on Goals**: G-1 (real-time enforcement quality) — incorrect bank responses undermine officer trust; G-4 (bank onboarding timeline) — failed certification delays bank go-live

**Probability**: MEDIUM

**Impact**: HIGH (enforcement error causing wrongful blocking is CRITICAL)

**Mitigation Strategy**: Publish a comprehensive certification test suite covering all response scenarios (including partial funds, zero balance, retry, and simultaneous request scenarios); require banks to pass all test cases before receiving ACTIVE status; conduct CESA-side integration testing with each bank in a staging environment before production

**Contingency Plan**: If a bank fails certification, set to ONBOARDING status and provide specific feedback; do not activate until all test cases pass; escalate to CBA if a bank is repeatedly failing certification without addressing issues

---

### Risk R-S6: EKENG Registration Bottleneck

**Related Stakeholders**: EKENG, Commercial Bank IT Leads, CESA IT Department

**Risk Description**: EKENG's X-Road member registration process takes longer than expected for CESA or individual banks, creating a bottleneck that delays Security Server deployment and the ability to test integration.

**Impact on Goals**: G-1 (pilot bank timeline) — cannot test without both parties being registered; G-4 (all banks in 12 months) — registration is a prerequisite for each bank

**Probability**: LOW-MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**: Engage EKENG in month 1 to understand registration timeline; initiate CESA's own registration immediately; request a streamlined registration track for the enforcement integration programme given its national significance

**Contingency Plan**: If EKENG registration is the bottleneck, escalate through CBA (which has authority over EKENG) to accelerate the process

---

## Governance & Decision Rights

### Decision Authority Matrix (RACI)

| Decision Type | Responsible | Accountable | Consulted | Informed |
|---------------|-------------|-------------|-----------|----------|
| Programme scope and budget | CESA Programme Manager | CESA Leadership | Ministry of Justice | All stakeholders |
| API specification finalisation | CESA IT Department | CESA Programme Manager | Bank IT Leads, Ministry of Justice | Banks, EKENG |
| Bank certification approval | CESA IT Department | CESA Programme Manager | Bank IT Leads | CBA, CESA Leadership |
| DPIA submission and approval | CESA Programme Manager | CESA Leadership | RA DPA, CESA IT | All |
| Legal reference format agreement | CESA Programme Manager | CESA Leadership | Ministry of Justice | CESA IT, Banks |
| Go/No-go for pilot bank go-live | CESA Programme Manager | CESA Leadership | Ministry of Justice, DPA, EKENG | CBA, Pilot Banks |
| Go/No-go for each subsequent bank | CESA IT Department | CESA Programme Manager | Bank IT Leads, CBA | CESA Leadership |
| Bank registry configuration changes | CESA System Administrators | CESA IT Department | CESA Programme Manager | CESA Leadership |
| Incident response (enforcement failure) | CESA IT Operations | CESA IT Department | Affected bank, EKENG | Officers, Supervisors |
| Programme escalation (strategic) | CESA Programme Manager | CESA Leadership | CBA, Ministry of Justice | All |

### Escalation Path

1. **Level 1 — Day-to-Day**: CESA IT Department / CESA System Administrators (bank integration issues, configuration changes, operational incidents)
2. **Level 2 — Programme**: CESA Programme Manager (scope, timeline, bank certification, requirements conflicts, non-routine bank issues)
3. **Level 3 — Strategic**: CESA Leadership (budget, go/no-go decisions, CBA escalation, DPA issues, Ministry of Justice legal questions)
4. **Level 4 — External**: CBA (bank participation mandate escalation); DPA (data protection dispute); Ministry of Justice (legal framework questions)

---

## Validation & Sign-off

### Stakeholder Review

| Stakeholder | Review Date | Comments | Status |
|-------------|-------------|----------|--------|
| CESA Leadership | PENDING | — | PENDING |
| CESA Programme Manager | PENDING | — | PENDING |
| Ministry of Justice | PENDING | — | PENDING |
| Central Bank of Armenia | PENDING | — | PENDING |

### Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Programme Sponsor | | | |
| Programme Manager | | | |
| Enterprise Architect | | | |

---

## Appendices

### Appendix A: Stakeholder Engagement Notes

All stakeholder analysis in this document is derived from the requirements document (ARC-001-REQ-v1.0) and the business process document (CESA-BANKS-BP.pdf). Formal stakeholder interviews are recommended before this document is moved from DRAFT to APPROVED status. The following priority interviews are recommended:

- **Priority 1 (Month 1)**: CESA Leadership — confirm strategic priorities and CBA mandate approach
- **Priority 1 (Month 1)**: Ministry of Justice — legal reference format agreement (G-3 dependency)
- **Priority 1 (Month 1)**: RA Data Protection Authority — pre-DPIA informal consultation
- **Priority 2 (Month 2)**: Central Bank of Armenia — enforcement integration briefing; regulatory mandate discussion
- **Priority 2 (Month 2)**: Commercial bank IT leads (2-3 banks) — API specification review; pilot bank identification
- **Priority 3 (Month 3)**: CESA Enforcement Officers — user research; UAT baseline establishment

### Appendix B: References

- `projects/001-cesa-banks/ARC-001-REQ-v1.0.md` — Requirements document (stakeholder list, business requirements, driver sources)
- `projects/001-cesa-banks/ARC-001-DATA-v1.0.md` — Data model (data governance structure, DPIA status)
- `projects/001-cesa-banks/diagrams/ARC-001-DIAG-001-v1.0.md` — System context diagram
- `projects/001-cesa-banks/diagrams/ARC-001-DFD-001-v1.0.md` — Data flow diagram
- RA Law on Enforcement Proceedings — legal framework
- RA Law on Personal Data Protection — DPIA obligations
- X-Road Protocol 6 specification — interoperability platform

---

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| CBBP | CESA-BANKS-BP.pdf | Business Process | `projects/001-cesa-banks/external/` | Existing AS-IS and to-be business process swimlane diagrams for enforcement actions across RA commercial banks. Three pages covering manual current state and X-Road-based automated to-be flows for account blocking, fund collection, restriction lifting, and account discovery. |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| CBBP-C1 | CBBP | Page 1 — AS-IS swimlane | Stakeholder Need | AS-IS process shows manual document preparation, review steps, and sequential dispatch to banks — source of hours-to-days enforcement delay and officer workload |
| CBBP-C2 | CBBP | Page 1 — TO-BE swimlane | Stakeholder Need | TO-BE state shows enforcement actions transmitted via X-Road (globe icon) with real-time confirmation flows — basis for SD-1, SD-4, SD-10 drivers |
| CBBP-C3 | CBBP | Page 2 — account discovery flow | Stakeholder Need | Separate discovery/enquiry process showing CESA querying banks via X-Road — basis for SD-2 (officer needs automated discovery) and SD-7 (CBA systemic oversight) |
| CBBP-C4 | CBBP | Pages 1-3 — all flows | Compliance Constraint | All process flows include explicit legal decision/order reference validation steps — basis for SD-8 (Ministry of Justice legal non-repudiation) and SD-9 (DPA compliance) |
| CBBP-C5 | CBBP | Page 3 — departmental variant | Business Requirement | Departmental routing variant shows multiple CESA departments originating enforcement — basis for SD-6 (bank leadership regulatory compliance) and SD-10 (EKENG platform ecosystem) |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:stakeholders` command
**Generated on**: 2026-04-22 GMT
**ArcKit Version**: 4.9.1
**Project**: CESA-Banks Enforcement Integration (Project 001)
**AI Model**: claude-sonnet-4-6
