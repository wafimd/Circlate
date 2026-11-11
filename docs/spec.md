# Circlate — Workforce Operating System

## Complete Architecture & Design Package

Nov 10, 2026 · @Wafi Muhamad

---

## Phase 1 — Business Analysis

### 1. Product Vision

Circlate is the Workforce Operating System built for the businesses that run Southeast Asia — the SME owner managing 25 staff across two restaurant locations, the HR manager at a 200-person construction contractor, the security company dispatching guards across Brunei at 2 a.m. It replaces the spreadsheet, the WhatsApp approval chain, and the wall-mounted attendance sheet with a single mobile-first platform that is affordable, opinionated, and fast to deploy.

The product vision is: **every business in ASEAN — regardless of size — deserves professional-grade workforce management, delivered for a flat monthly fee they can justify in the first week.**

### 2. Market Positioning

Circlate occupies the gap between consumer apps (too simple, no compliance) and enterprise HRMS platforms (too expensive, too slow, too complex). It is priced on a per-company flat fee, not per employee, which means a 200-person firm pays the same as a 50-person firm at the same tier — a sharp differentiator in a market conditioned by Workday and SuccessFactors per-seat pricing.

**Primary competitor landscape:**

| Competitor | Weakness vs Circlate |
| --- | --- |
| Workday / SAP SuccessFactors | Priced for enterprise; 6–18 month deployments; no ASEAN localisation |
| Sage HR / BambooHR | No offline attendance; limited ASEAN compliance |
| Kakitangan (MY) | Malaysia-centric; no training compliance module |
| Excel + WhatsApp | Zero audit trail; no mobile clock-in; manual approvals |
| Local payroll vendors | Payroll only; no recruitment, performance, or compliance |

**Positioning statement:** Circlate is the only mobile-first, compliance-aware Workforce OS built for ASEAN SMEs, deployed in under a day, priced for the region.

### 3. User Personas

**Persona 1 — Zainab, Restaurant Chain HR Manager (Brunei)** Manages 45 staff across 3 F&B outlets. Tracks attendance manually in Excel, approves leave via WhatsApp. Loses 4 hours/week on payroll prep. Primary pain: no audit trail, frequent disputes about overtime and late arrivals. Wants: mobile clock-in, automatic overtime calculation, leave visibility at a glance.

**Persona 2 — Haji Shahril, Construction Company Owner (SME)** 68 employees; mix of local staff and contract workers. Needs to track certifications (BOSIET, Working at Height, First Aid) for safety compliance audits. Currently uses a folder of paper certificates. Primary pain: expired cert discovered on-site during an audit. Wants: expiry alerts 30/60/90 days out, compliance dashboard for site managers.

**Persona 3 — Nurul, HR Executive at a Security Company** 140 guards across multiple sites, shift work, rotating rosters. High turnover, frequent recruitment. Primary pain: onboarding paperwork takes 3 days, roster conflicts discovered day-of. Wants: ATS Kanban board, QR clock-in with GPS validation, mobile shift view.

**Persona 4 — Marcus, IT Manager at a Professional Services Firm** Responsible for data security and system reliability. Evaluating whether to use SaaS or self-host. Primary pain: data sovereignty concerns, no SSO integration with existing Azure AD. Wants: self-hosted Docker option, Keycloak SSO, audit logs.

**Persona 5 — Farah, Line Manager (Retail)** Manages 12 store staff. Not an HR professional. Needs to approve leave, see who is on shift today, and escalate an expense claim — all from her phone in under 60 seconds. Primary pain: approval requests buried in email. Wants: push notification approvals with one-tap accept/reject.

### 4. User Types

| Role | Description | Primary Device |
| --- | --- | --- |
| System Admin | Full platform control; manages tenants (SaaS) or company config | Desktop |
| Company Admin | Configures company settings, billing, integrations | Desktop |
| HR Manager | Full HR access; runs recruitment, leave, compliance | Desktop + Mobile |
| Recruiter | ATS access; manages candidates, interviews, pipeline | Desktop |
| Finance | Expense approvals, billing visibility | Desktop |
| Compliance Admin | Training compliance matrix, certificate management | Desktop |
| Manager | Approves leave/expenses; views team attendance, performance | Mobile + Desktop |
| Employee | Self-service: clock-in, leave requests, expense claims, profile | Mobile |

### 5. Functional Requirements

**FR-01 — Identity & Access** Support SSO via Keycloak (OIDC/SAML2). Multi-factor authentication. Role-based access per module. Subdomain-per-tenant routing.

**FR-02 — Tenant Onboarding** Self-service company registration. Automated subdomain provisioning. 14-day free trial. Subscription plan selection via Pocket Pay. Database and storage provisioning per tenant.

**FR-03 — Employee Management** Create/edit employee profiles with personal data, employment details, emergency contacts, documents, and employment history. Soft-delete with data retention.

**FR-04 — Organisation Structure** Departments, teams, positions, reporting lines. Org chart visualisation. Headcount planning view.

**FR-05 — Attendance** QR code generation per employee. GPS coordinates captured on clock-in/out. Offline sync for mobile. Shift definitions. Overtime detection. Late arrival flagging. Remote/hybrid work mode.

**FR-06 — Leave Management** Configurable leave types. Annual leave accrual. Balance tracking. Manager approval workflow. Calendar view. Mobile request and approval.

**FR-07 — Recruitment ATS** Kanban pipeline (Applied → Screening → Interview → Assessment → Offer → Hired/Rejected). Candidate profiles with resume upload. Interview scheduling and notes. Pipeline reporting.

**FR-08 — Expense Management** Employee expense claims with receipt photo upload. Category codes. Approval workflow. Finance export.

**FR-09 — Training Compliance** Course and provider registry. Employee training records. Certificate upload. Expiry tracking. Automated notifications at 90/60/30/0 days. Compliance matrix by department and position. Dashboard and reports.

**FR-10 — Performance Management** Goal setting (OKR/KPI). Review cycles. 360-degree feedback. Manager notes.

**FR-11 — Skills Matrix** Employee skill profiles. Competency levels. Gap analysis. Succession planning view.

**FR-12 — Asset Management** Asset registry (device, vehicle, card). Assignment to employee. Return tracking. Condition notes.

**FR-13 — Document Management** Secure upload and storage. Document types (contract, certificate, policy). Version control. Employee-visible vs HR-only.

**FR-14 — Announcements** Company-wide or department-targeted posts. Read receipts. Scheduled publishing.

**FR-15 — Helpdesk** Employee ticket submission (HR, IT, Facilities). Status tracking. Manager/admin resolution.

**FR-16 — Approvals** Unified manager approval inbox. Push notifications. One-tap mobile approve/reject with comment.

**FR-17 — Reporting** Embedded Metabase dashboards. Headcount, attendance, leave, compliance, expense reports. Export to CSV/PDF.

**FR-18 — Billing** Subscription management via Pocket Pay. Plan upgrades/downgrades. Trial-to-paid conversion. Invoice generation. Payment webhook handling.

**FR-19 — Mobile Application** Flutter iOS and Android app. QR clock-in, GPS validation, leave requests, expense claims, approvals, announcements, profile.

### 6. Non-Functional Requirements

| ID | Requirement | Target |
| --- | --- | --- |
| NFR-01 | API response time (p95) | < 300 ms |
| NFR-02 | Mobile app cold-start time | < 2 s |
| NFR-03 | Uptime SLA (SaaS) | 99.9% monthly |
| NFR-04 | Concurrent users per tenant | 500 |
| NFR-05 | File upload max size | 50 MB |
| NFR-06 | Data encryption at rest | AES-256 |
| NFR-07 | Data encryption in transit | TLS 1.3 |
| NFR-08 | GDPR-equivalent data residency | Configurable per tenant |
| NFR-09 | Audit log retention | 7 years |
| NFR-10 | Mobile offline support | Attendance clock-in queue up to 24 h |
| NFR-11 | Deployment time (self-hosted) | < 30 min via Docker Compose |
| NFR-12 | Accessibility | WCAG 2.1 AA |
| NFR-13 | Supported browsers | Chrome 110+, Firefox 110+, Safari 16+, Edge 110+ |
| NFR-14 | Mobile OS support | iOS 16+, Android 11+ |

### 7. Business Requirements

- **BR-01** Flat per-company pricing with no per-seat fees enables SMEs to grow headcount without bill shock.
- **BR-02** Free tier (≤ 30 employees) drives adoption and word-of-mouth in target markets; conversion gate is feature unlock, not employee count.
- **BR-03** Brunei market requires BND currency support, Brunei public holiday calendar, and IC/passport number fields in employee profiles.
- **BR-04** Self-hosted mode (Mode C) is required to close government and enterprise accounts in air-gapped environments.
- **BR-05** White-label capability (Enterprise tier) enables reseller and OEM partnerships across ASEAN.
- **BR-06** PocketPay integration is the exclusive payment gateway; no Stripe or other processor in Phase 1.
- **BR-07** The platform must operate without a sales team for the Free and Business tiers — fully self-service signup and onboarding.
- **BR-08** Metabase is the reporting engine; custom report builder is out of scope for Phase 1.

### 8. Risks

| Risk | Likelihood | Impact | Mitigation |
| --- | --- | --- | --- |
| PocketPay API instability delays billing launch | Medium | High | Build billing service with provider-abstraction layer; fallback to manual invoice |
| Keycloak complexity delays auth delivery | Medium | High | Use Keycloak Docker image with pre-baked realm config; allocate sprint buffer |
| Multi-tenant DB-per-tenant approach increases infra cost | High | Medium | Use connection pooling (PgBouncer); right-size tenant DB instances |
| Flutter offline sync edge cases cause data loss | Medium | High | Implement idempotent sync with server-side conflict resolution; extensive device testing |
| PDPO (Brunei data protection) compliance gaps | Low | High | Engage local legal counsel pre-launch; build data export and right-to-erasure features early |
| Slow SME adoption due to change aversion | Medium | Medium | Invest in onboarding wizard, guided tour, and 1-click demo data seeding |
| iOS App Store review delays | Medium | Medium | Submit TestFlight build 6 weeks before launch; maintain web fallback for mobile flows |

### 9. Assumptions

- Brunei is the launch market; ASEAN expansion (MY, SG, ID) follows in Phase 2+.
- PocketPay provides a stable sandbox environment for development and testing.
- Customers in the Free tier are responsible for their own data backup in self-hosted mode.
- Payroll calculation and statutory deductions (TAP, SCP in Brunei) are out of scope for Phase 1 — the platform exports attendance data for use with a payroll processor.
- Metabase is deployed as a shared service in SaaS mode; each tenant accesses only their own data via row-level security.
- The iOS and Android apps are distributed via App Store and Google Play respectively; enterprise distribution (MDM) is an Enterprise tier feature.
- Phase 1 targets English as the only UI language; Malay (Bahasa Melayu) localisation is Phase 2.

### 10. Success Metrics

| Metric | 3-Month Target | 12-Month Target |
| --- | --- | --- |
| Tenants created (Free + paid) | 10 | 50 |
| Free-to-paid conversion rate | — | 25% |
| Monthly Recurring Revenue | BND 2,000 | BND 25,000 |
| Employee profiles created | 1,000 | 20,000 |
| Attendance clock-ins via mobile | 10,000/month | 200,000/month |
| NPS score | — | > 45 |
| Time-to-first-clock-in after signup | < 10 min | < 10 min |
| Support tickets per active tenant/month | — | < 0.5 |
| Self-hosted deployments | 5 | 50 |

## Phase 2 — Domain Design

Circlate is modelled as 20 bounded contexts across two tiers: **Foundation Domains** (Organisation, Authority Profiles, Position Management, Work Structures) that the entire platform depends on, and **Capability Domains** (Employees, Recruitment, Attendance, Leave, Expenses, and others) that consume the foundation. The core architectural principle is that **Positions own authority; employees inherit it by occupying positions**. Each context owns its data and communicates with others exclusively through domain events or explicit service calls — no shared database tables across contexts.

### Context Map

| Bounded Context | Tier | Core Responsibility |
| --- | --- | --- |
| Identity | Foundation | Authentication, users, sessions, MFA |
| Tenant Management | Foundation | Company provisioning, configuration, subdomain routing |
| Billing | Foundation | Subscriptions, plans, payments, invoices |
| **Organisation** | **Foundation** | **Legal entity, business units, departments — structural container** |
| **Authority Profiles** | **Foundation** | **Business authority definitions; derives technical permissions** |
| **Position Management** | **Foundation** | **Position templates, establishment, positions, grades, lifecycle, acting assignments** |
| **Work Structures** | **Foundation** | **Teams, projects, contracts, sites — operational execution model** |
| Employees | Capability | Personnel records, employment history, compensation, position occupancy |
| Recruitment | Capability | Vacancy-driven ATS pipeline, candidates, interviews, offers |
| Attendance | Capability | Clock-in/out, shifts, overtime, GPS/QR; routes exceptions through position hierarchy |
| Leave | Capability | Leave types, balances, requests; approval routes via position hierarchy |
| Expenses | Capability | Claims, receipts; approval routes via authority limits + position hierarchy |
| Performance | Capability | Goals, reviews, competency assessment; frameworks inherited from Position |
| Skills | Capability | Skill profiles, competency gaps, succession planning |
| Training Compliance | Capability | Courses, records, certificates; compliance requirements owned by Position |
| Assets | Capability | Asset registry, assignments, returns |
| Documents | Capability | Document storage, versions, access control |
| Announcements | Capability | Posts, targeting by position/department/BU, read receipts |
| Helpdesk | Capability | Tickets, categories, resolution |
| Notifications | Capability | Multi-channel delivery; routing ownership follows position hierarchy |

---

### BC-01 — Identity

**Purpose:** Owns the authentication lifecycle — login, token issuance, MFA, session management, and SSO federation. Delegates to Keycloak as the authority; this context wraps Keycloak with application-level user records and tenant association.

**Aggregates & Entities:**

- `User` (aggregate root) — id, email, keycloak\_id, tenant\_id, status, roles\[\]
- `Session` — token reference, issued\_at, expires\_at, device\_info
- `MfaEnrollment` — method (TOTP/SMS), enrolled\_at, verified

**Value Objects:**

- `Email` — validated format, lowercase-normalised
- `Role` — enum: Employee, Manager, HR, Recruiter, Finance, ComplianceAdmin, SystemAdmin
- `Permission` — resource + action pair

**Domain Events:**

- `UserCreated` — triggers welcome notification
- `UserDeactivated` — cascades to revoke active sessions
- `PasswordResetRequested`
- `SsoLoginCompleted`

**Services:**

- `KeycloakProvisioningService` — creates Keycloak realm users on tenant provisioning
- `TokenValidationService` — validates JWT for inbound API requests

---

### BC-02 — Tenant Management

**Purpose:** Manages the full lifecycle of a company tenant — provisioning, configuration, subdomain assignment, and isolation boundaries.

**Aggregates & Entities:**

- `Tenant` (aggregate root) — id, company\_name, subdomain, status, tier, region, created\_at
- `TenantConfiguration` — timezone, locale, currency, public\_holidays\[\], working\_hours
- `TenantFeatureFlag` — feature\_key, enabled

**Value Objects:**

- `Subdomain` — validated slug (kebab-case, 3–30 chars, unique)
- `Tier` — enum: Free, Business, Professional, Enterprise
- `Region` — enum: BN, MY, SG, ID (data residency)

**Domain Events:**

- `TenantProvisioned` — triggers DB creation, MinIO bucket, Keycloak realm, admin user creation
- `TenantSuspended` — billing payment failure
- `TenantDeleted` — data retention policy applied
- `TierUpgraded` / `TierDowngraded`

**Services:**

- `TenantProvisioningOrchestrator` — coordinates DB, storage, auth realm setup
- `SubdomainResolver` — maps incoming host header to tenant\_id

---

### BC-03 — Billing

**Purpose:** Manages subscription state, payment processing via PocketPay, invoice generation, and trial lifecycle.

**Aggregates & Entities:**

- `Subscription` (aggregate root) — tenant\_id, plan, status, trial\_ends\_at, current\_period\_start, current\_period\_end
- `Invoice` — id, amount, currency, status, issued\_at, paid\_at, pdf\_url
- `PaymentMethod` — pocket\_pay\_customer\_id, card\_last4, expires
- `WebhookEvent` — event\_type, payload, processed\_at, idempotency\_key

**Value Objects:**

- `Money` — amount (decimal) + currency (BND/USD)
- `PlanTier` — Free / Business / Professional / Enterprise
- `BillingCycle` — Monthly / Annual

**Domain Events:**

- `SubscriptionCreated`
- `SubscriptionRenewed`
- `PaymentFailed` — triggers grace period, then suspension
- `TrialExpired` — triggers conversion prompt
- `InvoiceIssued`

**Services:**

- `PocketPayGateway` — wraps PocketPay API for charge, refund, webhook verification
- `InvoiceGenerator` — PDF generation and storage
- `TrialExpiryScheduler` — cron-based trial expiry checks

---

### BC-04 — Organisation

**Purpose:** Foundational platform domain. Defines the structural container — the legal entity, business units, and departments — within which Positions, Authority Profiles, and Work Structures operate. All Capability Domains depend on this context. Organisation is established before employees are onboarded.

**Aggregates & Entities:**

- `Organisation` (aggregate root) — id, tenant\_id, legal\_name, registration\_no, country, industry, primary\_currency, created\_at
- `BusinessUnit` — id, organisation\_id, name, code, parent\_business\_unit\_id (self-ref, nullable), cost\_centre\_code
- `Department` — id, business\_unit\_id, name, code, cost\_centre\_code, head\_position\_id (nullable)

**Value Objects:**

- `OrganisationAddress` — street, city, state, country, post\_code
- `CostCentre` — code, name, business\_unit\_id

**Domain Events:**

- `OrganisationCreated` — tenant\_id, organisation\_id
- `DepartmentCreated` — department\_id, business\_unit\_id
- `BusinessUnitRestructured` — business\_unit\_id, new\_parent\_id

**Services:**

- `OrganisationHierarchyService` — resolve full structural path (org → BU → dept) for any entity
- `CostCentreService` — resolve cost centre for a position or work structure assignment

---

---

### BC-04b — Authority Profiles

**Purpose:** Owns business authority definitions — what roles *can do*, not what screens they can see. Technical permissions are derived from authority; organisation design never couples to UI design. Authority Profiles are reusable across Position Templates.

**Aggregates & Entities:**

- `AuthorityProfile` (aggregate root) — id, tenant\_id, name, description; e.g. *Manager Standard*, *Supervisor Standard*
- `AuthorityGrant` — authority\_profile\_id, authority\_key (e.g. `Leave.Approve`, `Expense.Approve`, `Overtime.Authorise`, `Recruitment.Initiate`, `Attendance.ReviewException`), scope (Own | Team | Department | Organisation)

**Value Objects:**

- `AuthorityKey` — string enum of all business authority verbs; source of truth for permission derivation
- `DerivedPermissionSet` — computed read/write/action permission tokens produced from an AuthorityProfile

**Domain Events:**

- `AuthorityProfileCreated`
- `AuthorityGrantAdded` — authority\_profile\_id, authority\_key
- `AuthorityGrantRevoked`

**Services:**

- `PermissionDerivationService` — translates AuthorityProfile → technical permission tokens consumed by the authorisation layer
- `EffectiveAuthorityService` — resolves an employee's merged effective authority from their current Position assignment(s)

---

### BC-04c — Position Management

**Purpose:** The organisational authority model. Positions own authority, compliance requirements, performance frameworks, and job descriptions. Employees inherit all of these by occupying a Position. Manages the full Position lifecycle and all assignment types.

**Aggregates & Entities:**

- `PositionGrade` (aggregate root) — id, tenant\_id, code (G1–Gn), min\_salary, mid\_salary, max\_salary, currency
- `PositionTemplate` (aggregate root) — id, tenant\_id, title, description, responsibilities, authority\_profile\_id, required\_skills\[\], required\_certifications\[\], grade\_id, performance\_framework\_id, competency\_requirements\[\]
- `WorkforceEstablishment` — id, department\_id, position\_template\_id, approved\_headcount; vacancy count = approved\_headcount − filled instances
- `Position` — id, establishment\_id, department\_id, business\_unit\_id, position\_template\_id, reports\_to\_position\_id (self-ref), cost\_centre\_code, state (Planned | Vacant | Filled | ActingCoverage | Frozen | Abolished), instance\_number
- `EmployeeAssignment` — id, employee\_id, position\_id, assignment\_type (Primary | Secondary | Acting | Temporary), start\_date, end\_date, assignment\_status, acting\_compensation\_method, acting\_compensation\_value

**Value Objects:**

- `AssignmentType` — Primary | Secondary | Acting | Temporary
- `PositionState` — Planned | Vacant | Filled | ActingCoverage | Frozen | Abolished
- `ActingCompensation` — method (FixedAllowance | PercentageUplift | PositionDifferential | None), amount, currency

**Domain Events:**

- `PositionCreated` — position\_id, department\_id, template\_id
- `PositionVacancyOpened` — position\_id (triggers Recruitment context)
- `PositionFilled` — position\_id, employee\_id, assignment\_id
- `ActingAssignmentActivated` — position\_id, acting\_employee\_id, start\_date, end\_date (triggers authority transfer in all dependent contexts)
- `ActingAssignmentEnded` — position\_id, acting\_employee\_id
- `PositionAbolished` — position\_id

**Services:**

- `ApprovalChainResolver` — walks the reports\_to hierarchy to resolve the approval chain for any entity (leave, expense, overtime, attendance exception)
- `ActingCoverageService` — activates/deactivates acting assignments; notifies all dependent contexts via domain event
- `VacancyMonitorService` — compares establishment headcount vs filled positions; raises PositionVacancyOpened when unfilled
- `ComplianceInheritanceService` — returns merged compliance requirements (position + work structure) for an employee assignment

---

### BC-04d — Work Structures

**Purpose:** Operational execution model, separate from organisational authority. Teams, projects, contracts, sites, and programmes through which work is delivered. Employees may participate in multiple Work Structures simultaneously. Work Structures carry operational responsibility and cost allocation but do not confer organisational authority.

**Aggregates & Entities:**

- `WorkStructure` (aggregate root) — id, tenant\_id, name, code, type (Team | Project | Programme | Contract | Site | Region | OperationalUnit | TaskForce | Committee | Branch), parent\_work\_structure\_id (self-ref, nullable), state (Active | Completed | Suspended | Archived), start\_date, end\_date
- `WorkStructureMembership` — id, work\_structure\_id, employee\_id, role\_in\_structure (Lead | Member | Specialist), allocation\_pct (0–100), assignment\_type (Primary | Secondary | Project | Site | Temporary), start\_date, end\_date, assignment\_reason
- `WorkStructureComplianceRequirement` — work\_structure\_id, certification\_id, training\_id, mandatory (bool); merged with Position requirements to compute employee compliance status

**Value Objects:**

- `AllocationPercentage` — integer 0–100; sum across all active work structures for one employee should not exceed 100 (warning, not hard block)
- `WorkStructureType` — Team | Project | Programme | Contract | Site | Region | OperationalUnit | TaskForce | Committee | Branch

**Domain Events:**

- `WorkStructureCreated` — work\_structure\_id, type
- `MembershipAssigned` — work\_structure\_id, employee\_id, allocation\_pct
- `AllocationChanged` — work\_structure\_id, employee\_id, old\_pct, new\_pct
- `WorkStructureCompleted` — work\_structure\_id

**Services:**

- `UtilisationService` — computes workforce utilisation per work structure from allocation percentages
- `WorkStructureApprovalRouter` — routes project timesheets and resource allocation requests to the Work Structure lead (separate from organisational approval chain)
- `WorkStructureComplianceService` — merges position + work structure compliance requirements to determine employee readiness for assignment

### BC-05 — Employees

**Purpose:** The canonical record of a person employed by the organisation. Employees do not own authority — they are occupants of Positions. The Employee context holds personal data, employment history, and compensation records. All authority, compliance requirements, approval rights, and performance frameworks are inherited through Position assignments managed in BC-04c.

**Aggregates & Entities:**

- `Employee` (aggregate root) — id, tenant\_id, employee\_number, first\_name, last\_name, ic\_number, nationality, gender, dob, photo\_url, status (Active | OnLeave | Suspended | Terminated); note: department/position/authority resolved via EmployeeAssignment in BC-04c, never stored directly
- `EmploymentRecord` — employee\_id, employment\_type (FullTime | PartTime | Contract | Intern), start\_date, end\_date, probation\_end\_date, termination\_reason
- `CompensationPackage` — employee\_id, base\_salary, currency, commission\_type, commission\_value, effective\_from; references PositionGrade for band validation
- `Allowance` — compensation\_package\_id, name (free-form), amount
- `BonusRecord` — employee\_id, amount, currency, reason, paid\_on
- `ContactInfo` — personal\_email, work\_email, phone, address
- `EmergencyContact` — name, relationship, phone

**Value Objects:**

- `EmployeeNumber` — tenant-scoped auto-increment string (e.g. EMP-00142)
- `EmploymentType` — Full-Time / Part-Time / Contract / Intern
- `EmployeeStatus` — Active / Probation / On-Leave / Resigned / Terminated

**Domain Events:**

- `EmployeeOnboarded` — triggers org chart update, attendance profile creation, leave balance initialisation
- `EmployeeTerminated` — triggers asset return request, access revocation
- `ProbationCompleted`

**Services:**

- `EmployeeSearchService` — full-text search with tenant isolation
- `OnboardingChecklist` — tracks onboarding task completion

---

### BC-06 — Recruitment

**Purpose:** Vacancy-driven hiring pipeline. A recruitment requisition is opened against a vacant Position (state = Vacant), not created ad hoc. The Position Template supplies the job description, required skills, certifications, grade, department, reporting line, and approval chain automatically — no duplication. On hire, the candidate is converted to an Employee and assigned to the Position, transitioning it from Vacant to Filled.

**Aggregates & Entities:**

- `RecruitmentRequisition` (aggregate root) — id, position\_id (FK to Position in BC-04c), position\_template\_id, department\_id, job\_title, job\_description (inherited from template, editable), required\_skills\[\] (inherited), grade\_id (inherited), reporting\_to\_position\_id (inherited), status (Draft | Open | OnHold | Closed | Cancelled), opened\_by, approved\_by, opened\_at, closed\_at
- `Candidate` — id, first\_name, last\_name, email, phone, source, resume\_storage\_path, created\_at
- `Application` — id, requisition\_id, candidate\_id, stage (Applied | Screening | Interview | Assessment | Offer | Hired | Rejected | Withdrawn), assigned\_to, notes\[\]
- `Interview` — application\_id, interviewer\_ids\[\], scheduled\_at, format (Phone | Video | InPerson | Technical), location\_or\_link, outcome (Proceed | Hold | Reject), notes
- `Offer` — application\_id, position\_id, salary\_offered, grade\_id, start\_date, expiry\_date, status (Pending | Accepted | Declined | Withdrawn)

**Value Objects:**

- `PipelineStage` — Applied / Screening / Interview / Assessment / Offer / Hired / Rejected
- `InterviewFormat` — Phone / Video / In-Person / Technical
- `CandidateSource` — Direct / Referral / LinkedIn / JobStreet / Agency

**Domain Events:**

- `ApplicationReceived`
- `CandidateAdvanced` — stage changed
- `OfferAccepted` — triggers `EmployeeOnboarded` in Employees BC
- `OfferRejected`

**Services:**

- `PipelineReportService` — stage conversion rates, time-to-hire
- `ResumeParserService` — extracts structured data from uploaded resumes (Phase 2)

---

### BC-07 — Attendance

**Purpose:** Records employee clock-in/out events, computes worked hours, detects late arrivals and overtime, supports shift and remote work patterns.

**Aggregates & Entities:**

- `AttendanceRecord` (aggregate root) — employee\_id, date, clock\_in\_time, clock\_out\_time, method, gps\_lat, gps\_lng, qr\_token, status
- `Shift` — id, name, start\_time, end\_time, days\_of\_week\[\], is\_flexible
- `ShiftAssignment` — employee\_id, shift\_id, effective\_from, effective\_to
- `OvertimeRequest` — employee\_id, date, hours, reason, approved\_by

**Value Objects:**

- `ClockMethod` — QR / GPS / QR+GPS / Manual
- `AttendanceStatus` — Present / Late / Absent / Leave / Holiday / Remote
- `WorkedHours` — regular\_hours + overtime\_hours

**Domain Events:**

- `EmployeeClockedIn`
- `EmployeeClockedOut`
- `LateArrivalDetected` — triggers manager notification
- `OvertimeApproved`
- `OfflineSyncCompleted` — bulk event from mobile after reconnection

**Services:**

- `ShiftRuleEngine` — evaluates clock times against shift definitions
- `QrTokenService` — generates and validates per-employee QR codes (rotating every 24 h)
- `GpsValidationService` — validates clock-in location against configured geofence

---

### BC-08 — Leave

**Purpose:** Manages leave types, employee balances, request/approval lifecycle, and integration with the attendance calendar.

**Aggregates & Entities:**

- `LeaveType` — id, name, days\_per\_year, is\_paid, carry\_over\_allowed, max\_carry\_over\_days, requires\_document
- `LeaveBalance` (aggregate root) — employee\_id, leave\_type\_id, year, entitled, taken, pending, remaining
- `LeaveRequest` — employee\_id, leave\_type\_id, start\_date, end\_date, days, reason, status, approved\_by, approved\_at

**Value Objects:**

- `LeaveStatus` — Pending / Approved / Rejected / Cancelled
- `LeavePeriod` — start\_date + end\_date + computed working\_days

**Domain Events:**

- `LeaveRequested` — triggers manager approval notification
- `LeaveApproved` — deducts balance; marks attendance as Leave
- `LeaveRejected`
- `BalanceAccrued` — scheduled annual accrual

**Services:**

- `WorkingDayCalculator` — excludes public holidays and weekends per tenant locale
- `LeaveBalanceAccrualService` — scheduled monthly/annual accrual

---

### BC-09 — Expenses

**Purpose:** Manages employee expense claims from submission through finance approval and reimbursement.

**Aggregates & Entities:**

- `ExpenseClaim` (aggregate root) — employee\_id, submitted\_at, total\_amount, currency, status
- `ExpenseItem` — claim\_id, category, description, amount, receipt\_url, merchant, expense\_date
- `ApprovalStep` — claim\_id, approver\_id (manager then finance), action, comment, actioned\_at

**Value Objects:**

- `ExpenseCategory` — Meals / Travel / Accommodation / Equipment / Training / Other
- `ClaimStatus` — Draft / Submitted / ManagerApproved / FinanceApproved / Paid / Rejected
- `Money` — amount + currency

**Domain Events:**

- `ExpenseSubmitted`
- `ExpenseManagerApproved` — advances to Finance queue
- `ExpenseFinanceApproved`
- `ExpensePaid`
- `ExpenseRejected`

**Services:**

- `ReceiptOcrService` — extracts amount/merchant from receipt images (Phase 2)
- `ExpenseExportService` — CSV/Excel export for payroll integration

---

### BC-10 — Performance

**Purpose:** Structures goal-setting, review cycles, feedback collection, and performance ratings.

**Aggregates & Entities:**

- `ReviewCycle` (aggregate root) — name, period\_start, period\_end, type, status
- `Goal` — employee\_id, cycle\_id, title, description, target, weight, progress, status
- `PerformanceReview` — employee\_id, reviewer\_id, cycle\_id, rating, comments, submitted\_at
- `Feedback` — from\_employee\_id, to\_employee\_id, type, body, cycle\_id

**Value Objects:**

- `ReviewType` — Annual / Mid-Year / Probation / 360
- `Rating` — 1–5 scale with label (Exceeds / Meets / Below)
- `GoalStatus` — Not Started / In Progress / Completed / Cancelled

**Domain Events:**

- `ReviewCycleOpened`
- `GoalSet`
- `ReviewSubmitted`
- `FeedbackRequested`

---

### BC-11 — Skills

**Purpose:** Maintains a company-wide skill taxonomy and each employee's rated competency profile.

**Aggregates & Entities:**

- `SkillCategory` — id, name
- `Skill` (aggregate root) — id, name, category\_id, description
- `EmployeeSkill` — employee\_id, skill\_id, proficiency\_level, assessed\_by, assessed\_at
- `SuccessionPlan` — position\_id, candidate\_employee\_ids\[\], readiness\_level

**Value Objects:**

- `ProficiencyLevel` — 1 Beginner / 2 Basic / 3 Intermediate / 4 Advanced / 5 Expert
- `ReadinessLevel` — Ready Now / 1–2 Years / 3+ Years

**Domain Events:**

- `SkillAssessed`
- `SkillGapIdentified` — when required skill not met by department average

---

### BC-12 — Training Compliance

**Purpose:** Tracks mandatory training requirements, employee completion records, certificate expiry, and compliance status — not an LMS.

**Aggregates & Entities:**

- `TrainingProvider` — id, name, contact, accreditation
- `Course` (aggregate root) — id, name, provider\_id, validity\_months, is\_mandatory, category
- `ComplianceRequirement` — course\_id, applies\_to (department\_ids\[\] or position\_ids\[\]), required\_by\_date
- `TrainingRecord` — employee\_id, course\_id, completed\_date, expiry\_date, certificate\_url, status
- `ComplianceAlert` — employee\_id, course\_id, alert\_type, scheduled\_at, sent\_at

**Value Objects:**

- `ComplianceStatus` — Compliant / Expiring Soon / Expired / Not Started
- `AlertType` — 90Day / 60Day / 30Day / Expired
- `CertificateRef` — MinIO object key + filename + mime\_type

**Domain Events:**

- `CertificateUploaded`
- `CertificateExpired`
- `CertificateExpiringSoon` — dispatched at 90/60/30 days
- `ComplianceRequirementBreach` — employee in non-compliant state

**Services:**

- `ComplianceMatrixService` — computes per-employee compliance status across all requirements
- `ExpiryAlertScheduler` — daily cron; dispatches alerts via Notifications BC

---

### BC-13 — Assets

**Purpose:** Tracks company-owned physical assets, their assignment to employees, and return lifecycle.

**Aggregates & Entities:**

- `Asset` (aggregate root) — id, asset\_tag, name, category, serial\_number, purchase\_date, purchase\_value, condition, status
- `AssetAssignment` — asset\_id, employee\_id, assigned\_date, return\_date, notes, condition\_at\_return

**Value Objects:**

- `AssetCategory` — Phone / Laptop / Vehicle / AccessCard / Tool / Other
- `AssetStatus` — Available / Assigned / Under Repair / Retired
- `AssetCondition` — New / Good / Fair / Damaged

**Domain Events:**

- `AssetAssigned`
- `AssetReturned`
- `AssetReturnRequested` — triggered by `EmployeeTerminated`

---

### BC-14 — Documents

**Purpose:** Secure document storage, categorisation, version tracking, and access control per tenant.

**Aggregates & Entities:**

- `Document` (aggregate root) — id, name, category, employee\_id (nullable), uploaded\_by, version, is\_employee\_visible, file\_ref
- `DocumentVersion` — document\_id, version\_number, file\_ref, uploaded\_at, uploaded\_by

**Value Objects:**

- `DocumentCategory` — Contract / Offer Letter / Certificate / Policy / ID / Other
- `FileRef` — MinIO bucket + object\_key + content\_type + size\_bytes

**Domain Events:**

- `DocumentUploaded`
- `DocumentVersionAdded`
- `DocumentExpired` — for time-bound documents (e.g. work permits)

---

### BC-15 — Announcements

**Purpose:** Company-wide or targeted communication — posts, read receipt tracking, scheduled publishing.

**Aggregates & Entities:**

- `Announcement` (aggregate root) — id, title, body, author\_id, target (All / Department / Team), publish\_at, expires\_at, status
- `ReadReceipt` — announcement\_id, employee\_id, read\_at

**Value Objects:**

- `AnnouncementTarget` — All / Department\[id\] / Team\[id\]
- `AnnouncementStatus` — Draft / Scheduled / Published / Expired

**Domain Events:**

- `AnnouncementPublished` — triggers push notification to targeted employees
- `AnnouncementRead`

---

### BC-16 — Helpdesk

**Purpose:** Internal ticketing for HR, IT, and Facilities requests submitted by employees.

**Aggregates & Entities:**

- `Ticket` (aggregate root) — id, employee\_id, category, subject, description, status, priority, assigned\_to, created\_at, resolved\_at
- `TicketComment` — ticket\_id, author\_id, body, created\_at

**Value Objects:**

- `TicketCategory` — HR / IT / Facilities
- `TicketStatus` — Open / In Progress / Resolved / Closed
- `Priority` — Low / Medium / High / Urgent

**Domain Events:**

- `TicketCreated` — triggers assignee notification
- `TicketResolved`
- `TicketCommentAdded`

---

### BC-17 — Notifications

**Purpose:** Abstracted multi-channel notification delivery consumed by all other contexts. No business logic — routing and delivery only.

**Aggregates & Entities:**

- `NotificationJob` — id, recipient\_employee\_id, channel, template\_key, payload, status, scheduled\_at, sent\_at, error

**Value Objects:**

- `NotificationChannel` — Push / Email / InApp
- `NotificationStatus` — Pending / Sent / Failed / Skipped

**Domain Events:**

- `NotificationSent`
- `NotificationFailed` — triggers retry queue

**Services:**

- `PushNotificationAdapter` — FCM (Android) + APNs (iOS)
- `EmailAdapter` — SMTP or transactional email provider
- `InAppNotificationStore` — persisted in-app notification feed per employee

---

## Approval Routing Architecture

### Overview

Every approval in Circlate is position-routed, not person-routed. When an employee submits a leave request, expense claim, or attendance exception, the platform does not ask "who is their manager?" — it asks "which position holds the authority to approve this action, and who currently occupies that position?"

This makes approval chains robust to personnel changes: if a manager leaves or transfers, the approval authority stays with the position and automatically transfers to whoever fills it next. It also enables clean delegation — when a position holder is away, authority delegates to a designated deputy position rather than a named individual.

Approval resolution follows three distinct authority types depending on the request domain:

### Three-Responsibility Model

Each position in Circlate carries up to three distinct types of responsibility. These are independent axes — a position may hold all three, two, or just one.

| Responsibility | Definition | Who holds it | Modules that use it |
| --- | --- | --- | --- |
| **Organisational Authority** | The business right to approve or reject actions on behalf of the organisation. Defined in Authority Profiles and attached to positions. | Line manager positions; designated approver positions | Leave, Expense Claims, Attendance Exceptions, Overtime, Recruitment offers |
| **Operational Responsibility** | Accountability for a work unit's output — a team, project, or operational group. Assigned through Work Structure membership with a supervisor role. | Work structure supervisors | Attendance, Timesheets, Task assignment, Performance reviews |
| **Financial Responsibility** | Stewardship of a cost centre or budget line. The position that owns the cost centre authorises spending against it. | Cost centre owners (typically department heads) | Expense Claims (over threshold), Procurement, Compensation changes |

**Why three separate axes?** In many organisations, the line manager, the operational lead, and the budget holder for a given employee are different people. For example, a software engineer on secondment to a cross-functional project might have:

- **Organisational Authority** approval from their home department manager (for leave)
- **Operational Responsibility** approval from the project lead (for timesheets)
- **Financial Responsibility** approval from the CFO's office (for expenses above BND 500)

Separating these allows Circlate to route each request to the correct authority without baking org-chart assumptions into individual modules.

### Approval Chain Resolution

When a request is submitted, the platform resolves the approver dynamically from the position graph. The resolution algorithm differs by request type:

**Leave Requests**

1. Identify the submitting employee's current position instance.
2. Traverse the organisational reporting line upward to find the nearest position that holds the `Approve Leave` authority profile entry.
3. Resolve the current occupant of that position — that person receives the approval task.
4. If no position in the reporting chain holds that authority, the request escalates to the HR Manager position for the tenant.

**Expense Claims**

1. Identify the cost centre associated with the submitting employee's primary work structure assignment.
2. Find the position designated as the owner of that cost centre.
3. If the claim amount exceeds the cost centre owner's approval threshold (configurable per position), the request cascades upward to the next cost centre in the hierarchy.
4. Claims with no cost centre assignment route to the Finance Manager position.

**Attendance Exceptions** (late arrivals, early departures, missed clock-ins)

1. Identify the submitting employee's active work structure membership and its supervisor position.
2. The work structure supervisor receives the correction request.
3. If the supervisor position is vacant, escalates to the HR Manager.

**Overtime Authorisation**

1. Resolved identically to Leave — the nearest position in the reporting line holding `Authorise Overtime` authority.

**Recruitment Offers**

1. The position with `Approve Hire` authority for the department that owns the vacancy.
2. Offers above a salary threshold additionally require the Finance Manager position to co-approve.

### Approval Delegation and Escalation

**Delegation** occurs when a position holder is on approved leave or officially absent. The position definition may designate a deputy position — when the primary holder is absent, Circlate automatically routes new approval tasks to the deputy's current occupant. Delegation is position-to-position, never person-to-person.

**Escalation** occurs on timeout. Each approval task carries a deadline (configurable per request type, defaulting to 3 business days). If the deadline passes without a decision:

1. The request escalates to the next position up the approval chain.
2. The original approver receives a notification that the request has been escalated away from them.
3. The escalation is recorded as a domain event and visible in the audit trail.

**Rules:**

- Maximum escalation depth: 3 hops. If no decision is reached after 3 escalations, the request is flagged for HR Manager manual resolution.
- Delegation chains do not escalate — a delegated task returns to the original approver chain on timeout, not the delegate's chain.
- An approver cannot approve their own requests. If resolution returns the request to the submitter's own position, it escalates one level immediately.
- All delegation and escalation events are immutable audit records.

### Approval Domain Events

All state transitions in the approval lifecycle emit domain events. These are consumed by BC-17 Notifications (to push alerts) and by BC-16 Helpdesk (for SLA tracking on HR tickets).

| Event | Payload | Consumers |
| --- | --- | --- |
| `ApprovalRequested` | requestId, requestType, submitterId, resolvedApproverId, positionId, deadline | Notifications, Audit Log |
| `ApprovalGranted` | requestId, approverId, positionId, decisionAt, notes | Requesting module (Leave/Expense/Attendance), Notifications, Audit Log |
| `ApprovalRejected` | requestId, approverId, positionId, decisionAt, reason | Requesting module, Notifications, Audit Log |
| `ApprovalEscalated` | requestId, fromPositionId, toPositionId, escalatedAt, reason | Notifications, HR Dashboard |
| `ApprovalDelegated` | requestId, fromPositionId, toDeputyPositionId, delegatedAt | Notifications, Audit Log |
| `ApprovalWithdrawn` | requestId, withdrawnBy, withdrawnAt | Requesting module, Notifications, Audit Log |
| `ApprovalDeadlineMissed` | requestId, approverId, positionId, deadlineAt | Notifications, Escalation trigger |

**Audit log requirement:** Every approval event is written to an immutable append-only audit table in the tenant database. The audit record captures: tenant ID, request ID, event type, actor position ID, actor person ID, timestamp (UTC), and a snapshot of the request state at that moment. Audit records may never be updated or deleted — they satisfy Brunei's Employment Order record-keeping obligations.

---

## Architecture Gap Review

### Missing Domains

The following cross-cutting concerns are referenced in the spec but lack a dedicated Bounded Context definition:

**BC-18 — Compensation (Recommended — add to Capability layer)** Salary packages, allowances, bonus records, and commission structures live on the employee record in the current build, but as a standalone HR concern they warrant their own BC. Without a BC boundary, compensation data has no defined aggregate root, no domain events, and no clear ownership. Recommended: elevate to BC-18 Compensation with its own aggregate (`CompensationPackage`), domain events (`CompensationUpdated`, `BonusRecorded`), and read model for the payroll export.

**BC-19 — Reports (Recommended — add to Capability layer)** The payroll export and future HR analytics have no BC home. Currently, report queries reach directly into multiple other BCs' data stores. Recommended: introduce BC-19 Reports as a read-side-only BC that materialises cross-domain views (attendance + leave + expenses + compensation) for export and dashboards. This keeps read-model concerns separate from the write-side aggregates.

**Audit Log (Cross-cutting — not a BC, but needs explicit infrastructure)** Approval events, compensation changes, and sensitive data access should write to an immutable audit store. This is not a BC — it is infrastructure. Recommended: add an `AuditLog` table per tenant database, written to via domain event handlers, never updated or deleted.

**Public Holiday Calendar (Missing — needed by Leave and Attendance)** Leave day counting and attendance shift patterns depend on public holidays. Brunei has 15–17 public holidays per year (some variable dates like Hari Raya). No BC or configuration surface exists for this. Recommended: add a `PublicHolidayCalendar` aggregate to BC-04 Organisation (it is org-wide configuration) with per-year calendars configurable by HR.

**Approval Workflow Engine (Architecture concern — not a separate BC)** Approval routing logic (described in this document) needs a home in the codebase. Recommended: implement as a domain service within the requesting module (Leave, Expense, etc.) that delegates resolution to the Position Management BC. Do not create a separate Workflow BC — that creates circular dependencies.

### Scalability Concerns

**Position graph traversal depth** Approval resolution walks the organisational reporting line upward. In a flat SME this is 2–3 hops. In a larger organisation (100+ positions) or a poorly maintained org chart, this could be 8–10 hops. Each hop is a database read. Recommended: cache the resolved approval chain per position (invalidated when any position in the chain changes), and enforce a maximum traversal depth of 10 with a hard fallback to HR Manager.

**Database-per-tenant connection counts** With PgBouncer in transaction-pooling mode, each tenant's database is a separate pool. At 50 tenants × 5 connections each = 250 connections baseline — manageable. At 500 tenants it becomes a PgBouncer configuration and monitoring concern. This is noted in Phase 3 and is not a Phase 1/2 risk, but the connection pool budget should be reviewed before launch.

**Notification fan-out for large announcements** BC-15 Announcements can target all employees in an organisation. For a 500-person company, sending a push notification to 500 devices in a single request will time out. Recommended: dispatch announcement notifications through a background job queue (e.g., Hangfire or a Redis-backed queue) rather than synchronously in the HTTP request.

**Cost allocation sum validation** Work structure assignments carry allocation percentages that must sum to 100% across all active assignments for one employee. This constraint spans multiple aggregate instances (one per work structure). It cannot be enforced inside a single aggregate transaction. Recommended: enforce as an eventual consistency check via a domain event handler on `WorkStructureAssignmentChanged`, and surface violations as a warning in the HR dashboard rather than a hard block.

**Leave balance accrual at scale** If leave balances are computed by summing time-entry records since employment start, queries will degrade for long-tenured employees. Recommended: use a snapshot pattern — store a balance checkpoint at the end of each leave year and compute the running total from the checkpoint forward.

### Workflow Gaps

**Leave balance accrual and entitlement configuration** BC-08 Leave defines leave types (Annual, Sick, Unpaid, Other) but does not specify how entitlement amounts are configured or how balances accrue. Brunei Employment Order requirements (see Compliance Gaps) mandate specific entitlements tied to tenure. Missing: a `LeavePolicy` aggregate per tenant that defines entitlement rules per employment type and tenure band, and an accrual engine that computes balances.

**Probation period** Employees in probation typically have restricted leave entitlements and different notice periods. The Employee aggregate has no probation concept. Missing: `ProbationEndDate` on the Employment record, and conditional leave entitlement rules during probation.

**Employee offboarding workflow** There is no offboarding process defined. When an employee resigns or is terminated: position instance must be vacated, work structure assignments must be ended, documents must be archived, leave balances must be computed for final payout, and assets must be returned. Missing: an `OffboardingChecklist` aggregate or a structured offboarding workflow in BC-05 Employees.

**Position succession on vacancy** When a position holder leaves, the position is vacant. Approval chains pointing to that position break. Missing: a `PositionVacancyCreated` domain event handler that immediately escalates all pending approvals from the vacated position, and triggers a recruitment vacancy if Workforce Establishment requires it.

**Bulk employee import** For SMEs migrating to Circlate from spreadsheets, importing 50–200 employees manually is not viable. Missing: a CSV/Excel import endpoint in BC-05 that maps columns to the Employee aggregate and validates against the existing org structure.

**Public holiday calendar** Absent from the domain model (see Missing Domains). Without it, leave day counting cannot exclude public holidays, and attendance patterns cannot recognise public holiday shifts.

**Employment type distinctions** The spec mentions full-time, part-time, and contract employees but does not model how they differ in terms of leave entitlement, working hours, or attendance rules. Missing: `EmploymentType` configuration aggregate that parameterises these rules per tenant.

### Security Gaps

**Multi-tenancy enforcement at the application layer** Database-per-tenant provides isolation at the storage layer, but the application layer must ensure it always connects to the correct tenant database for the authenticated user's tenant. If `TenantId` resolution from the JWT is misconfigured, one tenant could read another's data. Required: a middleware-enforced tenant context that selects the correct connection string on every request, with integration tests that verify cross-tenant data cannot be accessed.

**Compensation data sensitivity** Salary, allowances, bonus records, and commission values are sensitive HR data that most employees must not see. The current design has no field-level access control — only page-level gating with `[HR Only]` badges. Required: compensation endpoints must enforce that only positions holding the `View Compensation` or `Manage Compensation` authority profile entries can call them. Compensation data must never be included in general employee list responses.

**Document access control** BC-14 Documents has access control listed as a feature but the rules are not specified. An employee must be able to see their own documents but not another employee's. HR can see all. Managers may need to see their direct reports' employment documents. Required: define document visibility rules in BC-14 as explicit policy (not implicit) tied to authority profiles.

**RBAC derivation from authority profiles** The spec says technical permissions are derived from authority profiles, but the derivation mechanism is not defined. How does `Approve Leave` authority translate to an allowed API endpoint? Options: (a) explicit permission map in the codebase, (b) claims injected into the JWT at login, (c) checked at the domain service layer. Option (c) is recommended — keep permission checks inside the domain, close to the invariant being protected. This needs to be documented before Phase 2 implementation.

**API rate limiting and abuse prevention** No rate limiting is mentioned. The `/api/attendance/clock-in` endpoint in particular could be abused (or accidentally hammered by a buggy mobile client). Required: add rate limiting per tenant per endpoint, implemented at the API gateway or ASP.NET Core middleware layer.

**Audit log access** The audit log contains sensitive records (who approved whose expense, compensation history). It must be readable only by HR Manager and Tenant Admin positions. No access rules are currently defined for it.

### Reporting Gaps

**No dedicated Reports BC** The spec has 20 BCs, none of which owns the reporting domain. Reports sit in Phase 4 Module descriptions and are described feature-by-feature but have no aggregate, no domain events, and no data model. Without a BC boundary, report queries will spread ad-hoc across modules. Recommended: add BC-19 Reports (see Missing Domains) as a read-side BC with materialised views updated by domain event consumers.

**Only one report defined end-to-end (Payroll Export)** The codebase has the payroll export query, but all other reports in Phase 4 are aspirational features with no data model. Missing reports that HR/management will need on day one:

- Leave balance summary (per employee, per leave type, current year)
- Headcount by department/position (live and over time)
- Attendance summary (days worked, late arrivals, absences per month)
- Expense summary by department and category
- Recruitment pipeline status (open vacancies, candidates per stage)

**No scheduled / automated report delivery** Reports in the current design are on-demand only. SME payroll processors often need monthly reports emailed automatically. Missing: a scheduled report delivery feature (email CSV on a cron schedule) in BC-19.

**No custom report builder for Phase 1** This is explicitly out of scope for Phase 1 — noted here as a known gap to address in a later phase.

### UX Gaps

**Employee self-service boundary is undefined** The spec lists HR-only features but does not define what employees can do for themselves. In a typical HRMS, employees can: view their own payslips (out of scope), submit leave, submit expenses, view their own attendance, update personal contact info, and download their own documents. The boundary between employee self-service and HR-managed actions needs an explicit policy, ideally expressed as authority profile entries.

**Mobile app scope not tied to Phase plan** FR-19 mentions a Flutter mobile app for clock-in and notifications. This appears in Phase 4 Module descriptions, but the mobile-specific API endpoints, offline sync protocol, and device registration model are not designed. If mobile is in scope for the initial launch, these need a dedicated design pass.

**Bulk approval actions** During peak leave periods (e.g., Hari Raya), a manager may receive 20+ leave requests in one day. Approving them one at a time is friction. Missing: bulk approve/reject action on the approvals dashboard.

**Notification preference management** Employees should be able to choose how they receive notifications (email, in-app, push). BC-17 Notifications is the abstracted delivery layer, but there is no `NotificationPreference` model per employee. Missing: preference settings in BC-05 Employees that BC-17 reads before dispatching.

**Dashboard scope undefined** Phase 4 Module 1 mentions a dashboard but only for employees. HR managers need a different dashboard: pending approvals, headcount summary, upcoming leave, expense queue. No design exists for the manager dashboard vs employee dashboard distinction.

### Compliance Gaps

**Brunei Employment Order 2009 — Leave Entitlements** The Employment Order mandates minimum leave entitlements that Circlate must enforce or at least make configurable without workarounds:

- Annual leave: 7 days (< 2 years service), 8 days (2–5 years), 10 days (> 5 years)
- Sick leave: 14 days (without hospitalisation) or up to 60 days (with hospitalisation)
- Maternity leave: 15 weeks (for employees with ≥ 180 days service)
- Paternity leave: not mandated by law but common practice — Circlate should allow configuration

Currently BC-08 Leave has no `LeavePolicy` aggregate and cannot enforce or validate these rules. Required before launch.

**Brunei Personal Data Protection Order (PDPO) 2021** Employee personal data has retention and deletion requirements. Key implications:

- Employees may request deletion of their personal data after leaving
- Data must not be held longer than necessary for its purpose
- Cross-border data transfer restrictions apply (relevant for multi-region hosting)

Currently no data retention policy model exists. Required: a `DataRetentionPolicy` configuration per tenant, and a soft-delete / data-anonymisation workflow for departed employees.

**TAP and SCP employer contribution records** Payroll calculation is out of scope (spec §9 Assumptions), but Circlate exports data used by payroll processors who compute TAP (Tabung Amanah Pekerja) and SCP (Supplemental Contributory Pension) contributions. The payroll export format must include the fields those processors need: employment type, gross salary base, employment start date. Currently the export only includes attendance and expenses — salary data is missing.

**Brunei Labour Department audit reports** Employers must maintain records demonstrating compliance with the Employment Order (working hours, overtime, leave balances, accident records). No export format for a Labour Department audit is defined. Recommended: add a "Compliance Report" export to BC-19 Reports.

**IC (Identity Card) number storage** IC numbers are government-issued national identifiers — equivalent to a national ID number. Storing them without encryption or masking is a PDPO concern. Required: IC numbers must be stored encrypted at rest (or masked in display) and only accessible to HR Manager positions.

### Implementation Risks

**Foundation BCs must be built before all Capability BCs** Every Capability BC (Employees, Recruitment, Leave, etc.) depends on BC-04 Organisation, BC-04b Authority Profiles, BC-04c Position Management, and BC-04d Work Structures being in production first. The current codebase has `Employee.Department` and `Employee.Position` as plain strings — not entity relationships. This technical debt must be cleared before any approval routing or authority-based access control can function. Risk: **High**. Mitigation: dedicate the next sprint to building the Foundation BCs and migrating the string fields to entity foreign keys.

**Position graph as a new data structure in an RDBMS** Organisational hierarchies stored in a relational database require either adjacency lists (simple but slow for deep traversal) or closure tables / materialised path (fast but complex to maintain). The spec does not prescribe which. Risk: **Medium**. Recommendation: use a closure table pattern for `PositionReportingRelationship` — it makes ancestor/descendant queries a single join, essential for approval chain resolution.

**20 BCs across database-per-tenant EF Core migrations** Every time a BC adds or changes a table, a migration must run against every tenant's database. At 50+ tenants, running migrations synchronously on startup (current approach) will cause very long cold starts. Risk: **Medium**. Mitigation: introduce a migration runner service that runs tenant migrations asynchronously in a background job on deployment, with per-tenant migration state tracked in the platform database.

**Authority Profile derivation into technical permissions** The design calls for technical permissions to be derived from authority profiles, but the derivation mechanism is undefined. If this is deferred, Phase 2 feature development will use ad-hoc role checks that will not be aligned with the authority model, requiring a painful retrofit. Risk: **High**. Mitigation: define the permission derivation contract before writing any BC-level endpoint — even a simple mapping table in Phase 2 is better than none.

**Cost allocation sum-to-100% enforcement across aggregates** This constraint spans multiple work structure assignments and cannot be transactionally enforced in a single aggregate. If not addressed, the cost allocation data will silently drift and financial reporting will be wrong. Risk: **Medium**. Mitigation: use the eventual consistency check described in Scalability Concerns, plus a nightly validation job that alerts HR when employee allocations are inconsistent.

**Compensation data in the current build is not in a BC** Salary and allowance data was added to the Employee endpoint in the current prototype. Without a Compensation BC, there is no domain boundary — changes to compensation logic will bleed into the Employee aggregate. Risk: **Low for now, High at scale**. Mitigation: add BC-18 Compensation before Phase 2 features that depend on compensation data (reports, offer letters in recruitment, etc.).

---

## Foundation Architecture Package

### Foundation Domain Overview

The Foundation Architecture Package defines the seven platform-level bounded contexts that every operational module in Circlate depends on. No capability module (Attendance, Leave, Expenses, Recruitment, Performance, etc.) may implement its own organisational structure, authority model, approval routing, or policy engine. All such concerns are delegated exclusively to the Foundation layer.

**What makes a domain 'foundational'?** A domain is foundational if removing it would cause multiple capability BCs to break simultaneously, or if it owns a cross-cutting concern that — if duplicated per module — would create irreconcilable inconsistency. The seven Foundation BCs each meet this test:

| BC | Concern Owned | If absent |
| --- | --- | --- |
| BC-01 Identity | Who the system is talking to | No authentication, no tenant isolation |
| BC-02 Organisation | Where in the company an employee sits | No department/cost centre resolution |
| BC-03 Authority & Delegation | What a position is allowed to do | No approval routing, no access control |
| BC-04 Position Management | The organisational role an employee occupies | No authority inheritance, no headcount |
| BC-05 Work Structures | The operational group an employee works within | No project allocation, no matrix reporting |
| BC-06 Approval Routing | How approval decisions travel to the right person | Every module implements its own ad-hoc routing |
| BC-07 Rules & Policy Engine | Configurable business logic for every module | Rules hardcoded, untestable, non-configurable |

**Mandatory Build Order** The Foundation BCs must be built in dependency order. A BC may not be deployed until all its dependencies are live:

```
BC-01 Identity
  └── BC-02 Organisation  (needs tenant identity)
        └── BC-04 Position Management  (needs org structure)
              └── BC-03 Authority & Delegation  (needs position definitions)
                    └── BC-06 Approval Routing  (needs authority + positions)
  └── BC-05 Work Structures  (needs org + positions)
  └── BC-07 Rules & Policy Engine  (can be built in parallel after BC-01)
```

**Core Design Principles**

1. **Positions own authority; employees inherit it.** An employee's ability to approve a leave request is not a property of the employee — it is a property of the position they currently occupy. If they move to a different position, their authority changes automatically on the next request.
2. **Business authority precedes technical permissions.** The business defines "Approve Leave" as a human-readable authority entry. The technical layer derives `leave:approve` from that. Never the reverse.
3. **Work structures describe execution; positions describe authority.** The project lead position on a work structure holds supervisory authority. The work structure membership itself does not grant that authority — the position does.
4. **Policy rules are data, not code.** Every configurable business rule (leave accrual rates, expense thresholds, escalation timeouts) lives in BC-07 as a versioned policy definition. No capability BC may hardcode business rules.
5. **Approval routing is position-to-position, never person-to-person.** Approvals are assigned to the position, resolved to the current occupant at the moment of assignment. If the occupant changes mid-flow, the new occupant receives the pending task.

**Foundation-to-Capability Dependency Contract** Every capability BC receives the following from the Foundation layer via JWT claims and read-only query APIs — it must never query Foundation tables directly:

- `tenantId` — from BC-01 (JWT claim)
- `userId`, `employeeId` — from BC-01 (JWT claim)
- `currentPositionInstanceId` — from BC-04 (JWT claim, refreshed on login)
- `authorityCapabilities` — from BC-03 (JWT claim, list of capability strings)
- `primaryWorkStructureId` — from BC-05 (JWT claim)
- `departmentId`, `costCentreId` — from BC-02 (resolved via position → department on login)

Capability BCs use these claims for access control and routing. They never traverse the org hierarchy themselves.

---

### BC-01 — Identity

**Purpose:** Owns all authentication, identity verification, and tenant-scoped account management. BC-01 is the only BC that integrates with Keycloak. All other BCs receive identity through JWT claims only — they must never query identity tables directly. BC-01 also manages Service Accounts for machine-to-machine API calls.

#### Aggregates

**User** (Aggregate Root)

- `userId` Guid — surrogate PK, mirrored from Keycloak subject claim
- `tenantId` Guid — the tenant this account belongs to
- `email` Email (VO) — unique per tenant
- `displayName` string
- `status` UserStatus enum (PendingVerification / Active / Suspended / Deactivated)
- `passwordChangedAt` DateTime UTC
- `lastLoginAt` DateTime UTC (nullable)
- `employeeId` Guid (nullable) — link to BC-05 Employee aggregate once onboarded
- Entities: `MfaDevice[]`, `ActiveSession[]`

**ServiceAccount** (Aggregate Root)

- `serviceAccountId` Guid
- `tenantId` Guid
- `name` string — human-readable label
- `scopes` string\[\] — e.g. `["attendance:write", "reports:read"]`
- `status` ServiceAccountStatus (Active / Revoked)
- Entities: `ApiKey[]` — each key stores hash + prefix only; plain text shown once on creation

**TenantMembership** (Aggregate Root)

- `membershipId` Guid
- `userId` Guid
- `tenantId` Guid
- `role` PlatformRole enum (TenantAdmin / HRManager / Employee / ReadOnly)
- `status` MembershipStatus (Active / Suspended)
- `invitedAt`, `acceptedAt` DateTime UTC

#### Entities

**MfaDevice**

- `deviceId` Guid, `userId` Guid, `type` MfaType (TOTP / SMS / Email), `deviceLabel` string, `enrolledAt`, `lastUsedAt`, `isDefault` bool

**ActiveSession**

- `sessionId` Guid, `userId` Guid, `deviceType` (Web / Mobile / API), `refreshTokenHash` string, `issuedAt`, `expiresAt`, `revokedAt` (nullable)

**ApiKey**

- `keyId` Guid, `serviceAccountId` Guid, `keyPrefix` string (8 chars — shown to user), `keyHash` string (SHA-256), `createdAt`, `expiresAt` (nullable), `lastUsedAt`, `revokedAt` (nullable)

#### Value Objects

- **Email** — normalised (lowercase, trimmed), RFC 5322 validated
- **HashedPassword** — Argon2id hash, never stored in plaintext
- **JwtClaimsSet** — sub (userId), tid (tenantId), eid (employeeId), pid (positionInstanceId), caps (capability list), exp, iat — read-only after minting
- **TotpSecret** — base32 encoded seed, AES-256 encrypted at rest

#### Domain Events

| Event | Payload | Consumers |
| --- | --- | --- |
| `UserCreated` | userId, tenantId, email | BC-02 (init employee onboarding hook), Notifications |
| `UserSuspended` | userId, tenantId, reason, suspendedBy | Notifications, Audit Log |
| `UserReactivated` | userId, tenantId, reactivatedBy | Notifications, Audit Log |
| `PasswordChanged` | userId, tenantId, changedAt | Audit Log, Notifications |
| `MfaDeviceEnrolled` | userId, deviceId, deviceType | Audit Log |
| `MfaDeviceRevoked` | userId, deviceId | Audit Log |
| `SessionRevoked` | userId, sessionId, revokedAt, reason | Audit Log |
| `TenantMembershipCreated` | userId, tenantId, role | BC-05 Employees |
| `ApiKeyIssued` | serviceAccountId, keyId, keyPrefix, scopes | Audit Log |
| `ApiKeyRevoked` | serviceAccountId, keyId, revokedAt | Audit Log |

#### Authentication Flows

**Standard Password (Web)**

1. `POST /auth/token` with `grant_type=password`, `username`, `password`, `tenant_id`
2. Keycloak validates credentials in the tenant realm
3. Returns `access_token` (JWT, 15-minute TTL), `refresh_token` (7-day sliding)
4. Access token carries full JwtClaimsSet including `caps` and `pid`

**PKCE Flow (Mobile)**

1. Mobile app initiates PKCE: generates `code_verifier`, sends `code_challenge`
2. `GET /auth/authorize?response_type=code&code_challenge=...` → Keycloak login screen
3. Keycloak redirects to app deep-link with `authorization_code`
4. `POST /auth/token` with `grant_type=authorization_code`, `code_verifier` → tokens
5. Mobile stores refresh token in OS secure enclave (Keychain / Android Keystore)

**MFA Challenge**

1. After password auth, if MFA is enrolled and required: response includes `mfa_required: true`, `mfa_session_token`
2. `POST /auth/mfa/verify` with `mfa_session_token`, `code` (6-digit TOTP)
3. On success: full access + refresh tokens issued

**Service Account (M2M)**

1. `POST /auth/token/service` with `client_id` (serviceAccountId), `client_secret` (ApiKey plain text — only on creation)
2. Returns short-lived access token (1-hour TTL), no refresh
3. JWT carries `scope` claim, no `pid` or `eid`

**Token Refresh**

1. `POST /auth/refresh` with `refresh_token`
2. Keycloak validates non-revoked session, issues new access token
3. If refresh token within final 24 hours of TTL: also issues new refresh token (sliding)

#### API Contracts

`POST /auth/token` — Authenticate user Request: `{ grant_type, username, password, tenant_id }` Response 200: `{ access_token, refresh_token, token_type: "Bearer", expires_in: 900 }` Response 401: `{ error: "invalid_credentials" }` Response 403: `{ error: "account_suspended" }`

`POST /auth/refresh` — Refresh access token Request: `{ refresh_token }` Response 200: `{ access_token, refresh_token?, expires_in }` Response 401: `{ error: "token_expired" | "token_revoked" }`

`POST /auth/token/service` — Service account token Request: `{ client_id, client_secret }` Response 200: `{ access_token, token_type: "Bearer", expires_in: 3600, scope }`

`POST /auth/mfa/enrol` — Enrol TOTP device — requires auth Request: `{ device_label }` Response 200: `{ device_id, totp_uri, qr_code_data_url }` (secret not re-exposed after this)

`POST /auth/mfa/verify` — Verify MFA challenge Request: `{ mfa_session_token, code }` Response 200: full token response Response 401: `{ error: "invalid_code" | "code_expired" }`

`POST /auth/sessions/revoke` — Revoke all sessions (logout everywhere) — requires auth Response 204

`GET /api/users` — List tenant users — requires `users:read` `POST /api/users` — Create user — requires `users:write` `GET /api/users/{id}` — Get user — requires `users:read` `PATCH /api/users/{id}` — Update user (name, status) — requires `users:write` `POST /api/users/{id}/suspend` — Suspend — requires `users:manage` `POST /api/users/{id}/reactivate` — Reactivate — requires `users:manage`

`GET /api/service-accounts` — List — requires `service-accounts:read` `POST /api/service-accounts` — Create — requires `service-accounts:write` `POST /api/service-accounts/{id}/keys` — Issue API key — requires `service-accounts:write` `DELETE /api/service-accounts/{id}/keys/{keyId}` — Revoke key — requires `service-accounts:write`

#### Security Model

- **Keycloak configuration:** One Keycloak realm per tenant (isolates user stores, tokens, login pages). The platform database maps `tenantId → realmName`.
- **JWT algorithm:** RS256. Public keys fetched from Keycloak JWKS endpoint on startup and cached with 5-minute TTL.
- **Token validation:** Every API request validates signature, `exp`, `iss` (must match tenant realm), and `tid` claim (must match route parameter if present).
- **Refresh token storage:** Server-side session record in BC-01 database. If session record is revoked, refresh token is rejected even if not expired.
- **API key storage:** Plain text shown once on creation. Only SHA-256 hash stored. No recovery path — lost key must be revoked and reissued.
- **Brute-force protection:** Keycloak per-realm lockout policy: 5 failed attempts → 5-minute lockout. Progressive doubling up to 24 hours.
- **MFA requirement:** Configurable per tenant. Tenants may require MFA for all users, HR-only users, or no users. HR Manager may always self-enrol MFA regardless of tenant policy.

---

### BC-02 — Organisation

**Purpose:** Owns the structural hierarchy of a company — the legal entity, its business units, departments, cost centres, regions, and public holiday calendars. BC-02 is the structural backbone. BC-04 (positions) and BC-05 (work structures) hang off BC-02 nodes. No capability BC may define its own department or cost centre structure.

#### Aggregates

**Organisation** (Aggregate Root)

- `organisationId` Guid
- `tenantId` Guid
- `legalName` string
- `tradingName` string (nullable)
- `registrationNumber` string
- `countryCode` string (ISO 3166-1 alpha-2, e.g. `BN`)
- `defaultCurrency` string (ISO 4217, e.g. `BND`)
- `timezone` string (IANA, e.g. `Asia/Brunei`)
- `fiscalYearStartMonth` int (1–12)
- `status` OrgStatus (Active / Suspended / Dissolved)

**BusinessUnit** (Aggregate Root)

- `businessUnitId` Guid
- `tenantId` Guid
- `organisationId` Guid
- `parentBusinessUnitId` Guid (nullable — root business unit has null)
- `name` string
- `code` string (unique per tenant, e.g. `NORTH-REGION`)
- `type` BusinessUnitType enum (Division / Region / Branch / Site / Subsidiary)
- `countryCode` string (nullable — override for subsidiaries in other countries)
- `status` ActiveStatus

**Department** (Aggregate Root)

- `departmentId` Guid
- `tenantId` Guid
- `businessUnitId` Guid
- `name` string
- `code` string (unique per tenant, e.g. `HR`, `OPS-NORTH`)
- `headPositionId` Guid (nullable — FK to PositionInstance in BC-04; set once Position BC is live)
- `costCentreId` Guid (nullable — FK to CostCentre)
- `status` ActiveStatus

**CostCentre** (Aggregate Root)

- `costCentreId` Guid
- `tenantId` Guid
- `code` string (unique per tenant, e.g. `CC-OPS-01`)
- `name` string
- `parentCostCentreId` Guid (nullable — allows nested cost centre hierarchies)
- `ownerPositionId` Guid (nullable — the position responsible for this cost centre's budget)
- `approvalThreshold` decimal (nullable — expense amounts above this require escalation; null = no threshold)
- `currency` string (ISO 4217)
- `status` ActiveStatus

**PublicHolidayCalendar** (Aggregate Root)

- `calendarId` Guid
- `tenantId` Guid
- `year` int
- `countryCode` string
- `entries` PublicHolidayEntry\[\] (entities)
- `status` CalendarStatus (Draft / Published)

**PublicHolidayEntry** (Entity)

- `entryId` Guid
- `calendarId` Guid
- `date` DateOnly
- `name` string
- `type` HolidayType (National / Religious / Regional / Substitute)
- `applicableRegions` string\[\] (nullable — empty means all regions)

#### Value Objects

- **HierarchyPath** — string encoded materialised path (e.g. `/org-001/bu-002/dept-004/`) used for ancestor/descendant queries without recursive CTEs
- **CostCentreCode** — validated format: `CC-[A-Z0-9]{2,8}`, uppercase
- **DepartmentCode** — validated format: `[A-Z]{2,10}(-[A-Z0-9]{1,6})?`

#### Domain Events

| Event | Payload | Consumers |
| --- | --- | --- |
| `OrganisationCreated` | organisationId, tenantId, legalName, countryCode | BC-01 (init tenant config) |
| `BusinessUnitCreated` | businessUnitId, tenantId, name, type, parentId | BC-04 Position Management |
| `BusinessUnitMoved` | businessUnitId, oldParentId, newParentId | BC-04, BC-05, Audit Log |
| `DepartmentCreated` | departmentId, tenantId, businessUnitId, name | BC-04, Reports |
| `DepartmentHeadAssigned` | departmentId, positionInstanceId | Notifications |
| `CostCentreCreated` | costCentreId, tenantId, code, ownerPositionId | BC-06 Approval Routing |
| `CostCentreOwnerChanged` | costCentreId, oldOwnerPositionId, newOwnerPositionId | BC-06 (invalidate cached routing) |
| `PublicHolidayCalendarPublished` | calendarId, tenantId, year, entryCount | BC-08 Leave, BC-07 Attendance, Notifications |

#### Organisational Hierarchy Examples

**Small SME (20 employees — e.g. accounting firm)**

```
Organisation: Brunei Accounting Partners Sdn Bhd
  └── Department: Audit & Assurance      (CC-AUDIT)
  └── Department: Tax Advisory           (CC-TAX)
  └── Department: Corporate Secretarial  (CC-CORP)
  └── Department: Administration          (CC-ADMIN)
```

Single Business Unit (the whole firm). Four departments. Four cost centres. No regional structure.

**Construction Company (120 employees)**

```
Organisation: Buildright Construction Sdn Bhd
  └── BusinessUnit: Head Office (HO)       [Division]
        └── Department: Finance & Admin    (CC-HO-FIN)
        └── Department: HR & Compliance    (CC-HO-HR)
        └── Department: Procurement        (CC-HO-PROC)
  └── BusinessUnit: Project Division        [Division]
        └── BusinessUnit: Site Muara       [Site]
              └── Department: Civil Works  (CC-MUARA-CIV)
              └── Department: M&E Works    (CC-MUARA-ME)
        └── BusinessUnit: Site Tutong      [Site]
              └── Department: Civil Works  (CC-TUTONG-CIV)
  └── BusinessUnit: Equipment & Logistics  [Division]
        └── Department: Fleet Management   (CC-FLEET)
        └── Department: Warehousing        (CC-WH)
```

Projects become Work Structures in BC-05; sites are Business Units in BC-02.

**Security Company (350 employees)**

```
Organisation: Guardian Force Sdn Bhd
  └── BusinessUnit: Corporate              [Division]
        └── Department: Management         (CC-CORP-MGT)
        └── Department: HR & Training      (CC-CORP-HR)
  └── BusinessUnit: Brunei-Muara Region   [Region]
        └── Department: Static Guarding    (CC-BM-STATIC)
        └── Department: Mobile Patrol      (CC-BM-MOBILE)
  └── BusinessUnit: Belait Region          [Region]
        └── Department: Static Guarding    (CC-BE-STATIC)
  └── BusinessUnit: Tutong Region          [Region]
        └── Department: Static Guarding    (CC-TU-STATIC)
  └── BusinessUnit: Temburong Region       [Region]
        └── Department: Static Guarding    (CC-TE-STATIC)
```

Security shifts are Work Structures (Sites with shift patterns). Officers are assigned to Site work structures for operational purposes, to their Region department for HR purposes.

**Engineering Consultancy (60 employees — matrix organisation)**

```
Organisation: Pacific Engineering Consultants Sdn Bhd
  └── BusinessUnit: Corporate              [Division]
        └── Department: Finance & Admin    (CC-CORP)
  └── BusinessUnit: Technical Divisions   [Division]
        └── Department: Civil Engineering  (CC-CIVIL)
        └── Department: Structural Eng     (CC-STRUCT)
        └── Department: M&E Engineering    (CC-ME)
        └── Department: Environmental      (CC-ENV)
```

Engineers are permanently assigned to a Technical Department (home department for HR). Projects are Work Structures in BC-05 — an engineer may be allocated 60% to Project Alpha (Civil) and 40% to Project Bravo (Structural) simultaneously. The department owns the headcount; the project borrows the resource.

#### API Contracts

`GET /api/organisations` — Get organisation (one per tenant) — requires `organisation:read` `PATCH /api/organisations` — Update org details — requires `organisation:write`

`GET /api/business-units` — List (tree structure) — requires `organisation:read` `POST /api/business-units` — Create — requires `organisation:write` `GET /api/business-units/{id}` — Get with children — requires `organisation:read` `PATCH /api/business-units/{id}` — Update — requires `organisation:write` `POST /api/business-units/{id}/move` — Move to new parent — requires `organisation:write` Request: `{ newParentBusinessUnitId }`

`GET /api/departments` — List — requires `organisation:read` `POST /api/departments` — Create — requires `organisation:write` `PATCH /api/departments/{id}` — Update — requires `organisation:write`

`GET /api/cost-centres` — List (tree structure) — requires `organisation:read` `POST /api/cost-centres` — Create — requires `organisation:write` `PATCH /api/cost-centres/{id}` — Update — requires `organisation:write`

`GET /api/public-holidays/{year}` — Get calendar for year — requires `organisation:read` `POST /api/public-holidays` — Create/replace calendar — requires `organisation:write` Request: `{ year, countryCode, entries: [{ date, name, type, applicableRegions }] }` `POST /api/public-holidays/{year}/publish` — Publish calendar — requires `organisation:write`

#### Permission Model

Access to BC-02 endpoints is gated by two capabilities derived from BC-03 Authority Profiles:

- `organisation:read` — read-only view of org structure (all employees should have this for directory purposes)
- `organisation:write` — create/modify org structure (HR Manager / Tenant Admin only)

---

### BC-03 — Authority & Delegation

**Purpose:** Owns the Authority Profile system — the business-authority definitions that positions carry, and the derivation of technical permissions from them. Owns delegation records (temporary transfer of authority between positions). This BC is the authoritative RBAC specification for the entire Circlate platform. No technical permission check in any endpoint may bypass this contract.

#### Aggregates

**AuthorityProfile** (Aggregate Root)

- `profileId` Guid
- `tenantId` Guid
- `name` string (e.g. `Manager Standard`)
- `version` int (incremented on every publish)
- `status` ProfileStatus (Draft / Active / Deprecated)
- `entries` AuthorityEntry\[\] (entities)
- `publishedAt` DateTime UTC (nullable)

**AuthorityEntry** (Entity)

- `entryId` Guid
- `profileId` Guid
- `authorityName` string — human-readable business authority (e.g. `Approve Leave`)
- `capability` string — machine-readable capability string (e.g. `leave:approve:department`)
- `financialThreshold` decimal (nullable — for financial authority entries only)
- `scope` AuthorityScope enum (Own / Team / Department / Organisation)
- `notes` string (nullable)

**DelegationRecord** (Aggregate Root)

- `delegationId` Guid
- `tenantId` Guid
- `fromPositionInstanceId` Guid — the position delegating authority
- `toPositionInstanceId` Guid — the position receiving delegated authority
- `authorityEntries` string\[\] — the specific capabilities being delegated (subset of delegator's profile)
- `reason` string
- `startDate` DateOnly
- `endDate` DateOnly
- `status` DelegationStatus (Pending / Active / Expired / Revoked)
- `authorisedBy` Guid (position instance that approved the delegation)
- `createdAt`, `revokedAt` DateTime UTC

#### Value Objects

- **Capability** — validated string matching pattern `^[a-z][a-z0-9-]*:[a-z][a-z0-9-]*(:[a-z][a-z0-9-]*)?$`
- **FinancialThreshold** — positive decimal + currency code; `null` = unlimited

---

#### Permission Derivation Contract

This is the authoritative mapping from business authority to endpoint authorization. Every API endpoint in Circlate must declare exactly one required capability. That capability maps to exactly one business authority name. The chain is:

**`Business Authority → Capability String → JWT Claim → Endpoint Guard`**

The `caps` claim in the JWT is a JSON array of capability strings. The API middleware checks that at least one entry in `caps` matches the endpoint's declared requirement.

**Naming Standards for Capabilities**

Format: `{domain}:{action}[:{scope}]`

- `domain` — lowercase, hyphenated noun matching the BC: `leave`, `expenses`, `attendance`, `employees`, `compensation`, `recruitment`, `organisation`, `positions`, `work-structures`, `reports`, `rules`, `documents`, `assets`, `announcements`, `users`, `authority`
- `action` — verb: `read`, `write`, `approve`, `submit`, `manage`, `export`, `assign`, `delete`
- `scope` (optional) — `own`, `team`, `department`, `all`

Capability strings are **always lowercase with hyphens**. Never camelCase. Never underscores.

**Complete Capability Mapping Table**

| Business Authority | Capability | Endpoints Protected |
| --- | --- | --- |
| View Own Profile | `employees:read:own` | `GET /employees/me` |
| Update Own Contact Info | `employees:write:own` | `PATCH /employees/me` |
| View Team Profiles | `employees:read:team` | `GET /employees?scope=team` |
| View All Profiles | `employees:read:all` | `GET /employees` |
| Create Employee | `employees:write` | `POST /employees` |
| Edit Any Employee | `employees:write` | `PUT /employees/{id}` |
| Terminate Employee | `employees:terminate` | `POST /employees/{id}/terminate` |
| Submit Leave | `leave:submit` | `POST /leave` |
| View Own Leave | `leave:read:own` | `GET /leave/me` |
| View Team Leave | `leave:read:team` | `GET /leave?scope=team` |
| View All Leave | `leave:read:all` | `GET /leave` |
| Approve Leave (team) | `leave:approve:team` | `POST /leave/{id}/approve` |
| Approve Leave (department) | `leave:approve:department` | `POST /leave/{id}/approve` |
| Reject Leave | `leave:reject` | `POST /leave/{id}/reject` |
| Manage Leave Policies | `leave:manage-policy` | `POST/PUT /leave/policies` |
| Submit Expense | `expenses:submit` | `POST /expenses` |
| View Own Expenses | `expenses:read:own` | `GET /expenses/me` |
| View Team Expenses | `expenses:read:team` | `GET /expenses?scope=team` |
| View All Expenses | `expenses:read:all` | `GET /expenses` |
| Approve Expenses (≤500) | `expenses:approve:500` | `POST /expenses/{id}/approve` (threshold enforced) |
| Approve Expenses (≤2000) | `expenses:approve:2000` | `POST /expenses/{id}/approve` |
| Approve Expenses (≤5000) | `expenses:approve:5000` | `POST /expenses/{id}/approve` |
| Approve Expenses (unlimited) | `expenses:approve:unlimited` | `POST /expenses/{id}/approve` |
| View Own Attendance | `attendance:read:own` | `GET /attendance/me` |
| View Team Attendance | `attendance:read:team` | `GET /attendance?scope=team` |
| View All Attendance | `attendance:read:all` | `GET /attendance` |
| Authorise Overtime | `attendance:approve-overtime` | `POST /attendance/overtime/{id}/approve` |
| Approve Attendance Exception | `attendance:approve-exception` | `POST /attendance/exceptions/{id}/approve` |
| Manage Shift Patterns | `attendance:manage-patterns` | `POST/PUT /attendance/patterns` |
| Initiate Recruitment | `recruitment:initiate` | `POST /recruitment/vacancies` |
| Manage Recruitment Pipeline | `recruitment:manage` | `PUT /recruitment/applications/{id}` |
| Approve Hire | `recruitment:approve-hire` | `POST /recruitment/{id}/approve-offer` |
| View Compensation | `compensation:read:own` | `GET /compensation/me` |
| View Team Compensation | `compensation:read:team` | `GET /compensation?scope=team` |
| Manage Compensation | `compensation:write` | `POST/PUT /compensation` |
| Record Bonus | `compensation:record-bonus` | `POST /compensation/bonus` |
| Read Organisation | `organisation:read` | `GET /organisation, /departments, /cost-centres` |
| Manage Organisation | `organisation:write` | `POST/PUT/DELETE /organisation/*` |
| View Positions | `positions:read` | `GET /positions` |
| Manage Positions | `positions:write` | `POST/PUT/DELETE /positions` |
| Assign Authority Profile | `authority:assign` | `POST /positions/{id}/authority-profile` |
| Assign Employee to Position | `positions:assign` | `POST /positions/{id}/assign` |
| View Work Structures | `work-structures:read` | `GET /work-structures` |
| Manage Work Structures | `work-structures:write` | `POST/PUT/DELETE /work-structures` |
| Manage Allocations | `work-structures:allocate` | `POST /work-structures/{id}/allocations` |
| View Reports | `reports:read` | `GET /reports/*` |
| Export Reports | `reports:export` | `GET /reports/*/export` |
| Manage Report Schedules | `reports:manage` | `POST /reports/schedules` |
| Manage Rules & Policies | `rules:write` | `POST/PUT/DELETE /rules/policies` |
| View Rules | `rules:read` | `GET /rules/policies` |
| Manage Documents | `documents:write` | `POST/DELETE /documents` |
| View Own Documents | `documents:read:own` | `GET /documents/me` |
| View All Documents | `documents:read:all` | `GET /documents` |
| Manage Assets | `assets:write` | `POST/PUT /assets` |
| Assign Asset | `assets:assign` | `POST /assets/{id}/assign` |
| Publish Announcement | `announcements:publish` | `POST /announcements` |
| Manage Users | `users:manage` | `POST/PATCH /users` |
| Manage Authority Profiles | `authority:manage` | `POST/PUT /authority-profiles` |
| Manage Delegation | `authority:delegate` | `POST /delegations` |

---

#### Standard Authority Profiles

**Employee Standard** — Every employee's baseline profile. Attached to all positions by default.

| Authority | Capability | Scope |
| --- | --- | --- |
| View Own Profile | `employees:read:own` | Own |
| Update Own Contact Info | `employees:write:own` | Own |
| Submit Leave | `leave:submit` | Own |
| View Own Leave | `leave:read:own` | Own |
| Submit Expense | `expenses:submit` | Own |
| View Own Expenses | `expenses:read:own` | Own |
| View Own Attendance | `attendance:read:own` | Own |
| View Own Compensation | `compensation:read:own` | Own |
| View Own Documents | `documents:read:own` | Own |
| Read Organisation | `organisation:read` | Org-wide |
| View Positions | `positions:read` | Org-wide |

**Supervisor Standard** — For first-line supervisors managing a team.

Inherits all Employee Standard entries, plus:

| Authority | Capability | Financial Threshold |
| --- | --- | --- |
| View Team Profiles | `employees:read:team` | — |
| View Team Leave | `leave:read:team` | — |
| Approve Leave (team) | `leave:approve:team` | — |
| Reject Leave | `leave:reject` | — |
| View Team Expenses | `expenses:read:team` | — |
| Approve Expenses | `expenses:approve:500` | BND 500 |
| View Team Attendance | `attendance:read:team` | — |
| Authorise Overtime | `attendance:approve-overtime` | — |
| Approve Attendance Exception | `attendance:approve-exception` | — |
| View Work Structures | `work-structures:read` | — |

**Manager Standard** — For department/function managers.

Inherits all Supervisor Standard entries, plus:

| Authority | Capability | Financial Threshold |
| --- | --- | --- |
| Approve Leave (department) | `leave:approve:department` | — |
| Approve Expenses | `expenses:approve:2000` | BND 2,000 |
| View Team Compensation | `compensation:read:team` | — |
| Initiate Recruitment | `recruitment:initiate` | — |
| Approve Hire | `recruitment:approve-hire` | — |
| View Reports | `reports:read` | — |
| Manage Work Structures | `work-structures:write` | — |
| Manage Allocations | `work-structures:allocate` | — |

**Executive Standard** — For C-level / Directors.

Inherits all Manager Standard entries, plus:

| Authority | Capability | Financial Threshold |
| --- | --- | --- |
| View All Leave | `leave:read:all` | — |
| Approve Expenses | `expenses:approve:unlimited` | Unlimited |
| View All Attendance | `attendance:read:all` | — |
| View All Expenses | `expenses:read:all` | — |
| Manage Organisation | `organisation:write` | — |
| Export Reports | `reports:export` | — |
| Manage Delegation | `authority:delegate` | — |

**HR Manager** — Human Resources specific. Not a superset of Executive; separate profile.

| Authority | Capability |
| --- | --- |
| All Employee Standard entries | (see above) |
| View All Profiles | `employees:read:all` |
| Create Employee | `employees:write` |
| Edit Any Employee | `employees:write` |
| Terminate Employee | `employees:terminate` |
| View All Leave | `leave:read:all` |
| Approve Leave (org-wide) | `leave:approve:department` |
| Manage Leave Policies | `leave:manage-policy` |
| View All Expenses | `expenses:read:all` |
| Approve Expenses (≤2000) | `expenses:approve:2000` |
| Manage Compensation | `compensation:write` |
| Record Bonus | `compensation:record-bonus` |
| View All Compensation | `compensation:read:team` |
| Manage Positions | `positions:write` |
| Assign Employee to Position | `positions:assign` |
| Assign Authority Profile | `authority:assign` |
| View All Documents | `documents:read:all` |
| Manage Documents | `documents:write` |
| Publish Announcement | `announcements:publish` |
| Manage Users | `users:manage` |
| View Reports | `reports:read` |
| Export Reports | `reports:export` |
| Manage Rules & Policies | `rules:write` |

**Finance Manager** — Finance-specific. Expense authority without HR personnel access.

| Authority | Capability | Financial Threshold |
| --- | --- | --- |
| All Employee Standard entries | — | — |
| View All Expenses | `expenses:read:all` | — |
| Approve Expenses (unlimited) | `expenses:approve:unlimited` | Unlimited |
| View All Compensation | `compensation:read:team` | — |
| Export Reports | `reports:export` | — |

---

#### Authority Matrix (Standard Profiles Summary)

| Authority | Employee | Supervisor | Manager | Executive | HR Manager | Finance Manager |
| --- | --- | --- | --- | --- | --- | --- |
| View Own Profile | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| View Team/All Profiles | — | Team | Dept | All | All | — |
| Manage Employees | — | — | — | — | ✓ | — |
| Submit Leave | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Approve Leave | — | Team | Dept | All | All | — |
| Submit Expenses | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Approve Expenses | — | ≤500 | ≤2,000 | Unlimited | ≤2,000 | Unlimited |
| View Compensation | Own | Own | Team | All | All | All |
| Manage Compensation | — | — | — | — | ✓ | — |
| Approve Overtime | — | ✓ | ✓ | ✓ | ✓ | — |
| Initiate Recruitment | — | — | ✓ | ✓ | ✓ | — |
| Manage Organisation | — | — | — | ✓ | — | — |
| View Reports | — | — | ✓ | ✓ | ✓ | ✓ |
| Export Reports | — | — | — | ✓ | ✓ | ✓ |
| Manage Rules | — | — | — | — | ✓ | — |

---

#### Delegation Matrix

Delegation transfers a subset of a position's authority to another position for a defined period. Constraints:

1. **Cannot delegate authority you do not hold.** A Supervisor cannot delegate Manager-level capabilities.
2. **Cannot delegate to a subordinate position in the same reporting line.** This prevents circular authority.
3. **Delegation requires a mandatory end date.** No open-ended delegations.
4. **Delegated authority cannot be re-delegated.** The recipient cannot pass it on.
5. **Financial delegation cannot exceed the delegator's threshold.** A Manager with BND 2,000 limit cannot delegate BND 5,000 approval authority.

| Delegating Profile | May Delegate To | Delegatable Authorities |
| --- | --- | --- |
| Supervisor Standard | Peer Supervisor, Acting Supervisor | Leave approval (team), Expense approval (≤500), Overtime approval |
| Manager Standard | Deputy Manager, Senior Supervisor | Leave approval (dept), Expense approval (≤2000), Recruitment initiation |
| Executive Standard | Deputy Director, Manager | Leave approval (all), Expense approval (up to own threshold), Organisation write |
| HR Manager | Deputy HR Manager | All HR capabilities except Manage Users and Assign Authority Profile |
| Finance Manager | Deputy Finance Manager | Expense approval (up to own threshold), Compensation read |

---

#### Escalation Matrix

Escalation occurs when an approver fails to act within the SLA window (default: 3 business days, configurable per request type in BC-07).

| Request Type | Level 1 Approver | Level 2 (Escalation) | Level 3 (Final) |
| --- | --- | --- | --- |
| Leave | Direct line manager position | Department head position | HR Manager position |
| Expense (within threshold) | Cost centre owner position | Finance Manager position | Executive position |
| Expense (over threshold) | Finance Manager position | Executive position | Tenant Admin |
| Attendance Exception | Work structure supervisor | Department head | HR Manager |
| Overtime | Work structure supervisor | Manager | HR Manager |
| Recruitment Requisition | Department head | Executive | HR Manager |

Maximum 3 escalation hops. Beyond 3 hops: flagged as `EscalationExhausted`, HR Manager notified for manual resolution.

---

#### Domain Events

| Event | Payload | Consumers |
| --- | --- | --- |
| `AuthorityProfileCreated` | profileId, tenantId, name | BC-04 Position Management |
| `AuthorityProfilePublished` | profileId, version, entryCount | BC-04, BC-06 Approval Routing (invalidate cache) |
| `AuthorityProfileAssigned` | positionInstanceId, profileId, assignedBy | BC-06, BC-01 (re-issue JWT caps claim) |
| `AuthorityProfileRevoked` | positionInstanceId, profileId | BC-06, BC-01 (re-issue JWT) |
| `DelegationCreated` | delegationId, fromPositionId, toPositionId, capabilities, endDate | BC-06 Approval Routing, Notifications |
| `DelegationActivated` | delegationId, activatedAt | BC-06, BC-01 (temporary cap injection) |
| `DelegationExpired` | delegationId, expiredAt | BC-06, BC-01 (remove temp caps), Notifications |
| `DelegationRevoked` | delegationId, revokedBy, revokedAt | BC-06, BC-01, Notifications |

#### API Contracts

`GET /api/authority-profiles` — List profiles — requires `authority:manage` `POST /api/authority-profiles` — Create profile — requires `authority:manage` `GET /api/authority-profiles/{id}` — Get profile with entries — requires `authority:manage` `PUT /api/authority-profiles/{id}` — Update draft profile — requires `authority:manage` `POST /api/authority-profiles/{id}/publish` — Publish profile — requires `authority:manage` `POST /api/authority-profiles/{id}/deprecate` — Deprecate — requires `authority:manage`

`POST /api/positions/{positionId}/authority-profile` — Assign profile to position — requires `authority:assign` Request: `{ authorityProfileId, effectiveFrom }`

`GET /api/delegations` — List active delegations for tenant — requires `authority:delegate` `POST /api/delegations` — Create delegation — requires `authority:delegate` Request: `{ fromPositionInstanceId, toPositionInstanceId, capabilities[], reason, startDate, endDate }` `DELETE /api/delegations/{id}` — Revoke delegation — requires `authority:delegate`

`GET /api/authority-profiles/{id}/capabilities` — Preview resolved capability list for a profile — requires `authority:manage`

---

### BC-04 — Position Management

**Purpose:** Owns the complete position lifecycle — from abstract position definitions through approved headcount establishment to individual filled or vacant position instances. Maintains the organisational reporting hierarchy. Manages acting assignments when a position holder is temporarily unavailable. No capability BC may create its own notion of an organisational role or reporting relationship.

#### The Three-Layer Position Model

Positions in Circlate are not a flat list. They exist as three distinct concepts that must never be conflated:

**Layer 1 — Position Template** (what the role is) A position template is the job definition: title, grade, department, responsibilities, required skills, required certifications, and the authority profile that positions of this type carry. Templates are reusable. Twenty security officer positions all reference the same Security Officer template.

**Layer 2 — Position Establishment** (how many of this role are approved) Establishment is the annual approved headcount budget for a position template within a department. Created by HR and approved by Executive authority. Separates the question of "does this role exist?" from "how many people can fill it this year?".

**Layer 3 — Position Instance** (a specific slot that can be filled) An instance represents one approved position slot. It may be Vacant, Filled, or under ActingCoverage. Each instance is an independent entity within the establishment — it can be filled by different people over time, and its occupancy history is a full audit trail.

```
PositionTemplate: Security Officer (Grade G3)
  └── PositionEstablishment: Brunei-Muara Region 2026 — Approved: 20
        └── PositionInstance #001 → Filled by: Ahmad Bin Hassan (since 2024-03-01)
        └── PositionInstance #002 → Filled by: Siti Nabilah (since 2025-06-15)
        └── PositionInstance #003 → Vacant (Resignation 2026-01-10)
        └── PositionInstance #004 → ActingCoverage: Rafi Zulkifli (acting for Noor Hafiz)
        ... (20 instances total)
```

#### Aggregates

**PositionTemplate** (Aggregate Root)

- `templateId` Guid
- `tenantId` Guid
- `title` string (e.g. `Security Officer`)
- `code` string (unique per tenant, e.g. `POS-SEC-OFF`)
- `departmentId` Guid (FK to BC-02 Department)
- `gradeId` Guid (FK to PositionGrade)
- `defaultAuthorityProfileId` Guid (FK to BC-03 AuthorityProfile)
- `jobDescription` string (long text)
- `responsibilities` string\[\]
- `requiredSkillIds` Guid\[\] (FK to BC-11 Skill)
- `requiredCertificationIds` Guid\[\] (FK to BC-12 Training)
- `deputyTemplateId` Guid (nullable — the template whose instances provide deputy coverage)
- `reportingToTemplateId` Guid (nullable — parent in the org chart hierarchy)
- `status` TemplateStatus (Draft / Active / Deprecated)

**PositionEstablishment** (Aggregate Root)

- `establishmentId` Guid
- `tenantId` Guid
- `positionTemplateId` Guid
- `departmentId` Guid
- `effectiveYear` int
- `approvedHeadcount` int
- `filledCount` int (derived — count of non-Vacant instances)
- `vacantCount` int (derived — `approvedHeadcount - filledCount`)
- `budgetLineCode` string (nullable — ties to Finance BC cost tracking)
- `approvedByPositionId` Guid (the position instance that approved this establishment)
- `status` EstablishmentStatus (Draft / Approved / Frozen)

**PositionInstance** (Aggregate Root)

- `instanceId` Guid
- `tenantId` Guid
- `positionTemplateId` Guid
- `establishmentId` Guid
- `effectiveAuthorityProfileId` Guid (normally = template's default; override possible)
- `occupancy` PositionOccupancy (nullable entity — null means Vacant)
- `status` InstanceStatus (Vacant / Filled / ActingCoverage)
- `reportingToInstanceId` Guid (nullable — the specific instance this reports to; set after assignment)
- `createdAt` DateTime UTC

**PositionOccupancy** (Entity — child of PositionInstance)

- `occupancyId` Guid
- `instanceId` Guid
- `employeeId` Guid (FK to BC-05 Employee)
- `type` OccupancyType (Substantive / Acting)
- `startDate` DateOnly
- `endDate` DateOnly (nullable — open-ended for current occupant)
- `endReason` OccupancyEndReason (nullable — Resignation / Transfer / Termination / ActingEnded)

**ActingAssignment** (Aggregate Root)

- `actingAssignmentId` Guid
- `tenantId` Guid
- `targetInstanceId` Guid — the position instance being covered (must be Vacant or holder is on leave)
- `coveringEmployeeId` Guid — the employee performing the acting role
- `coveringFromInstanceId` Guid — the acting employee's substantive position instance
- `compensationMethod` ActingCompensationMethod enum (None / FixedAllowance / PercentageUplift / PositionDifferential)
- `compensationValue` decimal (nullable — the allowance amount, percentage, or not applicable)
- `compensationCurrency` string (applicable when FixedAllowance)
- `startDate` DateOnly
- `endDate` DateOnly
- `reason` string (e.g. `Annual Leave`, `Extended Medical Leave`, `Vacancy`)
- `authorisedByPositionId` Guid — must hold `positions:assign` capability
- `status` ActingStatus (Pending / Active / Completed / Cancelled)
- `auditApprovalRequired` bool (true if position grade difference ≥ 2 grades)

#### Acting Assignment Architecture

**When acting is used:**

- A position holder goes on extended leave (> 5 consecutive days) and their approval authority must be covered
- A position is Vacant and must be operationally covered before recruitment completes
- A specific delegation of operational responsibility (not authority — that uses BC-03 Delegation)

**Acting vs Delegation distinction:**

- **Delegation** (BC-03): Transfers specific approval authority entries from one position to another for a defined period. Used for leave, expense, and routing purposes.
- **Acting Assignment** (BC-04): Temporarily places an employee in a different position instance. The acting employee holds the full authority of the target position, not a subset. Used when the target position needs to be fully staffed.

**Compensation Methods:**

| Method | Description | Example |
| --- | --- | --- |
| `None` | No additional compensation for the acting period | Cover for peer absence with no uplift |
| `FixedAllowance` | A flat daily/monthly allowance added to base salary | BND 50/day acting allowance |
| `PercentageUplift` | A percentage of the acting employee's base salary | 10% uplift during acting period |
| `PositionDifferential` | The difference between the target position grade's midpoint and the acting employee's current salary | Grade G5 midpoint minus G3 midpoint |

**Acting Assignment Workflow:**

1. HR initiates acting assignment: selects target instance, covering employee, dates, reason, compensation method.
2. System validates: a. Covering employee's substantive position still exists and is Filled. b. Grade differential ≤ configured maximum (default: 3 grades). Flag if `auditApprovalRequired = true`. c. Date range does not overlap with another active acting assignment for the same target instance. d. Covering employee has no conflicting acting assignment in the period.
3. If `auditApprovalRequired = true`: routes to Executive authority for approval before activation.
4. On activation (`ActingStatus = Active`): a. `PositionInstance.status` changes to `ActingCoverage`. b. `PositionInstance.occupancy` updated with Acting type record. c. `ActingAssignmentActivated` domain event fired. d. BC-01 is notified: JWT for covering employee re-issued with authority profile of target position.
5. On completion/cancellation: a. `PositionInstance.status` reverts to `Filled` or `Vacant`. b. BC-01 notified: JWT reverts to substantive position authority profile. c. Compensation adjustment record created for Payroll Export (future Compensation BC).

#### Position Grade Framework

Grades provide a universal benchmark for authority thresholds, leave entitlements, notice periods, and salary band guidance. Grades are tenant-configurable but default bands are provided.

| Grade | Label | Default Monthly Salary Band (BND) | Leave Entitlement Band | Notice Period |
| --- | --- | --- | --- | --- |
| G1 | Entry Level | 500 – 800 | 7 days/year | 2 weeks |
| G2 | Junior | 800 – 1,200 | 7 days/year | 2 weeks |
| G3 | Mid-Level | 1,200 – 1,800 | 8 days/year | 1 month |
| G4 | Senior Individual | 1,800 – 2,500 | 8 days/year | 1 month |
| G5 | Supervisor | 2,500 – 3,500 | 10 days/year | 1 month |
| G6 | Senior Supervisor | 3,500 – 4,500 | 10 days/year | 2 months |
| G7 | Manager | 4,500 – 7,000 | 12 days/year | 2 months |
| G8 | Senior Manager | 7,000 – 10,000 | 14 days/year | 3 months |
| G9 | Director | 10,000 – 15,000 | 14 days/year | 3 months |
| G10 | Executive / C-Level | 15,000+ | 14 days/year | 6 months |

**Integration with Compensation BC:** The grade framework defines salary bands and leave entitlements that the future Compensation BC will use as guardrails. When BC-18 Compensation is built, the `CompensationPackage.baseSalary` will be validated against the grade band for the employee's current position instance. No payroll calculation is performed in BC-04.

#### Domain Events

| Event | Payload | Consumers |
| --- | --- | --- |
| `PositionTemplateCreated` | templateId, tenantId, title, gradeId, departmentId | BC-06 Routing |
| `PositionEstablishmentApproved` | establishmentId, templateId, year, headcount | Notifications |
| `PositionInstanceCreated` | instanceId, templateId, establishmentId | BC-06 |
| `PositionAssigned` | instanceId, employeeId, startDate, occupancyType | BC-01 (JWT refresh), BC-03 (profile activation), Notifications |
| `PositionVacated` | instanceId, employeeId, vacatedAt, reason | BC-06 (pending approvals escalation), BC-01, Notifications |
| `PositionTransferred` | instanceId, fromEmployeeId, toEmployeeId | BC-01, BC-06 |
| `ActingAssignmentCreated` | actingAssignmentId, targetInstanceId, coveringEmployeeId | Notifications |
| `ActingAssignmentActivated` | actingAssignmentId, activatedAt | BC-01, BC-06, Notifications |
| `ActingAssignmentCompleted` | actingAssignmentId, completedAt, compensationSummary | BC-18 Compensation (future), Notifications |
| `ActingAssignmentCancelled` | actingAssignmentId, cancelledAt, reason | BC-01, Notifications |
| `AuthorityProfileOverridden` | instanceId, overridingProfileId, overriddenBy | BC-06, BC-01 |
| `ReportingLineChanged` | instanceId, oldReportingToInstanceId, newReportingToInstanceId | BC-06 (invalidate routing cache) |

#### API Contracts

`GET /api/position-templates` — List all templates — requires `positions:read` `POST /api/position-templates` — Create template — requires `positions:write` `GET /api/position-templates/{id}` — Get template detail — requires `positions:read` `PUT /api/position-templates/{id}` — Update template — requires `positions:write`

`GET /api/position-establishments` — List establishments (filterable by year, department) — requires `positions:read` `POST /api/position-establishments` — Create establishment — requires `positions:write` Request: `{ positionTemplateId, departmentId, effectiveYear, approvedHeadcount, budgetLineCode }` `POST /api/position-establishments/{id}/approve` — Approve establishment — requires `positions:write` + `recruitment:approve-hire` (Executive level)

`GET /api/position-instances` — List instances (filterable by status, department, template) — requires `positions:read` `POST /api/position-instances` — Create instance against an establishment — requires `positions:write` `GET /api/position-instances/{id}` — Get instance with current occupancy — requires `positions:read` `POST /api/position-instances/{id}/assign` — Assign employee — requires `positions:assign` Request: `{ employeeId, startDate, occupancyType: "Substantive" }` `POST /api/position-instances/{id}/vacate` — Vacate position — requires `positions:assign` Request: `{ endDate, endReason }` `GET /api/position-instances/{id}/occupancy-history` — Full audit trail — requires `positions:read`

`GET /api/acting-assignments` — List active acting assignments — requires `positions:read` `POST /api/acting-assignments` — Create acting assignment — requires `positions:assign` Request: `{ targetInstanceId, coveringEmployeeId, startDate, endDate, reason, compensationMethod, compensationValue }` `POST /api/acting-assignments/{id}/activate` — Activate (or auto-activates on startDate) — requires `positions:assign` `POST /api/acting-assignments/{id}/complete` — Complete early — requires `positions:assign` `POST /api/acting-assignments/{id}/cancel` — Cancel — requires `positions:assign`

`GET /api/grades` — List grade definitions — requires `positions:read` `PUT /api/grades/{id}` — Update salary band for a grade — requires `positions:write`

`GET /api/org-chart` — Returns the full position reporting hierarchy as a tree — requires `positions:read` Response: nested tree of `{ instanceId, title, employeeName, status, children[] }`

---

### BC-05 — Work Structure Management

**Purpose:** Owns the operational groupings within which employees perform their work — projects, teams, sites, programmes, contracts, task forces, and committees. Work structures are first-class entities: they have supervisors, compliance requirements, cost allocations, and their own hierarchy. They are operationally distinct from the organisational hierarchy in BC-02 — an employee's department (BC-02) defines their HR home; their work structure assignments (BC-05) define where they spend their time.

#### Work Structure Types

| Type | Description | Example |
| --- | --- | --- |
| `Team` | A permanent functional team within a department | "Finance Team", "Night Security Team" |
| `Project` | Time-bounded, goal-oriented work | "KK Hospital Fit-Out Phase 2" |
| `Programme` | A collection of related projects under one umbrella | "Brunei Infrastructure Programme 2026" |
| `Site` | A physical location with its own operational requirements | "BSP Seria Site", "JPMC Guard Post" |
| `Contract` | A client contract requiring dedicated resource allocation | "Contract 2024-BSP-001" |
| `TaskForce` | A temporary cross-functional group formed for a specific purpose | "Safety Audit Task Force" |
| `Committee` | A governance or advisory body | "HSE Committee", "IT Steering Committee" |

#### Aggregates

**WorkStructure** (Aggregate Root)

- `workStructureId` Guid
- `tenantId` Guid
- `type` WorkStructureType enum
- `name` string
- `code` string (unique per tenant, e.g. `PROJ-2024-BSP-001`)
- `parentWorkStructureId` Guid (nullable — allows nesting: `Programme → Project → Sub-Project`)
- `supervisorPositionInstanceId` Guid (nullable — the position instance with operational responsibility)
- `costCentreId` Guid (nullable — cost centre override for this work structure; falls back to department cost centre)
- `departmentId` Guid (nullable — the owning department in BC-02; required for `Team` type)
- `startDate` DateOnly (nullable)
- `endDate` DateOnly (nullable)
- `status` WorkStructureStatus (Planning / Active / OnHold / Completed / Cancelled)
- `complianceRequirements` WorkStructureComplianceRequirement\[\] (entities)

**WorkStructureAssignment** (Aggregate Root)

- `assignmentId` Guid
- `tenantId` Guid
- `workStructureId` Guid
- `employeeId` Guid
- `role` AssignmentRole enum (Member / Lead / Coordinator / Supervisor / Observer)
- `allocationPercentage` decimal (0.00 to 1.00 — fraction of working time)
- `startDate` DateOnly
- `endDate` DateOnly (nullable)
- `isPrimary` bool — an employee's primary assignment is used for HR reporting and cost allocation default
- `status` AssignmentStatus (Pending / Active / Completed / Cancelled)
- `complianceStatus` AssignmentComplianceStatus (Compliant / PendingRequirements / NonCompliant)

**WorkStructureComplianceRequirement** (Entity — child of WorkStructure)

- `requirementId` Guid
- `workStructureId` Guid
- `type` ComplianceRequirementType enum (SiteInduction / ClientAccessPass / HSECertification / SecurityClearance / MedicalFitness / DrugTest / Custom)
- `name` string
- `mandatory` bool — if true, assignment cannot become Active until this requirement is met
- `validityPeriodDays` int (nullable — e.g. HSE certification valid for 365 days)
- `verificationRequired` bool — requires HR to upload a document as evidence

**EmployeeComplianceRecord** (Aggregate Root)

- `recordId` Guid
- `tenantId` Guid
- `employeeId` Guid
- `requirementId` Guid
- `workStructureId` Guid
- `satisfiedAt` DateTime UTC (nullable)
- `expiresAt` DateTime UTC (nullable)
- `evidenceDocumentId` Guid (nullable — link to BC-14 Document)
- `status` ComplianceRecordStatus (Pending / Satisfied / Expired / Waived)
- `waivedBy` Guid (nullable — position instance)
- `waivedReason` string (nullable)

#### Value Objects

- **AllocationPercentage** — decimal 0.00–1.00, displayed as 0%–100%; `0.60` = 60%
- **WorkStructureType** — the type enum above
- **HierarchyDepth** — maximum nesting depth: 5 levels (Programme → Project → Sub-Project → Work Package → Task is the deepest meaningful structure)

#### Work Structure Hierarchy

Work structures support nesting through `parentWorkStructureId`. The hierarchy can represent complex programme structures:

```
WorkStructure: Brunei Infrastructure Programme 2026  [Programme]
  └── WorkStructure: KK Hospital Project             [Project]
        └── WorkStructure: Civil Works Package       [Project/Sub]
        └── WorkStructure: M&E Package               [Project/Sub]
  └── WorkStructure: Temburong Bridge Phase 3        [Project]
        └── WorkStructure: North Abutment Site       [Site]
        └── WorkStructure: South Abutment Site       [Site]
```

An employee may be assigned at any level. If assigned to the Programme, they are considered to have awareness of all projects under it. Actual allocation percentages must be assigned at the leaf level where time is tracked.

#### Matrix Reporting Model

An employee may have simultaneously:

- A **functional manager** (the head of their department's position — organisational line management in BC-02/BC-04)
- A **project/work structure supervisor** (the supervisor position of their primary work structure assignment — operational management in BC-05)

These are independent reporting relationships. The functional manager handles HR concerns (leave, performance review, compensation changes). The project supervisor handles operational concerns (timesheets, task completion, day-to-day work direction).

**Example:**

```
Engineer Ahmad reports functionally to:
  Civil Engineering Department Head (BC-04 PositionInstance)
  → This position handles Ahmad's leave approvals, performance reviews

Ahmad is assigned to:
  Project Alpha (60%) — supervisor: Project Alpha PM (BC-05)
  Project Bravo (40%) — supervisor: Project Bravo PM (BC-05)
  → These supervisors approve Ahmad's timesheets and attendance exceptions
  → Ahmad's daily work is directed by his project supervisors
  → His HR matters go to his functional manager
```

Request routing (BC-06) must resolve the correct authority for each request type:

- Leave, Expense → functional manager (position hierarchy)
- Timesheet, Attendance exception → work structure supervisor (work structure hierarchy)
- Performance review → functional manager
- Overtime → depends on where the overtime is worked → work structure supervisor

#### Allocation Architecture

Allocation percentages represent the proportion of an employee's total working capacity dedicated to a work structure.

**Invariants:**

1. An employee's total active allocation percentage must be ≤ 100%.
2. An employee may have exactly one primary assignment at any time.
3. Lead role may only have one occupant per work structure at a time.
4. If `mandatory` compliance requirements are unmet, assignment status must remain `Pending` — it cannot activate.

**Capacity Calculation:** For a work structure with multiple assignments:

```
Total Capacity Allocated = SUM(allocationPercentage) for all Active assignments
Over-allocated employees = employees where SUM across all work structures > 1.00
```

**Utilisation Calculation** (operational metric for Reports BC):

```
Utilisation = actual time logged (from Attendance BC) ÷ expected time (from allocation % × working days)
```

**Conflict Detection Rules:**

- **Over-allocation:** New assignment would bring total allocation > 100% → Warning raised, HR confirmation required. Not a hard block (some tenants permit >100% short-term).
- **Date overlap conflict:** New assignment overlaps with an existing assignment to the same work structure for the same employee → Rejected (hard block).
- **Duplicate lead:** Assigning a second `Lead` role to a work structure where one already exists → Rejected unless the first lead's assignment end date is set.
- **Compliance prerequisite:** If work structure has mandatory compliance requirements and employee has no corresponding `EmployeeComplianceRecord` with status `Satisfied` → Assignment status set to `Pending`, not `Active`. HR notified.

#### Work Structure Compliance Interactions with Position Requirements

Work structure compliance requirements are distinct from position requirements (defined in BC-04 PositionTemplate). Both may apply simultaneously:

- **Position requirement** (BC-04): Applies to the employee because of the position they hold. E.g., a Security Officer position requires a valid Security Licence. This is checked on `PositionAssigned`.
- **Work structure requirement** (BC-05): Applies to the employee because of the site or project they're working on. E.g., a BSP site requires a site induction. This is checked on `WorkStructureAssignment` activation.

An employee may satisfy a requirement at the position level but still need to complete additional work structure requirements before being assigned to a specific site.

#### Domain Events

| Event | Payload | Consumers |
| --- | --- | --- |
| `WorkStructureCreated` | workStructureId, tenantId, type, name, supervisorPositionId | BC-06 Routing |
| `WorkStructureActivated` | workStructureId, activatedAt | Notifications |
| `WorkStructureCompleted` | workStructureId, completedAt | BC-06, Reports |
| `WorkStructureSupervisorChanged` | workStructureId, oldSupervisorId, newSupervisorId | BC-06 (invalidate routing cache), Notifications |
| `ProjectAllocationChanged` | assignmentId, employeeId, workStructureId, oldPct, newPct | Reports, BC-06 |
| `EmployeeAssignedToWorkStructure` | assignmentId, employeeId, workStructureId, role, allocationPct | BC-06, Notifications |
| `EmployeeRemovedFromWorkStructure` | assignmentId, employeeId, workStructureId, endedAt | BC-06 |
| `ComplianceRequirementAdded` | requirementId, workStructureId, type, mandatory | BC-05 internal (re-evaluate all active assignments) |
| `ComplianceRequirementSatisfied` | recordId, employeeId, workStructureId, requirementId | BC-05 (try activate pending assignment), Notifications |
| `ComplianceRequirementExpired` | recordId, employeeId, workStructureId, requirementId | Notifications, HR Dashboard |

#### API Contracts

`GET /api/work-structures` — List (filterable by type, status, department) — requires `work-structures:read` `POST /api/work-structures` — Create — requires `work-structures:write` Request: `{ type, name, code, parentWorkStructureId?, supervisorPositionInstanceId?, costCentreId?, startDate?, endDate? }` `GET /api/work-structures/{id}` — Get with assignments and compliance — requires `work-structures:read` `PATCH /api/work-structures/{id}` — Update — requires `work-structures:write` `POST /api/work-structures/{id}/activate` — Activate — requires `work-structures:write` `POST /api/work-structures/{id}/complete` — Mark complete — requires `work-structures:write`

`GET /api/work-structures/{id}/assignments` — List assignments — requires `work-structures:read` `POST /api/work-structures/{id}/assignments` — Assign employee — requires `work-structures:allocate` Request: `{ employeeId, role, allocationPercentage, startDate, endDate?, isPrimary }` `PATCH /api/work-structures/{id}/assignments/{assignmentId}` — Update allocation — requires `work-structures:allocate` `DELETE /api/work-structures/{id}/assignments/{assignmentId}` — End assignment — requires `work-structures:allocate` Request: `{ endDate, endReason }`

`GET /api/work-structures/{id}/compliance` — List compliance requirements — requires `work-structures:read` `POST /api/work-structures/{id}/compliance` — Add requirement — requires `work-structures:write` `POST /api/employees/{employeeId}/compliance-records` — Record satisfied requirement — requires `employees:write` Request: `{ requirementId, workStructureId, satisfiedAt, expiresAt?, evidenceDocumentId? }`

`GET /api/employees/{employeeId}/allocations` — All active allocations for an employee — requires `employees:read:team` Response: `[{ workStructureId, name, role, allocationPercentage, isPrimary, status }]` `GET /api/work-structures/{id}/utilisation` — Utilisation report for a work structure — requires `reports:read`

---

### BC-06 — Approval Routing

**Purpose:** The position-routed approval engine. Receives approval requests from capability BCs (Leave, Expenses, Attendance, Recruitment, Assets) and resolves them to the correct approver position instance. Manages the full lifecycle of an approval — routing, escalation, delegation, timeout, and audit. No capability BC may implement its own approval routing — all approvals flow through this engine.

#### Aggregates

**ApprovalRequest** (Aggregate Root)

- `requestId` Guid
- `tenantId` Guid
- `requestType` ApprovalRequestType enum (LeaveRequest / ExpenseClaim / AttendanceException / OvertimeRequest / RecruitmentRequisition / AssetRequest)
- `sourceId` Guid — the ID of the originating record in the source BC (e.g., the leaveRequestId)
- `submitterEmployeeId` Guid
- `submitterPositionInstanceId` Guid
- `status` ApprovalStatus (Pending / Approved / Rejected / Escalated / Withdrawn / EscalationExhausted)
- `currentApprovalStepId` Guid (nullable — points to the active step)
- `submittedAt` DateTime UTC
- `resolvedAt` DateTime UTC (nullable)
- `metadata` Dictionary\<string, string> — contextual data for routing (e.g., `{ "amount": "750.00", "currency": "BND" }`)

**ApprovalChain** (Aggregate Root)

- `chainId` Guid
- `tenantId` Guid
- `requestId` Guid
- `steps` ApprovalStep\[\] (entities, ordered)
- `currentStepIndex` int
- `resolvedAt` DateTime UTC (nullable)

**ApprovalStep** (Entity — child of ApprovalChain)

- `stepId` Guid
- `chainId` Guid
- `stepIndex` int
- `resolvedApproverPositionInstanceId` Guid — the position instance assigned to this step
- `resolvedApproverEmployeeId` Guid (nullable — the person occupying that instance at assignment time)
- `deadline` DateTime UTC — computed from policy (BC-07)
- `status` StepStatus (Pending / Approved / Rejected / Escalated / Skipped)
- `decidedAt` DateTime UTC (nullable)
- `decisionNotes` string (nullable)
- `escalationLevel` int (0 = not escalated, 1 = first escalation, etc.)

#### Routing Sources

| Request Type | Primary Routing Source | Secondary Source (if primary insufficient) |
| --- | --- | --- |
| Leave Request | Organisational hierarchy — position reporting line | HR Manager position |
| Expense Claim | Cost centre hierarchy — cost centre owner position | Finance Manager, then Executive |
| Attendance Exception | Work structure hierarchy — work structure supervisor | Department head, then HR Manager |
| Overtime Request | Work structure hierarchy — work structure supervisor | Department head |
| Recruitment Requisition | Organisational hierarchy — department head | Executive (approve hire authority) |
| Asset Request | Cost centre owner for the department | Executive |

#### Resolution Algorithm

The `ApprovalRoutingService` resolves an approval chain when a request is submitted:

**Step 1 — Load context**

- Load the submitter's current `PositionInstance` and its `effectiveAuthorityProfileId`
- Load the submitter's `WorkStructureAssignment` (primary, if exists)
- Load the request `metadata` (amount, type, etc.)

**Step 2 — Determine routing source**

- Apply the routing source table above based on `requestType`
- For Expense Claims: check amount against cost centre threshold to determine whether single-step or multi-step approval is needed

**Step 3 — Walk the hierarchy** For position hierarchy routing:

1. Start from the submitter's `reportingToInstanceId`
2. Load that position instance and its authority profile
3. Check if the profile contains the required capability for this request type
4. If YES: this is the approver. Add as ApprovalStep. Done (unless multi-step required).
5. If NO: move to that position's `reportingToInstanceId` and repeat
6. If `reportingToInstanceId` is null: no approver found in hierarchy — fall back to HR Manager position

For work structure hierarchy routing:

1. Start from the submitter's primary work structure's `supervisorPositionInstanceId`
2. Check if that supervisor position holds the required capability
3. If YES: use it. If NO or null: walk to the work structure's `parentWorkStructureId`'s supervisor

For cost centre hierarchy routing:

1. Load the cost centre for the submitter's department (or override from work structure)
2. Check the cost centre's `ownerPositionId`
3. If the request amount exceeds the cost centre's `approvalThreshold`: also add the parent cost centre's owner as a second step

**Step 4 — Check for active delegation** For each resolved approver position instance:

1. Query `DelegationRecord` for active delegations from this position that include the required capability
2. If a delegation exists: replace the step's `resolvedApproverPositionInstanceId` with the delegate position
3. Record `isDelegated = true` and `originalPositionInstanceId` on the step for audit

**Step 5 — Check position occupancy** For each resolved approver position instance:

1. If the instance is Vacant: escalate immediately — skip to its parent in the hierarchy
2. If the instance has ActingCoverage: use the acting employee as the approver (they hold full position authority)
3. If the occupant is on approved leave: check for active delegation (covered in Step 4)

**Step 6 — Apply escalation policy**

- Retrieve the escalation timeout from BC-07 for this request type
- Set `deadline` on each step
- Build the escalation chain: if Step 1 times out, Step 2 activates; if Step 2 times out, Step 3 activates

**Step 7 — Persist and notify**

- Save the `ApprovalChain` and `ApprovalRequest` with `status = Pending`
- Fire `ApprovalRequested` domain event
- BC-17 Notifications consumes event and sends notification to the first step's current approver

---

#### Approval Chain Decision Trees

**Leave Approval Decision Tree:**

```
Employee submits Leave Request
  │
  ├─ Routing Source: Position Hierarchy
  │
  ├─ Who has 'leave:approve' capability above submitter in reporting line?
  │     │
  │     ├─ Resolved: Line Manager Position
  │     │     │
  │     │     ├─ Position Filled? YES → Assign to occupant
  │     │     │     │
  │     │     │     ├─ Active delegation for leave:approve? YES → Route to delegate
  │     │     │     ├─ No delegation → Route to occupant
  │     │     │
  │     │     ├─ Position Vacant? → Escalate to next level up
  │     │     ├─ Occupant on ActingCoverage? → Route to acting employee
  │     │
  │     ├─ No position in hierarchy has leave:approve capability
  │           → Route to HR Manager position
  │
  ├─ Approval step created → Deadline set (default: 3 business days)
  ├─ Timeout? → Escalate to Department Head
  ├─ 2nd timeout? → Escalate to HR Manager
  ├─ 3rd timeout? → Status = EscalationExhausted, HR manual flag
```

**Expense Claim Decision Tree:**

```
Employee submits Expense Claim (Amount: BND 750)
  │
  ├─ Routing Source: Cost Centre Hierarchy
  ├─ Load department cost centre (CC-OPS-01, threshold: BND 500, owner: Ops Manager)
  │
  ├─ Amount (750) > Threshold (500)? YES → Multi-step approval required
  │
  ├─ Step 1: Cost Centre Owner (Ops Manager Position)
  │     Does Ops Manager hold 'expenses:approve:2000'? YES
  │     Ops Manager Filled? YES → Assign Step 1
  │
  ├─ Step 2: Parent Cost Centre Owner (Finance Manager Position)
  │     Finance Manager holds 'expenses:approve:unlimited'? YES → Assign Step 2
  │
  ├─ Both steps must approve (sequential)
  ├─ Step 1 approval → Step 2 activates
  ├─ Step 2 approval → Expense Claim approved, source BC notified
  │
  ├─ Step 1 timeout (3 days) → Escalate to Finance Manager directly
  ├─ Step 2 timeout → Escalate to Executive
```

**Attendance Exception Decision Tree:**

```
Employee submits Attendance Exception (missed clock-in)
  │
  ├─ Routing Source: Work Structure Hierarchy
  ├─ Load employee's primary work structure
  │
  ├─ Work structure has supervisor position? YES → Ops Supervisor Position
  │     Filled? YES → Does supervisor hold 'attendance:approve-exception'? YES
  │     → Assign to supervisor
  │
  ├─ Supervisor Vacant? → Look at parent work structure supervisor
  ├─ No work structure? → Route to Department Head (position hierarchy fallback)
  ├─ Department Head Vacant? → Route to HR Manager
  │
  ├─ Timeout (1 business day — shorter SLA for attendance) → HR Manager
```

**Recruitment Requisition Decision Tree:**

```
Manager submits Recruitment Requisition (position: Security Officer, Grade G3)
  │
  ├─ Routing Source: Position Hierarchy
  ├─ Who above submitter holds 'recruitment:approve-hire'?
  │
  ├─ Check Department Head Position
  │     Holds 'recruitment:approve-hire'? YES → Step 1: Department Head
  │
  ├─ Grade ≥ G7 (Manager level)? NO (G3) → Single-step approval sufficient
  ├─ Grade ≥ G7? → Requires Executive co-approval → Add Step 2: Executive
  │
  ├─ Salary offer within grade band? → Checked by BC-07 Rules
  │     Exceeds band? → Flag for Finance Manager additional review
  │
  ├─ All steps approved → Vacancy opens, Recruitment BC notified
```

**Overtime Authorisation Decision Tree:**

```
Employee submits Overtime Request (3 hours, Project Alpha)
  │
  ├─ Routing Source: Work Structure Hierarchy (overtime is project-related)
  ├─ Load Project Alpha work structure
  ├─ Project Alpha Supervisor: PM Position
  │     Holds 'attendance:approve-overtime'? YES → Assign to PM
  │
  ├─ Total overtime hours this month > policy threshold (BC-07)?
  │     YES (> 20 hrs) → Requires Department Head co-approval
  │     → Add Step 2: Department Head
  │
  ├─ PM approves → Department Head approval required
  ├─ Both approve → Overtime logged to timesheet
  ├─ PM timeout (2 business days) → Escalate to Department Head directly
```

#### Escalation Logic

**Standard escalation: Timeout-based**

- SLA deadline reached with no decision → `StepEscalated` event fired
- Current step marked `Escalated`, next step activated
- Escalation level tracked on each step
- Maximum 3 escalation hops. Beyond that → `EscalationExhausted`

**Non-standard escalation: Authority exceeded**

- Occurs during resolution: a request requires a capability that no position in the reporting chain holds
- System immediately routes to the designated fallback position (HR Manager / Finance Manager) without waiting for timeout
- Logged as `ImmediateEscalation` in audit trail

**Non-standard escalation: Position vacant**

- Occurs during resolution: the resolved approver position is Vacant
- System immediately skips to the next position up the hierarchy
- Logged as `VacancyEscalation`

**Non-standard escalation: Acting assignment active**

- The position has ActingCoverage: the acting employee holds full position authority
- Request assigned to acting employee's employeeId (not the original holder)
- Logged as `ActingApprover` in the step

#### Domain Events

| Event | Payload | Consumers |
| --- | --- | --- |
| `ApprovalRequested` | requestId, requestType, sourceId, submitterId, stepId, approverId, deadline | BC-17 Notifications |
| `ApprovalGranted` | requestId, stepId, approverId, positionId, decisionAt, notes | Source BC, Notifications, Audit Log |
| `ApprovalRejected` | requestId, stepId, approverId, positionId, decisionAt, reason | Source BC, Notifications, Audit Log |
| `ApprovalEscalated` | requestId, stepId, fromPositionId, toPositionId, reason, escalationLevel | Notifications, HR Dashboard |
| `EscalationExhausted` | requestId, totalEscalations | HR Dashboard (manual flag), Notifications |
| `ApprovalWithdrawn` | requestId, withdrawnBy, withdrawnAt | Source BC, Audit Log |
| `ApprovalDeadlineMissed` | requestId, stepId, deadline | BC-06 internal (triggers escalation) |

#### API Contracts

`POST /api/approvals` — Submit approval request (called by source BCs internally, not directly by users) Request: `{ requestType, sourceId, submitterEmployeeId, submitterPositionInstanceId, metadata }` Response 201: `{ requestId, chainId, currentApproverEmployeeId, deadline }`

`GET /api/approvals/pending` — Get pending approvals for the calling user — requires auth Response: list of pending approval requests where the calling user is the current step approver

`POST /api/approvals/{id}/approve` — Approve — requires the matching capability for the request type Request: `{ notes? }` Response 200: `{ requestId, status, nextStep? }`

`POST /api/approvals/{id}/reject` — Reject — requires the matching capability Request: `{ reason }` Response 200: `{ requestId, status }`

`POST /api/approvals/{id}/withdraw` — Withdraw (submitter only, before approval) Response 200

`GET /api/approvals/{id}/chain` — Get full approval chain with all steps — requires `reports:read` or is the submitter `GET /api/approvals?requestType=&status=&from=&to=` — List approvals (HR/Manager view) — requires `reports:read`

---

### BC-07 — Rules & Policy Engine

**Purpose:** The centralised rule store and evaluation engine. Every piece of configurable business logic in Circlate — leave entitlements, overtime thresholds, escalation timeouts, expense category limits, attendance grace periods — is stored here as a versioned policy definition. No capability BC may hardcode business rules. BC-07 provides a `PolicyEvaluator` service that other BCs call to evaluate whether an action is permitted, and what parameters apply.

**Key principle:** Rules are data, not code. HR Managers and Tenant Admins configure rules through the admin interface. When a rule changes, no deployment is needed — the new policy version takes effect on its `effectiveFrom` date.

#### Aggregates

**PolicyDefinition** (Aggregate Root)

- `policyId` Guid
- `tenantId` Guid
- `type` PolicyType enum (see categories below)
- `name` string (human-readable, e.g. `Annual Leave Policy 2026`)
- `version` int (incremented on each publish)
- `status` PolicyStatus (Draft / Active / Deprecated)
- `effectiveFrom` DateOnly
- `effectiveTo` DateOnly (nullable — null = indefinitely active)
- `scope` PolicyScope (Global / Department / EmploymentType / Grade) — which employees this policy applies to
- `scopeId` Guid (nullable — the specific department/grade the policy applies to)
- `rules` Rule\[\] (entities, evaluated in priority order)
- `createdBy` Guid (position instance)
- `publishedAt` DateTime UTC (nullable)

**Rule** (Entity — child of PolicyDefinition)

- `ruleId` Guid
- `policyId` Guid
- `name` string (e.g. `Sick leave cap — no hospitalisation`)
- `priority` int (lower number = higher priority; first matching rule wins)
- `condition` RuleCondition (VO)
- `action` RuleAction (VO)
- `isActive` bool

**PolicyEvaluationLog** (Aggregate Root — append-only)

- `logId` Guid
- `tenantId` Guid
- `policyId` Guid
- `policyVersion` int
- `evaluatedAt` DateTime UTC
- `subjectEmployeeId` Guid
- `requestContext` Dictionary\<string, string> — snapshot of the input context
- `matchedRuleId` Guid (nullable)
- `result` EvaluationResult (Allowed / Denied / Modified / Flagged)
- `resultParameters` Dictionary\<string, string> — the output values from the matched rule's action

#### Value Objects

**RuleCondition**

- `field` string — dotted path to the value being tested (e.g. `employee.tenure.years`, `leave.type`, `expense.amount`, `attendance.lateMinutes`)
- `operator` ConditionOperator enum (Equals / NotEquals / GreaterThan / GreaterThanOrEqual / LessThan / LessThanOrEqual / In / NotIn / Between / IsNull / IsNotNull)
- `value` string — JSON-serialised comparison value
- `valueHigh` string (nullable — upper bound for Between operator)

**RuleAction**

- `type` ActionType enum (Allow / Deny / Cap / SetValue / Require / Notify / Route)
- `parameters` Dictionary\<string, string> — action-specific parameters:
  - `Allow`: no parameters needed
  - `Deny`: `{ "reason": "Insufficient leave balance" }`
  - `Cap`: `{ "field": "leave.days", "maxValue": "14" }`
  - `SetValue`: `{ "field": "expense.requiresReceipt", "value": "true" }`
  - `Require`: `{ "capability": "expenses:approve:unlimited" }` — escalates to that approver level
  - `Notify`: `{ "capability": "hr.manager", "message": "Overtime threshold exceeded" }`
  - `Route`: `{ "toProfile": "hr-manager" }` — override approval routing

#### Policy Categories

**LeavePolicy** (`PolicyType.Leave`) Configures leave entitlement amounts, accrual, carry-over, and eligibility.

Example rules:

| Priority | Condition | Action |
| --- | --- | --- |
| 1 | `leave.type == Annual AND employee.tenure.years < 2` | SetValue: `entitlementDays = 7` |
| 2 | `leave.type == Annual AND employee.tenure.years BETWEEN 2 AND 5` | SetValue: `entitlementDays = 8` |
| 3 | `leave.type == Annual AND employee.tenure.years > 5` | SetValue: `entitlementDays = 10` |
| 4 | `leave.type == Sick AND hospitalisation == false` | Cap: `leave.days <= 14` |
| 5 | `leave.type == Sick AND hospitalisation == true` | Cap: `leave.days <= 60` |
| 6 | `leave.type == Maternity AND employee.tenure.days >= 180` | SetValue: `entitlementDays = 105` (15 weeks) |
| 7 | `leave.type == Annual AND leave.days > carryOverMax` | Deny: `"Carry-over limit exceeded"` |
| 8 | `leave.startDate IN publicHolidays` | Notify: HR Manager |

**OvertimePolicy** (`PolicyType.Overtime`) Controls overtime eligibility, rate multipliers, and approval thresholds.

| Priority | Condition | Action |
| --- | --- | --- |
| 1 | `employee.grade IN [G1, G2, G3, G4]` | SetValue: `overtimeRate = 1.5` |
| 2 | `employee.grade IN [G5, G6]` | SetValue: `overtimeRate = 1.0` |
| 3 | `employee.grade >= G7` | Deny: `"Managers not eligible for overtime"` |
| 4 | `overtime.monthlyHours > 20` | Require: `attendance:approve-overtime` at department-head level |
| 5 | `overtime.dayType == PublicHoliday` | SetValue: `overtimeRate = 2.0` |

**AttendancePolicy** (`PolicyType.Attendance`) Defines shift grace periods, late arrival thresholds, and absence rules.

| Priority | Condition | Action |
| --- | --- | --- |
| 1 | `attendance.lateMinutes <= 15` | Allow: grace period, no exception required |
| 2 | `attendance.lateMinutes BETWEEN 16 AND 60` | Require: attendance exception submission |
| 3 | `attendance.lateMinutes > 60` | Require: exception + Notify supervisor |
| 4 | `attendance.missedClockIn == true` | Require: exception + Route to work structure supervisor |
| 5 | `attendance.consecutiveAbsenceDays >= 3` | Notify: HR Manager |

**ExpensePolicy** (`PolicyType.Expense`) Sets category limits, receipt requirements, and pre-approval thresholds.

| Priority | Condition | Action |
| --- | --- | --- |
| 1 | `expense.amount > 50 AND expense.receipt == null` | Deny: `"Receipt required for claims over BND 50"` |
| 2 | `expense.category == Entertainment AND expense.amount > 200` | Require: pre-approval before submission |
| 3 | `expense.category == Travel AND expense.amount > 500` | Require: `expenses:approve:2000` capability |
| 4 | `expense.amount > 1000` | SetValue: `requiresFinanceReview = true` |

**ApprovalPolicy** (`PolicyType.Approval`) Configures escalation timeouts per request type and approval deadlines.

| Priority | Condition | Action |
| --- | --- | --- |
| 1 | `approval.requestType == Leave` | SetValue: `deadlineBusinessDays = 3` |
| 2 | `approval.requestType == ExpenseClaim` | SetValue: `deadlineBusinessDays = 5` |
| 3 | `approval.requestType == AttendanceException` | SetValue: `deadlineBusinessDays = 1` |
| 4 | `approval.requestType == RecruitmentRequisition` | SetValue: `deadlineBusinessDays = 7` |
| 5 | `approval.escalationLevel >= 3` | Route: HR Manager + Notify: Tenant Admin |

**CompliancePolicy** (`PolicyType.Compliance`) Defines certification validity rules and renewal warnings.

| Priority | Condition | Action |
| --- | --- | --- |
| 1 | `compliance.type == HSECertification AND daysToExpiry <= 30` | Notify: employee + HR Manager |
| 2 | `compliance.type == SecurityClearance AND daysToExpiry <= 60` | Notify: HR Manager |
| 3 | `compliance.status == Expired AND assignment.mandatory == true` | Deny: assignment activation |

#### Rule Evaluation Flow

When a capability BC needs to evaluate a rule (e.g., Leave BC checking leave entitlement):

1. **Build EvaluationContext**
   - Caller provides: `tenantId`, `employeeId`, `policyType`, and a context dictionary of relevant field values (`{ "leave.type": "Annual", "employee.tenure.years": "3.5", ... }`)
2. **Load active PolicyDefinition**
   - Find the `Active` policy of the matching `type` whose `effectiveFrom ≤ today < effectiveTo (if set)` and whose `scope` applies to the employee (global policies first, then department-specific overrides)
   - If multiple active policies match scope: more specific scope wins (Department > EmploymentType > Grade > Global)
3. **Evaluate rules in priority order**
   - For each `Rule` (sorted by `priority` ASC):
     - Evaluate `condition.field` against the context
     - Apply `condition.operator` with `condition.value`
     - If condition matches: take the action. Stop (first match wins, unless action type is `Notify` — notifications are non-stopping)
   - If no rule matches: return `EvaluationResult.Allowed` with no modifications (permissive default)
4. **Build EvaluationResult**
   - `result`: Allowed / Denied / Modified / Flagged
   - `resultParameters`: output values from the matched action
   - `matchedRuleId`: for audit trail
5. **Persist PolicyEvaluationLog** (async, does not block the caller)
6. **Return result to caller**
   - Caller BC acts on the result: proceeds, blocks the action, or applies the modified parameter values

#### Event Integration

BC-07 fires events that other BCs consume:

| Event | Payload | Consumers |
| --- | --- | --- |
| `PolicyActivated` | policyId, type, version, effectiveFrom | All BCs that evaluate this policy type (invalidate policy cache) |
| `PolicyDeprecated` | policyId, type | All BCs (invalidate cache) |
| `RuleViolation` | policyId, ruleId, employeeId, context | BC-17 Notifications (if Notify action), Audit Log |
| `PolicyEvaluated` | logId, policyId, result | Audit Log (async) |

#### Administration Model

**SME Configuration (Simple Mode)** For tenants with standard requirements, Circlate provides pre-built policy templates conforming to Brunei Employment Order 2009 defaults. HR Manager activates these with a single toggle. No rule editing required.

Pre-built templates:

- `Brunei Employment Order — Leave Entitlements (2024)` — Annual/Sick/Maternity leave per tenure
- `Standard Expense Policy — BND` — Receipt thresholds, common category limits
- `Standard Overtime Policy` — Eligibility by grade, 1.5x/2x rates
- `Standard Approval SLAs` — 3-day leave, 5-day expense, 1-day attendance

**Enterprise Configuration (Advanced Mode)** For tenants requiring customisation, every rule set is editable. HR Manager or Tenant Admin can:

- Create new policy definitions
- Add, edit, reorder rules within a definition
- Set scope overrides (department-specific leave policies)
- Preview rule evaluation against a test employee before publishing
- Schedule future activation (policy takes effect on a future `effectiveFrom` date)
- Deprecate old policies with a transition period

**Policy versioning:** Every published policy is immutable. Editing creates a new version. Old versions are retained for audit purposes — a `PolicyEvaluationLog` always records which version was active at evaluation time.

#### Domain Events

| Event | Payload | Consumers |
| --- | --- | --- |
| `PolicyCreated` | policyId, tenantId, type, name | Audit Log |
| `PolicyPublished` | policyId, type, version, effectiveFrom | All relevant BCs (cache invalidation) |
| `PolicyActivated` | policyId, type, version | All relevant BCs |
| `PolicyDeprecated` | policyId, type, deprecatedAt | All relevant BCs |
| `RuleAdded` | policyId, ruleId, priority, condition, action | Audit Log |
| `RuleRemoved` | policyId, ruleId | Audit Log |

#### API Contracts

`GET /api/policies` — List policies (filterable by type, status) — requires `rules:read` `POST /api/policies` — Create policy definition — requires `rules:write` Request: `{ type, name, effectiveFrom, effectiveTo?, scope, scopeId? }` `GET /api/policies/{id}` — Get with all rules — requires `rules:read` `PUT /api/policies/{id}/rules` — Replace all rules — requires `rules:write` Request: `{ rules: [{ name, priority, condition: { field, operator, value, valueHigh? }, action: { type, parameters } }] }` `POST /api/policies/{id}/publish` — Publish policy — requires `rules:write` `POST /api/policies/{id}/deprecate` — Deprecate — requires `rules:write`

`POST /api/policies/evaluate` — Preview evaluation (dry run, not logged) — requires `rules:read` Request: `{ policyType, employeeId, context: { field: value } }` Response: `{ result, resultParameters, matchedRuleName, matchedRuleId? }`

`GET /api/policies/templates` — List available pre-built templates — requires `rules:read` `POST /api/policies/templates/{templateId}/activate` — Activate a pre-built template — requires `rules:write`

`GET /api/policy-evaluation-log` — Query evaluation history — requires `reports:read` Query params: `employeeId?, policyId?, from?, to?, result?`

---

### Foundation Domain Events Catalogue

All events are published to an internal event bus (MediatR in-process for Phase 1; migrable to a message broker in Phase 3). Events are ordered within a single BC — across BCs they are eventually consistent. All events carry `tenantId` and `occurredAt` (UTC) in addition to the specific payload fields listed below.

#### BC-01 Identity Events

| Event | Producer | Consumers | Business Purpose | Ordering Constraint |
| --- | --- | --- | --- | --- |
| `UserCreated` | BC-01 | BC-05 Employees | An account was created; employee onboarding may start | None |
| `UserSuspended` | BC-01 | BC-17 Notifications, Audit | User loses system access immediately | Must follow no pending UserCreated |
| `UserReactivated` | BC-01 | BC-17 Notifications, Audit | Access restored | Must follow UserSuspended |
| `PasswordChanged` | BC-01 | Audit | Security record | None |
| `MfaDeviceEnrolled` | BC-01 | Audit | Security posture change | None |
| `SessionRevoked` | BC-01 | Audit | Active session terminated | None |
| `TenantMembershipCreated` | BC-01 | BC-05 Employees | Tenant account linked to employee | Requires UserCreated to have fired |
| `ApiKeyIssued` | BC-01 | Audit | M2M credential created | None |
| `ApiKeyRevoked` | BC-01 | Audit | M2M credential disabled | Must follow ApiKeyIssued |

#### BC-02 Organisation Events

| Event | Producer | Consumers | Business Purpose | Ordering Constraint |
| --- | --- | --- | --- | --- |
| `OrganisationCreated` | BC-02 | BC-01, BC-07 | Tenant org initialised | First event in tenant lifecycle |
| `BusinessUnitCreated` | BC-02 | BC-04, BC-05 | New structural node added | Requires OrganisationCreated |
| `BusinessUnitMoved` | BC-02 | BC-04, BC-06, Audit | Hierarchy restructure | BC-04 must invalidate position reporting lines |
| `DepartmentCreated` | BC-02 | BC-04, Reports | New department exists | Requires BusinessUnitCreated |
| `DepartmentHeadAssigned` | BC-02 | BC-17 Notifications | Leadership change | Requires PositionAssigned in BC-04 |
| `CostCentreCreated` | BC-02 | BC-06 Routing | New budget node created | None |
| `CostCentreOwnerChanged` | BC-02 | BC-06 | Routing cache must be invalidated | None |
| `PublicHolidayCalendarPublished` | BC-02 | BC-08 Leave, BC-07 Rules | Holiday dates available for leave calculations | Must fire before leave year begins |

#### BC-03 Authority & Delegation Events

| Event | Producer | Consumers | Business Purpose | Ordering Constraint |
| --- | --- | --- | --- | --- |
| `AuthorityProfileCreated` | BC-03 | BC-04 | Profile available to assign to positions | None |
| `AuthorityProfilePublished` | BC-03 | BC-04, BC-06 | Capabilities locked in; can now be assigned | Must follow AuthorityProfileCreated |
| `AuthorityProfileAssigned` | BC-03 | BC-01 (JWT refresh), BC-06 | Position now carries a new capability set | BC-04 PositionInstance must exist |
| `AuthorityProfileRevoked` | BC-03 | BC-01, BC-06 | Position loses authority; active approvals may be affected | BC-06 must re-route pending steps |
| `DelegationCreated` | BC-03 | BC-06, BC-17 | Delegation record registered | None |
| `DelegationActivated` | BC-03 | BC-01 (temp caps), BC-06 | Delegate now has temporary capabilities | Must follow DelegationCreated |
| `DelegationExpired` | BC-03 | BC-01, BC-06, BC-17 | Delegation period ended; capabilities revert | Must follow DelegationActivated |
| `DelegationRevoked` | BC-03 | BC-01, BC-06, BC-17 | Manual early termination | Must follow DelegationActivated |

#### BC-04 Position Management Events

| Event | Producer | Consumers | Business Purpose | Ordering Constraint |
| --- | --- | --- | --- | --- |
| `PositionTemplateCreated` | BC-04 | BC-06 | New position type exists | Requires BC-02 DepartmentCreated |
| `PositionEstablishmentApproved` | BC-04 | BC-17, Reports | Headcount budget approved for the year | Requires PositionTemplateCreated |
| `PositionInstanceCreated` | BC-04 | BC-06 | A specific slot is open to be filled | Requires PositionEstablishmentApproved |
| `PositionAssigned` | BC-04 | BC-01 (JWT), BC-03, BC-05, BC-17 | Employee now occupies the position and inherits its authority | Requires PositionInstanceCreated, EmployeeCreated |
| `PositionVacated` | BC-04 | BC-06 (escalate pending approvals), BC-01, BC-17 | Authority is removed; in-flight approvals must be redirected | BC-06 must immediately escalate all pending steps for this position |
| `PositionTransferred` | BC-04 | BC-01, BC-06, BC-17 | Lateral move; authority changes | Must follow PositionAssigned on new instance |
| `ActingAssignmentActivated` | BC-04 | BC-01 (temp authority), BC-06, BC-17 | Acting employee now holds position authority | BC-01 must refresh acting employee's JWT before first approval action |
| `ActingAssignmentCompleted` | BC-04 | BC-01 (revert), BC-17 | Acting period over; authority reverts | Must follow ActingAssignmentActivated |
| `ReportingLineChanged` | BC-04 | BC-06 | Approval chains must be recomputed | BC-06 routing cache invalidated |

#### BC-05 Work Structure Events

| Event | Producer | Consumers | Business Purpose | Ordering Constraint |
| --- | --- | --- | --- | --- |
| `WorkStructureCreated` | BC-05 | BC-06 | Operational unit exists | Requires BC-02 DepartmentCreated or BC-04 PositionInstanceCreated |
| `WorkStructureActivated` | BC-05 | BC-17 | Work has begun | Must follow WorkStructureCreated |
| `WorkStructureCompleted` | BC-05 | BC-06, Reports | Operational unit closed | BC-06 ends any routing via this work structure |
| `WorkStructureSupervisorChanged` | BC-05 | BC-06 | Supervisor routing must be re-resolved | BC-06 routing cache invalidated |
| `EmployeeAssignedToWorkStructure` | BC-05 | BC-06, BC-17 | Employee joins the operational unit | Requires BC-04 PositionAssigned |
| `EmployeeRemovedFromWorkStructure` | BC-05 | BC-06 | Employee leaves the operational unit | BC-06 routing updated |
| `ProjectAllocationChanged` | BC-05 | Reports, BC-06 | Cost allocation changes | None |
| `ComplianceRequirementSatisfied` | BC-05 | BC-05 (activate assignment), BC-17 | Blocking requirement cleared | Requires ComplianceRequirementAdded |
| `ComplianceRequirementExpired` | BC-05 | BC-17, HR Dashboard | Renewal needed | Requires ComplianceRequirementSatisfied |

#### BC-06 Approval Routing Events

| Event | Producer | Consumers | Business Purpose | Ordering Constraint |
| --- | --- | --- | --- | --- |
| `ApprovalRequested` | BC-06 | BC-17 | Approver must be notified | None |
| `ApprovalGranted` | BC-06 | Source BC (Leave/Expense/etc.), BC-17, Audit | Approval action taken | Must follow ApprovalRequested |
| `ApprovalRejected` | BC-06 | Source BC, BC-17, Audit | Rejection action taken | Must follow ApprovalRequested |
| `ApprovalEscalated` | BC-06 | BC-17, HR Dashboard | Timeout escalation occurred | Requires ApprovalDeadlineMissed |
| `EscalationExhausted` | BC-06 | HR Dashboard, BC-17 | 3-hop limit reached; manual intervention | Requires 3× ApprovalEscalated |
| `ApprovalWithdrawn` | BC-06 | Source BC, Audit | Submitter retracted request | None |
| `ApprovalDeadlineMissed` | BC-06 (scheduled check) | BC-06 internal | Triggers escalation logic | None |

#### BC-07 Rules & Policy Engine Events

| Event | Producer | Consumers | Business Purpose | Ordering Constraint |
| --- | --- | --- | --- | --- |
| `PolicyActivated` | BC-07 | All BCs (cache invalidate) | New rules are live | Must follow PolicyPublished |
| `PolicyDeprecated` | BC-07 | All BCs | Old rules no longer apply | Must follow PolicyActivated |
| `RuleViolation` | BC-07 | BC-17 Notifications, Audit | An action violated a business rule | Fired during evaluation |
| `PolicyEvaluated` | BC-07 | Audit Log | Audit record of rule application | Async; non-blocking |

#### Cross-BC Ordering Dependencies

The following sequences are hard ordering dependencies. Violation causes referential integrity failures:

1. `OrganisationCreated` → `BusinessUnitCreated` → `DepartmentCreated` → `PositionTemplateCreated` → `PositionEstablishmentApproved` → `PositionInstanceCreated`
2. `UserCreated` → `TenantMembershipCreated` → `PositionAssigned` (links user to position)
3. `AuthorityProfileCreated` → `AuthorityProfilePublished` → `AuthorityProfileAssigned` → `PositionAssigned`
4. `PositionAssigned` → `EmployeeAssignedToWorkStructure`
5. `ActingAssignmentActivated` → (BC-01 JWT refresh) → first approval action by acting employee
6. `PositionVacated` → (BC-06 escalates pending approvals) → `ApprovalEscalated`

---

### Foundation ERD

All Foundation tables reside in the **tenant database** (one per company) except `users`, `tenant_memberships`, and `service_accounts` which reside in the **platform database**. Column types are PostgreSQL. All primary keys are `UUID`. All tables include `created_at TIMESTAMPTZ NOT NULL DEFAULT now()` unless noted.

#### Platform Database Tables (BC-01 Identity)

```sql
CREATE TABLE users (
  user_id         UUID PRIMARY KEY,
  tenant_id       UUID NOT NULL,
  email           TEXT NOT NULL,
  display_name    TEXT NOT NULL,
  status          TEXT NOT NULL CHECK (status IN ('PendingVerification','Active','Suspended','Deactivated')),
  employee_id     UUID,                        -- set after onboarding in tenant DB
  password_changed_at  TIMESTAMPTZ,
  last_login_at   TIMESTAMPTZ,
  created_at      TIMESTAMPTZ NOT NULL DEFAULT now(),
  UNIQUE (tenant_id, email)
);
CREATE INDEX idx_users_tenant ON users (tenant_id);

CREATE TABLE mfa_devices (
  device_id       UUID PRIMARY KEY,
  user_id         UUID NOT NULL REFERENCES users(user_id),
  type            TEXT NOT NULL CHECK (type IN ('TOTP','SMS','Email')),
  device_label    TEXT NOT NULL,
  totp_secret_enc TEXT,                        -- AES-256 encrypted; NULL for non-TOTP
  enrolled_at     TIMESTAMPTZ NOT NULL,
  last_used_at    TIMESTAMPTZ,
  is_default      BOOLEAN NOT NULL DEFAULT false,
  revoked_at      TIMESTAMPTZ
);
CREATE INDEX idx_mfa_user ON mfa_devices (user_id);

CREATE TABLE active_sessions (
  session_id          UUID PRIMARY KEY,
  user_id             UUID NOT NULL REFERENCES users(user_id),
  device_type         TEXT NOT NULL CHECK (device_type IN ('Web','Mobile','API')),
  refresh_token_hash  TEXT NOT NULL,
  issued_at           TIMESTAMPTZ NOT NULL,
  expires_at          TIMESTAMPTZ NOT NULL,
  revoked_at          TIMESTAMPTZ
);
CREATE INDEX idx_sessions_user ON active_sessions (user_id);
CREATE INDEX idx_sessions_hash ON active_sessions (refresh_token_hash);

CREATE TABLE service_accounts (
  service_account_id  UUID PRIMARY KEY,
  tenant_id           UUID NOT NULL,
  name                TEXT NOT NULL,
  scopes              TEXT[] NOT NULL DEFAULT '{}',
  status              TEXT NOT NULL CHECK (status IN ('Active','Revoked')),
  created_at          TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE api_keys (
  key_id              UUID PRIMARY KEY,
  service_account_id  UUID NOT NULL REFERENCES service_accounts(service_account_id),
  key_prefix          TEXT NOT NULL,
  key_hash            TEXT NOT NULL,
  created_at          TIMESTAMPTZ NOT NULL DEFAULT now(),
  expires_at          TIMESTAMPTZ,
  last_used_at        TIMESTAMPTZ,
  revoked_at          TIMESTAMPTZ
);
CREATE UNIQUE INDEX idx_api_keys_hash ON api_keys (key_hash);

CREATE TABLE tenant_memberships (
  membership_id   UUID PRIMARY KEY,
  user_id         UUID NOT NULL REFERENCES users(user_id),
  tenant_id       UUID NOT NULL,
  role            TEXT NOT NULL CHECK (role IN ('TenantAdmin','HRManager','Employee','ReadOnly')),
  status          TEXT NOT NULL CHECK (status IN ('Active','Suspended')),
  invited_at      TIMESTAMPTZ NOT NULL,
  accepted_at     TIMESTAMPTZ,
  UNIQUE (user_id, tenant_id)
);
CREATE INDEX idx_memberships_tenant ON tenant_memberships (tenant_id);
```

#### Tenant Database Tables (BC-02 Organisation)

```sql
CREATE TABLE organisations (
  organisation_id         UUID PRIMARY KEY,
  tenant_id               UUID NOT NULL UNIQUE,
  legal_name              TEXT NOT NULL,
  trading_name            TEXT,
  registration_number     TEXT,
  country_code            CHAR(2) NOT NULL,
  default_currency        CHAR(3) NOT NULL DEFAULT 'BND',
  timezone                TEXT NOT NULL DEFAULT 'Asia/Brunei',
  fiscal_year_start_month SMALLINT NOT NULL DEFAULT 1 CHECK (fiscal_year_start_month BETWEEN 1 AND 12),
  status                  TEXT NOT NULL DEFAULT 'Active'
);

CREATE TABLE business_units (
  business_unit_id        UUID PRIMARY KEY,
  tenant_id               UUID NOT NULL,
  organisation_id         UUID NOT NULL REFERENCES organisations(organisation_id),
  parent_business_unit_id UUID REFERENCES business_units(business_unit_id),
  name                    TEXT NOT NULL,
  code                    TEXT NOT NULL,
  type                    TEXT NOT NULL CHECK (type IN ('Division','Region','Branch','Site','Subsidiary')),
  country_code            CHAR(2),
  hierarchy_path          TEXT NOT NULL,         -- materialised path e.g. /org-id/bu-id/
  status                  TEXT NOT NULL DEFAULT 'Active',
  UNIQUE (tenant_id, code)
);
CREATE INDEX idx_bu_tenant ON business_units (tenant_id);
CREATE INDEX idx_bu_path ON business_units USING gist (hierarchy_path gist_trgm_ops);

CREATE TABLE departments (
  department_id       UUID PRIMARY KEY,
  tenant_id           UUID NOT NULL,
  business_unit_id    UUID NOT NULL REFERENCES business_units(business_unit_id),
  name                TEXT NOT NULL,
  code                TEXT NOT NULL,
  head_position_id    UUID,                      -- FK to position_instances (nullable until BC-04 live)
  cost_centre_id      UUID,                      -- FK to cost_centres (nullable)
  status              TEXT NOT NULL DEFAULT 'Active',
  UNIQUE (tenant_id, code)
);
CREATE INDEX idx_dept_tenant ON departments (tenant_id);

CREATE TABLE cost_centres (
  cost_centre_id          UUID PRIMARY KEY,
  tenant_id               UUID NOT NULL,
  code                    TEXT NOT NULL,
  name                    TEXT NOT NULL,
  parent_cost_centre_id   UUID REFERENCES cost_centres(cost_centre_id),
  owner_position_id       UUID,                  -- FK to position_instances
  approval_threshold      NUMERIC(12,2),
  currency                CHAR(3) NOT NULL DEFAULT 'BND',
  status                  TEXT NOT NULL DEFAULT 'Active',
  UNIQUE (tenant_id, code)
);

CREATE TABLE public_holiday_calendars (
  calendar_id  UUID PRIMARY KEY,
  tenant_id    UUID NOT NULL,
  year         SMALLINT NOT NULL,
  country_code CHAR(2) NOT NULL,
  status       TEXT NOT NULL CHECK (status IN ('Draft','Published')),
  UNIQUE (tenant_id, year, country_code)
);

CREATE TABLE public_holiday_entries (
  entry_id              UUID PRIMARY KEY,
  calendar_id           UUID NOT NULL REFERENCES public_holiday_calendars(calendar_id) ON DELETE CASCADE,
  date                  DATE NOT NULL,
  name                  TEXT NOT NULL,
  type                  TEXT NOT NULL CHECK (type IN ('National','Religious','Regional','Substitute')),
  applicable_regions    TEXT[]
);
CREATE INDEX idx_holiday_calendar ON public_holiday_entries (calendar_id);
CREATE INDEX idx_holiday_date ON public_holiday_entries (calendar_id, date);
```

#### Tenant Database Tables (BC-03 Authority & Delegation)

```sql
CREATE TABLE authority_profiles (
  profile_id    UUID PRIMARY KEY,
  tenant_id     UUID NOT NULL,
  name          TEXT NOT NULL,
  version       INT NOT NULL DEFAULT 1,
  status        TEXT NOT NULL CHECK (status IN ('Draft','Active','Deprecated')),
  published_at  TIMESTAMPTZ
);
CREATE INDEX idx_ap_tenant ON authority_profiles (tenant_id);

CREATE TABLE authority_entries (
  entry_id              UUID PRIMARY KEY,
  profile_id            UUID NOT NULL REFERENCES authority_profiles(profile_id) ON DELETE CASCADE,
  authority_name        TEXT NOT NULL,
  capability            TEXT NOT NULL,
  financial_threshold   NUMERIC(12,2),
  scope                 TEXT NOT NULL CHECK (scope IN ('Own','Team','Department','Organisation')),
  notes                 TEXT
);
CREATE INDEX idx_ae_profile ON authority_entries (profile_id);
CREATE INDEX idx_ae_capability ON authority_entries (capability);

CREATE TABLE delegation_records (
  delegation_id               UUID PRIMARY KEY,
  tenant_id                   UUID NOT NULL,
  from_position_instance_id   UUID NOT NULL,
  to_position_instance_id     UUID NOT NULL,
  authority_entries           TEXT[] NOT NULL,   -- capability strings being delegated
  reason                      TEXT NOT NULL,
  start_date                  DATE NOT NULL,
  end_date                    DATE NOT NULL,
  status                      TEXT NOT NULL CHECK (status IN ('Pending','Active','Expired','Revoked')),
  authorised_by_position_id   UUID NOT NULL,
  revoked_at                  TIMESTAMPTZ,
  CHECK (end_date > start_date)
);
CREATE INDEX idx_del_from_pos ON delegation_records (from_position_instance_id, status);
CREATE INDEX idx_del_to_pos ON delegation_records (to_position_instance_id, status);
```

#### Tenant Database Tables (BC-04 Position Management)

```sql
CREATE TABLE position_grades (
  grade_id        UUID PRIMARY KEY,
  tenant_id       UUID NOT NULL,
  code            TEXT NOT NULL,          -- 'G1' to 'G10'
  label           TEXT NOT NULL,
  min_salary      NUMERIC(12,2) NOT NULL,
  max_salary      NUMERIC(12,2) NOT NULL,
  midpoint        NUMERIC(12,2) NOT NULL,
  currency        CHAR(3) NOT NULL,
  leave_days      SMALLINT NOT NULL,
  notice_period_days SMALLINT NOT NULL,
  UNIQUE (tenant_id, code)
);

CREATE TABLE position_templates (
  template_id                 UUID PRIMARY KEY,
  tenant_id                   UUID NOT NULL,
  title                       TEXT NOT NULL,
  code                        TEXT NOT NULL,
  department_id               UUID NOT NULL REFERENCES departments(department_id),
  grade_id                    UUID NOT NULL REFERENCES position_grades(grade_id),
  default_authority_profile_id UUID REFERENCES authority_profiles(profile_id),
  job_description             TEXT,
  responsibilities            TEXT[],
  required_skill_ids          UUID[],
  required_certification_ids  UUID[],
  deputy_template_id          UUID REFERENCES position_templates(template_id),
  reporting_to_template_id    UUID REFERENCES position_templates(template_id),
  status                      TEXT NOT NULL CHECK (status IN ('Draft','Active','Deprecated')),
  UNIQUE (tenant_id, code)
);
CREATE INDEX idx_pt_dept ON position_templates (department_id);

CREATE TABLE position_establishments (
  establishment_id            UUID PRIMARY KEY,
  tenant_id                   UUID NOT NULL,
  position_template_id        UUID NOT NULL REFERENCES position_templates(template_id),
  department_id               UUID NOT NULL REFERENCES departments(department_id),
  effective_year              SMALLINT NOT NULL,
  approved_headcount          SMALLINT NOT NULL CHECK (approved_headcount > 0),
  budget_line_code            TEXT,
  approved_by_position_id     UUID,
  status                      TEXT NOT NULL CHECK (status IN ('Draft','Approved','Frozen')),
  UNIQUE (tenant_id, position_template_id, department_id, effective_year)
);

CREATE TABLE position_instances (
  instance_id                 UUID PRIMARY KEY,
  tenant_id                   UUID NOT NULL,
  position_template_id        UUID NOT NULL REFERENCES position_templates(template_id),
  establishment_id            UUID NOT NULL REFERENCES position_establishments(establishment_id),
  effective_authority_profile_id UUID REFERENCES authority_profiles(profile_id),
  reporting_to_instance_id    UUID REFERENCES position_instances(instance_id),
  status                      TEXT NOT NULL CHECK (status IN ('Vacant','Filled','ActingCoverage'))
);
CREATE INDEX idx_pi_template ON position_instances (position_template_id);
CREATE INDEX idx_pi_reporting ON position_instances (reporting_to_instance_id);

CREATE TABLE position_occupancies (
  occupancy_id    UUID PRIMARY KEY,
  instance_id     UUID NOT NULL REFERENCES position_instances(instance_id),
  employee_id     UUID NOT NULL,
  type            TEXT NOT NULL CHECK (type IN ('Substantive','Acting')),
  start_date      DATE NOT NULL,
  end_date        DATE,
  end_reason      TEXT CHECK (end_reason IN ('Resignation','Transfer','Termination','ActingEnded','Retirement') OR end_reason IS NULL)
);
CREATE INDEX idx_occ_instance ON position_occupancies (instance_id);
CREATE INDEX idx_occ_employee ON position_occupancies (employee_id);
CREATE INDEX idx_occ_current ON position_occupancies (instance_id) WHERE end_date IS NULL;

CREATE TABLE acting_assignments (
  acting_assignment_id        UUID PRIMARY KEY,
  tenant_id                   UUID NOT NULL,
  target_instance_id          UUID NOT NULL REFERENCES position_instances(instance_id),
  covering_employee_id        UUID NOT NULL,
  covering_from_instance_id   UUID NOT NULL REFERENCES position_instances(instance_id),
  compensation_method         TEXT NOT NULL CHECK (compensation_method IN ('None','FixedAllowance','PercentageUplift','PositionDifferential')),
  compensation_value          NUMERIC(12,2),
  compensation_currency       CHAR(3),
  start_date                  DATE NOT NULL,
  end_date                    DATE NOT NULL,
  reason                      TEXT NOT NULL,
  authorised_by_position_id   UUID NOT NULL,
  status                      TEXT NOT NULL CHECK (status IN ('Pending','Active','Completed','Cancelled')),
  audit_approval_required     BOOLEAN NOT NULL DEFAULT false,
  CHECK (end_date > start_date)
);
CREATE INDEX idx_aa_target ON acting_assignments (target_instance_id, status);
CREATE INDEX idx_aa_covering ON acting_assignments (covering_employee_id, status);
```

#### Tenant Database Tables (BC-05 Work Structures)

```sql
CREATE TABLE work_structures (
  work_structure_id               UUID PRIMARY KEY,
  tenant_id                       UUID NOT NULL,
  type                            TEXT NOT NULL CHECK (type IN ('Team','Project','Programme','Site','Contract','TaskForce','Committee')),
  name                            TEXT NOT NULL,
  code                            TEXT NOT NULL,
  parent_work_structure_id        UUID REFERENCES work_structures(work_structure_id),
  supervisor_position_instance_id UUID REFERENCES position_instances(instance_id),
  cost_centre_id                  UUID REFERENCES cost_centres(cost_centre_id),
  department_id                   UUID REFERENCES departments(department_id),
  start_date                      DATE,
  end_date                        DATE,
  status                          TEXT NOT NULL CHECK (status IN ('Planning','Active','OnHold','Completed','Cancelled')),
  UNIQUE (tenant_id, code)
);
CREATE INDEX idx_ws_tenant ON work_structures (tenant_id, status);
CREATE INDEX idx_ws_parent ON work_structures (parent_work_structure_id);

CREATE TABLE work_structure_assignments (
  assignment_id           UUID PRIMARY KEY,
  tenant_id               UUID NOT NULL,
  work_structure_id       UUID NOT NULL REFERENCES work_structures(work_structure_id),
  employee_id             UUID NOT NULL,
  role                    TEXT NOT NULL CHECK (role IN ('Member','Lead','Coordinator','Supervisor','Observer')),
  allocation_percentage   NUMERIC(5,4) NOT NULL CHECK (allocation_percentage > 0 AND allocation_percentage <= 1),
  start_date              DATE NOT NULL,
  end_date                DATE,
  is_primary              BOOLEAN NOT NULL DEFAULT false,
  status                  TEXT NOT NULL CHECK (status IN ('Pending','Active','Completed','Cancelled')),
  compliance_status       TEXT NOT NULL DEFAULT 'Compliant' CHECK (compliance_status IN ('Compliant','PendingRequirements','NonCompliant'))
);
CREATE INDEX idx_wsa_ws ON work_structure_assignments (work_structure_id, status);
CREATE INDEX idx_wsa_employee ON work_structure_assignments (employee_id, status);

CREATE TABLE work_structure_compliance_requirements (
  requirement_id          UUID PRIMARY KEY,
  work_structure_id       UUID NOT NULL REFERENCES work_structures(work_structure_id) ON DELETE CASCADE,
  type                    TEXT NOT NULL,
  name                    TEXT NOT NULL,
  mandatory               BOOLEAN NOT NULL DEFAULT true,
  validity_period_days    INT,
  verification_required   BOOLEAN NOT NULL DEFAULT false
);

CREATE TABLE employee_compliance_records (
  record_id               UUID PRIMARY KEY,
  tenant_id               UUID NOT NULL,
  employee_id             UUID NOT NULL,
  requirement_id          UUID NOT NULL REFERENCES work_structure_compliance_requirements(requirement_id),
  work_structure_id       UUID NOT NULL REFERENCES work_structures(work_structure_id),
  satisfied_at            TIMESTAMPTZ,
  expires_at              TIMESTAMPTZ,
  evidence_document_id    UUID,
  status                  TEXT NOT NULL CHECK (status IN ('Pending','Satisfied','Expired','Waived')),
  waived_by               UUID,
  waived_reason           TEXT
);
CREATE INDEX idx_ecr_employee ON employee_compliance_records (employee_id, status);
```

#### Tenant Database Tables (BC-06 Approval Routing)

```sql
CREATE TABLE approval_requests (
  request_id                      UUID PRIMARY KEY,
  tenant_id                       UUID NOT NULL,
  request_type                    TEXT NOT NULL,
  source_id                       UUID NOT NULL,
  submitter_employee_id           UUID NOT NULL,
  submitter_position_instance_id  UUID REFERENCES position_instances(instance_id),
  status                          TEXT NOT NULL CHECK (status IN ('Pending','Approved','Rejected','Escalated','Withdrawn','EscalationExhausted')),
  current_approval_step_id        UUID,
  submitted_at                    TIMESTAMPTZ NOT NULL,
  resolved_at                     TIMESTAMPTZ,
  metadata                        JSONB NOT NULL DEFAULT '{}'
);
CREATE INDEX idx_ar_tenant ON approval_requests (tenant_id, status);
CREATE INDEX idx_ar_source ON approval_requests (source_id, request_type);

CREATE TABLE approval_chains (
  chain_id            UUID PRIMARY KEY,
  tenant_id           UUID NOT NULL,
  request_id          UUID NOT NULL REFERENCES approval_requests(request_id),
  current_step_index  SMALLINT NOT NULL DEFAULT 0,
  resolved_at         TIMESTAMPTZ
);

CREATE TABLE approval_steps (
  step_id                             UUID PRIMARY KEY,
  chain_id                            UUID NOT NULL REFERENCES approval_chains(chain_id),
  step_index                          SMALLINT NOT NULL,
  resolved_approver_position_instance_id UUID REFERENCES position_instances(instance_id),
  resolved_approver_employee_id       UUID,
  original_position_instance_id       UUID,     -- set when delegated
  is_delegated                        BOOLEAN NOT NULL DEFAULT false,
  deadline                            TIMESTAMPTZ NOT NULL,
  status                              TEXT NOT NULL CHECK (status IN ('Pending','Approved','Rejected','Escalated','Skipped')),
  decided_at                          TIMESTAMPTZ,
  decision_notes                      TEXT,
  escalation_level                    SMALLINT NOT NULL DEFAULT 0
);
CREATE INDEX idx_step_chain ON approval_steps (chain_id, step_index);
CREATE INDEX idx_step_approver ON approval_steps (resolved_approver_employee_id, status);
CREATE INDEX idx_step_deadline ON approval_steps (deadline) WHERE status = 'Pending';
```

#### Tenant Database Tables (BC-07 Rules & Policy Engine)

```sql
CREATE TABLE policy_definitions (
  policy_id       UUID PRIMARY KEY,
  tenant_id       UUID NOT NULL,
  type            TEXT NOT NULL,
  name            TEXT NOT NULL,
  version         INT NOT NULL DEFAULT 1,
  status          TEXT NOT NULL CHECK (status IN ('Draft','Active','Deprecated')),
  effective_from  DATE NOT NULL,
  effective_to    DATE,
  scope           TEXT NOT NULL CHECK (scope IN ('Global','Department','EmploymentType','Grade')),
  scope_id        UUID,
  created_by      UUID,
  published_at    TIMESTAMPTZ
);
CREATE INDEX idx_pd_tenant_type ON policy_definitions (tenant_id, type, status);
CREATE INDEX idx_pd_effective ON policy_definitions (tenant_id, type, effective_from, effective_to);

CREATE TABLE policy_rules (
  rule_id             UUID PRIMARY KEY,
  policy_id           UUID NOT NULL REFERENCES policy_definitions(policy_id) ON DELETE CASCADE,
  name                TEXT NOT NULL,
  priority            INT NOT NULL,
  condition_field     TEXT NOT NULL,
  condition_operator  TEXT NOT NULL,
  condition_value     TEXT NOT NULL,
  condition_value_high TEXT,
  action_type         TEXT NOT NULL,
  action_parameters   JSONB NOT NULL DEFAULT '{}',
  is_active           BOOLEAN NOT NULL DEFAULT true
);
CREATE INDEX idx_pr_policy ON policy_rules (policy_id, priority);

CREATE TABLE policy_evaluation_logs (
  log_id              UUID PRIMARY KEY,
  tenant_id           UUID NOT NULL,
  policy_id           UUID REFERENCES policy_definitions(policy_id),
  policy_version      INT NOT NULL,
  evaluated_at        TIMESTAMPTZ NOT NULL,
  subject_employee_id UUID NOT NULL,
  request_context     JSONB NOT NULL,
  matched_rule_id     UUID,
  result              TEXT NOT NULL CHECK (result IN ('Allowed','Denied','Modified','Flagged')),
  result_parameters   JSONB NOT NULL DEFAULT '{}'
);
CREATE INDEX idx_pel_tenant ON policy_evaluation_logs (tenant_id, evaluated_at DESC);
CREATE INDEX idx_pel_employee ON policy_evaluation_logs (subject_employee_id, evaluated_at DESC);
```

#### Key Cross-Table Foreign Key Summary

| Child Column | References | Notes |
| --- | --- | --- |
| `departments.head_position_id` | `position_instances.instance_id` | Set after BC-04 is live |
| `departments.cost_centre_id` | `cost_centres.cost_centre_id` | Nullable |
| `cost_centres.owner_position_id` | `position_instances.instance_id` | Drives expense routing |
| `position_templates.department_id` | `departments.department_id` | Required |
| `position_instances.reporting_to_instance_id` | `position_instances.instance_id` | Self-referential hierarchy |
| `work_structures.supervisor_position_instance_id` | `position_instances.instance_id` | Drives attendance routing |
| `approval_steps.resolved_approver_position_instance_id` | `position_instances.instance_id` | May be null if position vacated mid-flow |

---

### Foundation APIs

Each BC's individual endpoint contracts are defined inline in the BC sections above. This section defines the cross-cutting API conventions that apply to all Foundation endpoints without exception.

#### API Versioning

- All Foundation APIs are versioned in the URL path: `/api/v1/...`
- Phase 1 ships at `v1`. Breaking changes require a new version (`v2`) with at least 6 months parallel support.
- Non-breaking additions (new optional fields, new response fields) do not require a version bump.
- Version is omitted from the BC sections above for readability; assume `/api/v1/` prefix throughout.

#### Standard Error Response Format

All error responses return `application/json` with this structure:

```json
{
  "type": "https://circlate.io/errors/validation",
  "title": "One or more validation errors occurred",
  "status": 422,
  "traceId": "00-4a0d8b1234abc...",
  "errors": {
    "amount": ["Amount must be greater than 0"],
    "currency": ["Currency must be a valid ISO 4217 code"]
  }
}
```

Standard HTTP status codes used:

| Code | Meaning | When used |
| --- | --- | --- |
| 200 | OK | Successful read or update |
| 201 | Created | Resource successfully created |
| 204 | No Content | Successful delete or action with no response body |
| 400 | Bad Request | Malformed JSON, missing required fields |
| 401 | Unauthorised | Missing or invalid JWT |
| 403 | Forbidden | Valid JWT but insufficient capability |
| 404 | Not Found | Resource does not exist for this tenant |
| 409 | Conflict | Duplicate record (unique constraint violation) |
| 422 | Unprocessable | Business rule violation (not a format error) |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Unexpected failure (never expose internals) |

#### Idempotency

All mutating requests (`POST`, `PUT`, `DELETE`) accept an optional `Idempotency-Key` header (UUID). If provided:

- The server stores the response for that key for 24 hours.
- Duplicate requests with the same key return the stored response without re-executing.
- Idempotency keys are tenant-scoped — the same key may be reused across different tenants.

This is mandatory for all mobile clients (unreliable connectivity) and all approval actions (double-submit prevention).

#### Pagination

All list endpoints support cursor-based pagination:

Request: `GET /api/v1/employees?limit=25&after=<cursor>`

Response:

```json
{
  "data": [...],
  "pagination": {
    "limit": 25,
    "hasNextPage": true,
    "nextCursor": "eyJpZCI6IjEyMzQ..."
  }
}
```

- Default `limit`: 25. Maximum: 200.
- Cursor is a base64-encoded opaque token (not a page number). Do not construct cursors manually.
- Offset-based pagination (`?page=2`) is not supported.

#### Tenant Context

The tenant is always resolved from the JWT `tid` claim, never from a URL parameter. Requests that include a `tenantId` in the URL are only used by platform-admin endpoints (not tenant-user endpoints). This prevents tenant parameter tampering.

#### Rate Limiting

| Endpoint Category | Limit | Window |
| --- | --- | --- |
| Authentication (`/auth/token`) | 10 requests | 1 minute per IP |
| MFA verification | 5 requests | 5 minutes per user |
| Standard API endpoints | 300 requests | 1 minute per tenant |
| Clock-in (`/attendance/clock-in`) | 5 requests | 1 minute per employee |
| Bulk operations | 10 requests | 1 minute per tenant |
| Report export | 20 requests | 1 hour per tenant |

Rate limit responses include headers: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`.

#### Consolidated Foundation Endpoint Index

| BC | Base Path | Key Endpoints |
| --- | --- | --- |
| BC-01 Identity | `/api/v1/auth` | `/token`, `/refresh`, `/token/service`, `/mfa/enrol`, `/mfa/verify`, `/sessions/revoke` |
| BC-01 Users | `/api/v1/users` | `GET/POST /users`, `GET/PATCH /{id}`, `/{id}/suspend`, `/{id}/reactivate` |
| BC-01 Service Accounts | `/api/v1/service-accounts` | `GET/POST`, `/{id}/keys`, `/{id}/keys/{keyId}` |
| BC-02 Organisation | `/api/v1/organisations` | `GET/PATCH /` |
| BC-02 Business Units | `/api/v1/business-units` | `GET/POST`, `/{id}`, `/{id}/move` |
| BC-02 Departments | `/api/v1/departments` | `GET/POST`, `/{id}` |
| BC-02 Cost Centres | `/api/v1/cost-centres` | `GET/POST`, `/{id}` |
| BC-02 Holidays | `/api/v1/public-holidays` | `GET /{year}`, `POST`, `/{year}/publish` |
| BC-03 Authority | `/api/v1/authority-profiles` | `GET/POST`, `/{id}`, `/{id}/publish`, `/{id}/deprecate`, `/{id}/capabilities` |
| BC-03 Delegation | `/api/v1/delegations` | `GET/POST`, `/{id}` |
| BC-03 Assign | `/api/v1/positions/{id}/authority-profile` | `POST` |
| BC-04 Templates | `/api/v1/position-templates` | `GET/POST`, `/{id}` |
| BC-04 Establishment | `/api/v1/position-establishments` | `GET/POST`, `/{id}/approve` |
| BC-04 Instances | `/api/v1/position-instances` | `GET/POST`, `/{id}`, `/{id}/assign`, `/{id}/vacate`, `/{id}/occupancy-history` |
| BC-04 Acting | `/api/v1/acting-assignments` | `GET/POST`, `/{id}/activate`, `/{id}/complete`, `/{id}/cancel` |
| BC-04 Grades | `/api/v1/grades` | `GET`, `/{id}` |
| BC-04 Org Chart | `/api/v1/org-chart` | `GET` |
| BC-05 Work Structures | `/api/v1/work-structures` | `GET/POST`, `/{id}`, `/{id}/activate`, `/{id}/complete` |
| BC-05 Assignments | `/api/v1/work-structures/{id}/assignments` | `GET/POST`, `/{assignmentId}` |
| BC-05 Compliance | `/api/v1/work-structures/{id}/compliance` | `GET/POST` |
| BC-05 Allocations | `/api/v1/employees/{id}/allocations` | `GET` |
| BC-05 Utilisation | `/api/v1/work-structures/{id}/utilisation` | `GET` |
| BC-06 Approvals | `/api/v1/approvals` | `POST`, `/pending`, `/{id}/approve`, `/{id}/reject`, `/{id}/withdraw`, `/{id}/chain` |
| BC-07 Policies | `/api/v1/policies` | `GET/POST`, `/{id}`, `/{id}/rules`, `/{id}/publish`, `/{id}/deprecate` |
| BC-07 Evaluate | `/api/v1/policies/evaluate` | `POST` (dry run) |
| BC-07 Templates | `/api/v1/policies/templates` | `GET`, `/{id}/activate` |
| BC-07 Logs | `/api/v1/policy-evaluation-log` | `GET` |

## Foundation Security Architecture

### 1. Authentication Model

**Provider**: Keycloak (self-hosted), one realm per tenant.

| Layer | Mechanism | Notes |
| --- | --- | --- |
| Human users | OIDC Authorization Code + PKCE | Browser-based login via Next.js |
| Machine-to-machine | OAuth 2.0 Client Credentials | Background jobs, integrations |
| Token format | JWT RS256 | Signed with realm private key |
| Token TTL | Access: 15 min, Refresh: 8 h, ID: 15 min | Configured per realm |
| Realm name pattern | `circlate-{tenantId}` | Isolated realm, no cross-tenant SSO |
| User federation | Optional LDAP/AD bridge per tenant | HR-initiated; Keycloak syncs on login |

**Token structure** — the backend validates on every request:

```
Header: { alg: RS256, kid: <realm-key-id> }
Payload: {
  iss: https://auth.circlate.com/realms/circlate-{tenantId},
  sub: <keycloak-user-uuid>,
  tid: <tenantId>,
  emp: <employeeId>,
  pos: [<positionInstanceId>],
  caps: ["leave:request","leave:approve:team", ...],
  roles: ["employee","manager"],
  exp: <unix-ts>,
  iat: <unix-ts>,
  jti: <uuid>
}
```

**Capability derivation on login** (Keycloak Protocol Mapper — Java SPI):

1. Load `EmployeePositionAssignment` for the subject.
2. Walk each position → its `AuthorityProfile` → its `AuthorityEntries`.
3. Map each `BusinessAuthority.Name` → `Capability` string via the Permission Derivation Contract (BC-03).
4. Deduplicate, sort, inject as `caps` array claim.
5. Same mapper injects `tid`, `emp`, `pos`.

**Token revocation**: Redis `SET jti:{jti} revoked EX {remaining_ttl}`. All endpoints check the revocation set after signature validation. Triggered when an employee's position assignment changes mid-session.

---

### 2. Authorisation Model

Authorisation is **capability-based**, not role-based. Roles are coarse groupings for Keycloak UI only. The backend enforces capabilities exclusively.

**Guard implementation** (ASP.NET Core Policy + MediatR pipeline):

```csharp
[RequiresCapability("leave:approve:team")]

public class CapabilityRequirementHandler : AuthorizationHandler<CapabilityRequirement>
{
    protected override Task HandleRequirementAsync(
        AuthorizationHandlerContext context, CapabilityRequirement requirement)
    {
        var caps = context.User.FindAll("caps").Select(c => c.Value);
        if (caps.Contains(requirement.Capability))
            context.Succeed(requirement);
        return Task.CompletedTask;
    }
}
```

**Scope modifiers** (`caps` claim values):

| Scope suffix | Meaning | Example |
| --- | --- | --- |
| `:self` | Own records only | `attendance:view:self` |
| `:team` | Direct reports' records | `leave:approve:team` |
| `:department` | Department the position owns | `expenses:approve:department` |
| `:organisation` | All records in tenant | `employees:manage:organisation` |
| *(no suffix)* | Action without scope restriction | `reports:export` |

**Data-level enforcement** (EF Core global query filters):

```csharp
modelBuilder.Entity<LeaveRequest>()
    .HasQueryFilter(l => l.TenantId == _tenantId);

if (!caps.Contains("leave:view:organisation"))
    query = query.Where(l => l.EmployeeId == currentEmployeeId
                          || directReportIds.Contains(l.EmployeeId));
```

---

### 3. Tenant Isolation Strategy

**Database isolation**: Platform DB holds only `Tenant`, `TenantUser` identity rows. Each tenant's operational data lives in its own PostgreSQL schema within a shared cluster (schema-per-tenant), with an optional migration path to database-per-tenant for Enterprise tier.

```
circlate_platform DB:
  public.tenants
  public.tenant_users

circlate_operational DB:
  tenant_{tenantId}.employees
  tenant_{tenantId}.positions
  tenant_{tenantId}.leave_requests
  ... (all operational tables)
```

**EF Core multi-tenancy pattern**:

```csharp
public class AppDbContext : DbContext, IAppDbContext
{
    private readonly string _schema;

    protected override void OnModelCreating(ModelBuilder mb)
    {
        mb.HasDefaultSchema(_schema);
    }
}
```

**Tenant context injection** — resolved once per HTTP request:

1. JWT middleware validates token, extracts `tid` claim.
2. `TenantContextMiddleware` sets `TenantContext.Current = tid`.
3. DI container resolves `AppDbContext` with schema `tenant_{tid}`.
4. Any query without explicit filter still hits only the tenant schema.

**Cross-tenant attack surface mitigations**:

- Schema names are UUIDs (non-guessable).
- EF Core global query filters provide defence-in-depth.
- Background jobs carry a `tenantId` parameter; never iterate tenants in a single DB context.
- Keycloak realm isolation prevents token reuse across tenants.

---

### 4. Audit Logging Model

All state-mutating operations emit an `AuditEntry` automatically via a MediatR pipeline behaviour.

```sql
CREATE TABLE audit_log (
    id                uuid PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id         uuid NOT NULL,
    actor_user_id     uuid NOT NULL,
    actor_employee_id uuid,
    actor_position_id uuid,
    action            text NOT NULL,
    entity_type       text NOT NULL,
    entity_id         uuid NOT NULL,
    before_state      jsonb,
    after_state       jsonb,
    ip_address        inet,
    user_agent        text,
    occurred_at       timestamptz NOT NULL DEFAULT now(),
    idempotency_key   uuid
);
CREATE INDEX ix_audit_log_tenant_entity ON audit_log(tenant_id, entity_type, entity_id);
CREATE INDEX ix_audit_log_actor       ON audit_log(tenant_id, actor_employee_id);
CREATE INDEX ix_audit_log_occurred    ON audit_log(tenant_id, occurred_at DESC);
```

**Retention**: Append-only, never updated or deleted. Default 7-year retention for Brunei labour law compliance. Archived to cold storage after 2 years.

**Sensitive field redaction**: Fields in `SensitiveFields` registry (salary, IC number, bank account) are replaced with `"[REDACTED]"` in `before_state`/`after_state` for all roles except `audit:view:sensitive`. Raw values stored in a separately encrypted `audit_log_sensitive` table linked by `audit_log.id`.

---

### 5. Sensitive Data Controls

#### Compensation Data

| Control | Implementation |
| --- | --- |
| Column-level encryption | `salary_encrypted bytea` stored using AES-256-GCM; plaintext never persisted |
| Key per tenant | Encryption key in Vault under `secret/tenant/{tid}/salary-key` |
| Read capability | `compensation:view:self`, `compensation:view:team`, `compensation:view:organisation` |
| API response masking | `GET /employees/{id}` returns `"salary": null` without capability |
| Audit on access | Every decrypted salary read logs `Compensation.Viewed` to audit\_log |
| Export restriction | Payroll export requires `reports:export` AND `compensation:view:organisation` |

#### IC / National ID (Brunei IC)

| Control | Implementation |
| --- | --- |
| Storage | `ic_number_encrypted bytea` — same AES-256-GCM pattern |
| Display masking | Returns `"XX-XXXXX"` (last 5 digits only) without `employees:view:sensitive` |
| Search | Full IC search requires `employees:search:sensitive`; partial match requires `employees:view:sensitive` |
| Tokenisation | Internal keys reference `employee_id` (UUID), never IC number |
| Breach response | Treated as PII under Brunei PDPO; breach triggers mandatory notification to MOFE |

#### Other PII Fields

- `date_of_birth` — masked to year only without `employees:view:sensitive`
- `phone_number` — last 4 digits visible; full number requires `employees:view:sensitive`
- `bank_account_number` — stored encrypted; only Payroll role (`compensation:manage`) may read
- `address` — stored plaintext but behind `employees:view:sensitive` capability check

---

### 6. API Security Standards

**Transport**: TLS 1.3 minimum. HTTP/2 required. HSTS with 1-year max-age.

**Request requirements**:

| Header | Required on | Rule |
| --- | --- | --- |
| `Authorization: Bearer <jwt>` | All endpoints except `/health`, `/api/auth/*` | Validated on every request |
| `Idempotency-Key: <uuid>` | POST, PUT, PATCH | 409 Conflict if duplicate key within 24 h |
| `Content-Type: application/json` | All mutation endpoints | 415 if absent |

**Rate limiting** (Redis token bucket per `tid:userId`):

| Tier | Limit |
| --- | --- |
| Standard | 300 req/min |
| Payroll export | 10 req/min |
| Bulk import | 5 req/min |
| Auth endpoints | 20 req/min per IP |

**Input validation**:

- All command DTOs validated with FluentValidation before MediatR dispatch.
- String fields: max length enforced, HTML stripped, Unicode normalised to NFC.
- Date fields: ISO 8601 only; reject ambiguous formats.
- Enum fields: validated against known values; unknown values return 400.
- File uploads: MIME validated by magic bytes, max 20 MB, virus scan via ClamAV sidecar before storage.

**Security headers** (all responses):

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Content-Security-Policy: default-src 'none'
Referrer-Policy: no-referrer
```

**Error responses**: Never leak stack traces, table names, or SQL in production.

```json
{
  "type": "validation_error",
  "title": "One or more fields are invalid",
  "status": 400,
  "errors": { "field": ["message"] },
  "traceId": "<correlation-id>"
}
```

---

### 7. Secrets Management

| Secret | Storage | Rotation |
| --- | --- | --- |
| PostgreSQL credentials | Vault dynamic secrets (90-day TTL) | Automatic |
| Redis password | Vault KV v2 | Manual, 90 days |
| Keycloak client secret | Vault KV v2 | Manual, 180 days |
| Tenant salary encryption keys | Vault KV v2 per tenant | Manual, annual |
| JWT signing keys | Keycloak-managed realm key | Keycloak rotation tooling, annual |
| SMTP credentials | Vault KV v2 | Manual, 180 days |

Applications retrieve secrets at startup via Vault agent sidecar. `appsettings.Production.json` is gitignored; production config is injected via environment variables resolved from Vault.

**Secret scanning**: Git pre-commit hook (gitleaks) blocks commits containing private keys, connection strings, or JWT secrets.

## Foundation Reporting Requirements

All foundation reports are read-only projections. They must reflect current live state, not cached snapshots, unless a refresh cadence is specified. Access is controlled via capabilities from the Permission Derivation Contract.

---

### FR-01 Authority Assignment Report

**Purpose**: Shows every live authority assignment in the tenant — which position holds which business authorities and through which authority profile.

**Data sources**: `authority_profiles`, `authority_entries`, `position_establishments`, `position_instances`, `employee_position_assignments`

**Columns**:

| Column | Source |
| --- | --- |
| Employee Name | `employees.full_name` |
| Position Title | `position_templates.title` |
| Position Instance Ref | `position_instances.reference_code` |
| Authority Profile | `authority_profiles.name` |
| Business Authority | `authority_entries.business_authority` |
| Scope | `authority_entries.scope` |
| Effective From | `employee_position_assignments.start_date` |
| Acting? | `employee_position_assignments.is_acting` |

**Filters**: Department, Authority Profile, Business Authority name, Acting assignments only

**Refresh cadence**: Real-time (no caching)

**Access**: `authority:report` capability (HR Manager, System Admin)

**Use case**: Compliance review — verify no unapproved authority is active; identify overly broad authority grants; support role audits.

---

### FR-02 Delegation Report

**Purpose**: Shows all active and historical delegations — who delegated what authority to whom, for what period, and whether it has been used.

**Data sources**: `authority_delegations`, `authority_entries`, `employees`, `position_instances`

**Columns**:

| Column | Source |
| --- | --- |
| Delegating Employee | `employees.full_name` (from position) |
| Delegating Position | `position_instances.reference_code` |
| Receiving Employee | `employees.full_name` |
| Delegated Authority | `authority_entries.business_authority` |
| Delegated Scope | `authority_delegations.scope_override` |
| Start Date | `authority_delegations.start_date` |
| End Date | `authority_delegations.end_date` |
| Status | Derived: Active / Expired / Revoked |
| Actions Taken | Count of approvals performed under this delegation |

**Filters**: Status (Active / All), Delegating employee, Receiving employee, Date range

**Refresh cadence**: Real-time

**Access**: `authority:report` capability

**Use case**: Audit trail for who made decisions during leave periods; validate no delegation exceeds the delegator's own scope.

---

### FR-03 Vacancy Report

**Purpose**: Shows all approved position establishments that are either unfilled or understaffed relative to their approved headcount.

**Data sources**: `position_establishments`, `position_instances`, `employee_position_assignments`

**Columns**:

| Column | Source |
| --- | --- |
| Position Title | `position_templates.title` |
| Department | `organisation_units.name` |
| Approved Headcount | `position_establishments.approved_headcount` |
| Filled Slots | Count of active `position_instances` with active assignment |
| Vacant Slots | Approved Headcount − Filled Slots |
| Days Vacant | Date.Today − last filled date (from assignment history) |
| Criticality | `position_establishments.criticality_level` |

**Filters**: Department, Criticality level, Vacant only (default on), Minimum days vacant

**Refresh cadence**: Real-time

**Access**: `employees:manage:organisation` or `recruitment:manage` capability

**Use case**: Recruitment pipeline planning; identifies which positions have been vacant longest; feeds into recruitment requisition creation.

---

### FR-04 Acting Assignment Report

**Purpose**: Shows all current and historical acting assignments — where an employee is temporarily placed into a different position.

**Data sources**: `acting_assignments`, `employees`, `position_instances`, `position_templates`

**Columns**:

| Column | Source |
| --- | --- |
| Employee Name | `employees.full_name` |
| Home Position | Original `position_instances.reference_code` |
| Acting Position | Acting `position_instances.reference_code` |
| Acting Position Title | `position_templates.title` |
| Start Date | `acting_assignments.start_date` |
| End Date | `acting_assignments.end_date` (null = open-ended) |
| Authorised By | Approver `employees.full_name` |
| Duration (days) | Derived |
| Status | Active / Ended / Scheduled |

**Filters**: Status, Employee, Department, Date range

**Refresh cadence**: Real-time

**Access**: `authority:report` capability

**Use case**: Payroll supplementation review (acting allowance); succession planning visibility; audit of authority exposure during acting periods.

---

### FR-05 Organisation Structure Report

**Purpose**: A snapshot of the full organisational hierarchy — units, their parent relationships, the positions within them, and which employees currently fill those positions.

**Data sources**: `organisation_units`, `position_establishments`, `position_instances`, `employee_position_assignments`, `employees`

**Output formats**: Tabular (default) and hierarchical tree (JSON export)

**Columns** (tabular):

| Column | Source |
| --- | --- |
| Unit Name | `organisation_units.name` |
| Unit Code | `organisation_units.code` |
| Parent Unit | `organisation_units.parent_id` → name |
| Unit Level | Derived depth from root |
| Position Title | `position_templates.title` |
| Position Code | `position_establishments.code` |
| Employee Name | `employees.full_name` |
| Acting? | `employee_position_assignments.is_acting` |
| Employment Status | `employees.status` |

**Filters**: Unit (subtree), Position filled/vacant, Include acting assignments

**Point-in-time**: Accept `asOf` date parameter — reports show the structure as it existed on that date, using assignment history.

**Refresh cadence**: Real-time for current; point-in-time reads from audit history

**Access**: `employees:view:organisation` capability (all managers and above)

**Use case**: Organisational design reviews; headcount planning; onboarding context for new executives.

---

### FR-06 Workforce Allocation Report

**Purpose**: Shows how employees' effort is allocated across work structures — teams, projects, programmes, sites. Identifies over-allocated and under-allocated employees.

**Data sources**: `work_structure_assignments`, `work_structures`, `employees`, `position_instances`

**Columns**:

| Column | Source |
| --- | --- |
| Employee Name | `employees.full_name` |
| Department | `organisation_units.name` |
| Work Structure | `work_structures.name` |
| Structure Type | `work_structures.type` (Team / Project / Programme / …) |
| Allocation % | `work_structure_assignments.allocation_percentage × 100` |
| Role in Structure | `work_structure_assignments.role` |
| Start Date | `work_structure_assignments.start_date` |
| End Date | `work_structure_assignments.end_date` |
| Total Allocation % | Sum across all structures for that employee |

**Derived indicators**:

- 🔴 Over-allocated: Total > 100%
- 🟡 Under-utilised: Total < 60%
- 🟢 Nominal: 80–100%

**Filters**: Employee, Department, Work structure type, Structure name, Allocation status (over / under / nominal)

**Refresh cadence**: Real-time

**Access**: `work-structures:manage` or `employees:manage:organisation` capability

**Use case**: Resource planning; identify capacity for new project assignments; flag employees approaching burnout risk via over-allocation.

---

### FR-07 Position Risk Report

**Purpose**: Identifies positions that represent a concentration risk to the organisation — single points of failure, long-term vacancies, or positions with authority that is currently unassigned or delegated indefinitely.

**Data sources**: `position_establishments`, `position_instances`, `employee_position_assignments`, `authority_entries`, `authority_delegations`

**Risk signals detected**:

| Risk Signal | Detection Logic |
| --- | --- |
| Sole occupant of critical position | `criticality_level = High` AND `filled_slots = 1` AND no backup designation |
| Critical position vacant | `criticality_level = High` AND `filled_slots = 0` |
| Authority delegation running > 90 days | `authority_delegations.end_date − start_date > 90` |
| Acting assignment running > 60 days | `acting_assignments` with no end date, start > 60 days ago |
| Position with no holder and pending approvals | Approval queue items whose approver position has no active assignment |
| Authority profile not reviewed in 12 months | `authority_profiles.last_reviewed_at < today − 365 days` |

**Columns**:

| Column | Notes |
| --- | --- |
| Risk Signal | From the table above |
| Severity | High / Medium / Low |
| Position / Employee | Affected entity |
| Department | Context |
| Days in Current State | How long the risk has existed |
| Recommended Action | Templated text per signal type |

**Refresh cadence**: Daily batch (computed at 06:00 BNT); on-demand refresh available to HR Manager

**Access**: `authority:report` capability

**Use case**: Monthly governance review by HR Director; input to succession planning; compliance evidence for labour authority inspections.

---

### FR-08 Approval Queue Ageing Report

**Purpose**: Shows all pending approval requests grouped by approver position, with ageing bands. Identifies stalled approvals and escalation candidates.

**Data sources**: `approval_requests`, `approval_steps`, `position_instances`, `employees`

**Ageing bands**: < 1 day / 1–3 days / 4–7 days / > 7 days

**Columns**:

| Column | Source |
| --- | --- |
| Request Type | `approval_requests.entity_type` |
| Requestor | Employee name |
| Current Approver Position | `approval_steps.assigned_position` → title |
| Current Approver Employee | `employee_position_assignments` lookup |
| Days Waiting | Date.Today − `approval_steps.assigned_at` |
| Ageing Band | Derived |
| Escalation Policy | `policy_definitions` lookup for this request type |
| Auto-escalates At | Derived from policy timeout |

**Filters**: Request type, Approver department, Ageing band, Escalation imminent (within 24 h)

**Refresh cadence**: Real-time

**Access**: `approvals:report` capability (HR Manager, any manager for their own queue)

**Use case**: Daily queue management by HR; proactive escalation before SLA breach; identifies approvers who need coverage (leave / vacancy).

## Foundation Risks & Mitigations

Severity: **H** = High (must mitigate before go-live), **M** = Medium (mitigate within first 3 months), **L** = Low (monitor).

---

### BC-01 Identity Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| I-01 | Keycloak realm misconfiguration exposes one tenant's tokens to another | H | Per-realm issuer validation on every JWT; integration test suite asserts `iss` matches `tid` before each deployment |
| I-02 | Custom Keycloak SPI (capability mapper) fails silently — user logs in with empty `caps` | H | Mapper throws, logs, and returns HTTP 500 on internal error; integration test asserts `caps` is non-empty for a known employee |
| I-03 | Token revocation check adds latency to every request | M | Redis revocation set is an O(1) GET; acceptable overhead; only populated on position change events, not on every login |
| I-04 | Keycloak single point of failure for all tenant logins | M | Deploy Keycloak in active-active cluster (2+ nodes) behind load balancer; health check at `/health`; monitored by uptime alerting |
| I-05 | Capability list in JWT grows too large for HTTP header limits | L | Caps are short strings (`leave:approve:team`); typical employee has < 30 caps ≈ 600 bytes; monitor max JWT size in staging |

---

### BC-02 Organisation Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| O-01 | Circular parent relationships in `organisation_units` corrupt tree queries | H | Database constraint: `CHECK (id <> parent_id)`; application-layer cycle detection before INSERT/UPDATE; recursive CTE depth limit 50 |
| O-02 | Bulk org restructures (parent\_id updates) cause fan-out of approval chain invalidations | M | Org restructure is a versioned operation; approval chains are re-evaluated lazily at approval time, not eagerly on structure change |
| O-03 | Historical org structure queries are slow (full audit\_log scan) | M | Maintain `organisation_unit_history` table with effective date ranges; indexed on `(unit_id, effective_from, effective_to)` |
| O-04 | Multiple root units (no single CEO-equivalent) breaks hierarchy assumptions | L | Enforce single root constraint in application layer; allow optional `virtual_root` for matrix organisations |

---

### BC-03 Authority & Delegation Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| A-01 | Delegation exceeds delegator's own scope — privilege escalation | H | Delegation validation: `delegated_scope ⊆ delegator_current_scope`; enforced at delegation creation and re-validated at each use |
| A-02 | Delegation end date not enforced — permanent authority transfer | H | Scheduled job (`DelegationExpiryJob`) runs every 15 min; expired delegations set to `Expired` status; Redis TTL on delegation cache entries |
| A-03 | Authority profile change doesn't invalidate live JWT tokens | H | On `AuthorityProfileUpdated` domain event: revoke all JWTs for employees holding affected positions via Redis revocation set |
| A-04 | `caps` claim computed at login — stale if position changes during session | M | Covered by I-02 token revocation; short 15-min access token TTL limits exposure window |
| A-05 | Permission Derivation Contract mapping gets out of sync between Keycloak SPI and API guards | M | Contract is the single source of truth (BC-03 spec); SPI and guard are both generated from the same YAML contract file at build time |
| A-06 | An employee can hold multiple positions with conflicting authorities (e.g. requestor + approver for the same workflow) | H | Conflict detection rule: `authority:request` and `authority:approve` for the same domain must not coexist in a single employee's effective capability set; enforced at position assignment |

---

### BC-04 Position Management Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| P-01 | Position instance created without an establishment — orphaned positions with no headcount control | H | Foreign key `position_instances.establishment_id NOT NULL`; application blocks creation if establishment is at capacity |
| P-02 | Headcount bypass: creating multiple instances against a single-headcount establishment | H | `CHECK` constraint + application guard: `SELECT COUNT(*) FROM position_instances WHERE establishment_id = ? AND status = 'Active'` before INSERT |
| P-03 | Deleting a position that still has an active employee assignment | H | Soft-delete only; `position_instances.status = Inactive`; application blocks inactivation if `employee_position_assignments` record is active |
| P-04 | Acting assignment conflicts with primary assignment — same employee in two positions simultaneously | M | Maximum one acting assignment per employee at a time; enforced at assignment creation |
| P-05 | Position templates proliferate — no governance on new template creation | L | `position_templates` require `hr_manager` capability to create; template count dashboard in FR-05 org report |

---

### BC-05 Work Structure Management Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| W-01 | Allocation percentage validation is enforced only at assignment time — bulk restructures can push total > 100% | H | Trigger or EF Core interceptor re-checks total allocation after any `work_structure_assignments` INSERT/UPDATE |
| W-02 | Work structure supervisor routes approvals but has no formal authority — creates shadow hierarchy | M | Operational responsibility (work structure) and organisational authority (position) are explicitly separate in BC-05; approval routing (BC-06) uses org hierarchy for authority-based decisions, work structure supervisor only for operational notifications |
| W-03 | Long-running projects never close — assignment records accumulate | L | `work_structures.status` enforced; HR Manager receives quarterly report of structures with no end date set and no active changes |
| W-04 | Employee leaves the organisation but remains assigned to work structures | M | `EmployeeTerminated` domain event triggers automatic end-dating of all work structure assignments on the termination date |

---

### BC-06 Approval Routing Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| R-01 | Approval chain resolves to no eligible approver — request stuck in perpetuity | H | Resolution algorithm Step 7: if no approver found after full hierarchy walk, escalate to HR Manager as ultimate fallback; never return an empty approver |
| R-02 | Approver position becomes vacant mid-approval — pending item is orphaned | H | `PositionVacated` event triggers re-evaluation of all pending approval steps assigned to that position; re-routed to the position's hierarchical superior |
| R-03 | Circular approval chain (A approves B's requests; B approves A's requests) | M | Chain validation rejects same-employee-appears-twice patterns; requestor cannot appear as an approver in their own chain |
| R-04 | Approval audit trail is insufficient for labour dispute | M | Each `approval_steps` record includes: assigned\_at, acted\_at, actor employee and position, action taken, comment; combined with `audit_log` this satisfies Brunei Employment Order evidentiary requirements |
| R-05 | Escalation timeout policy misconfiguration causes immediate escalation on new requests | M | Policy validation: `timeout_hours >= 1`; tested in staging with synthetic approvals before each production policy change |
| R-06 | High-volume approval periods (month-end expenses) overload the approval queue | L | Approval processing is async via MediatR + background queue; queue depth monitored; approval table indexed on `(tenant_id, status, assigned_position_id)` |

---

### BC-07 Rules & Policy Engine Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| E-01 | Policy rule with a logical error silently allows or denies all requests | H | Rules must be tested against a fixture set before activation; `PolicyDefinition.status = Draft` until HR Manager publishes; staging environment runs all rules against synthetic data |
| E-02 | Two active policies with overlapping conditions produce conflicting outcomes | H | Priority field on `Rule` entities; deterministic evaluation: highest priority rule wins; conflict detection at publish time warns if two rules match identical conditions |
| E-03 | Policy version history grows unboundedly — table becomes slow | M | `policy_versions` archived after 7 years; active version index maintained separately |
| E-04 | Condition expression language allows arbitrary code injection | H | Condition expressions are a restricted DSL (field comparisons, logical operators, date arithmetic only); no `eval`, no string interpolation; parsed with an allowlist grammar, rejected if unknown tokens present |
| E-05 | Tenant misconfigures a policy that removes all leave entitlement | M | System policies (minimum statutory leave per Brunei Employment Order) are read-only platform defaults; tenant policies layer on top and cannot reduce below statutory minimum |

---

### Cross-Cutting: Scalability Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| S-01 | Schema-per-tenant PostgreSQL accumulates too many schemas — connection pooling degrades | M | PgBouncer connection pooler with schema-aware routing; migrate large tenants to dedicated database if schema count exceeds 500 |
| S-02 | Foundation ERD join depth — approval resolution requires 6-way join | M | Materialised view `mv_employee_authority` refreshed on `AuthorityAssigned` event; approval resolution reads the view, not the full join |
| S-03 | Redis revocation set grows if TTLs are not set correctly | M | Every `SET` on the revocation index includes `EX {remaining_ttl}` derived from the JWT `exp`; Redis `maxmemory-policy allkeys-lru` as final safety net |
| S-04 | Background jobs (delegation expiry, escalation) compete for DB connections | L | Jobs run in a dedicated worker process with a separate connection pool (max 10); never share pool with API request path |

---

### Cross-Cutting: Operational Risks

| # | Risk | Sev | Mitigation |
| --- | --- | --- | --- |
| X-01 | EF Core migration applied to wrong tenant schema in production | H | Migration runner: explicit schema parameter required; dry-run mode outputs SQL without executing; two-person confirmation for production migrations |
| X-02 | Vault unavailable at startup — secrets not injected, app fails to start | H | Vault agent sidecar with local cache; app reads from cache on Vault unavailability; cache TTL = 24 h; alert on Vault unreachability |
| X-03 | Foundation spec drifts from implementation — team implements a different permission model | H | Capability contract YAML is the source of truth; Keycloak SPI and API guard attributes are both generated from it; CI fails if they diverge |
| X-04 | Audit log volume causes storage cost escalation | M | Partition `audit_log` by `occurred_at` month; automated archival of partitions older than 2 years to object storage; retrieval API reads from both live table and archive |
| X-05 | PDPO (Brunei Personal Data Protection Order) breach — PII in logs | H | Structured logging framework configured with PII scrubber middleware; IC number, salary, bank account patterns are redacted before log emission; log pipeline tested quarterly |

---

### Risk Summary Matrix

| Domain | High | Medium | Low | Total |
| --- | --- | --- | --- | --- |
| BC-01 Identity | 2 | 2 | 1 | 5 |
| BC-02 Organisation | 1 | 2 | 1 | 4 |
| BC-03 Authority & Delegation | 4 | 2 | 0 | 6 |
| BC-04 Position Management | 3 | 1 | 1 | 5 |
| BC-05 Work Structure | 1 | 2 | 1 | 4 |
| BC-06 Approval Routing | 2 | 3 | 1 | 6 |
| BC-07 Rules Engine | 3 | 2 | 0 | 5 |
| Cross-Cutting Scalability | 0 | 3 | 1 | 4 |
| Cross-Cutting Operational | 3 | 2 | 0 | 5 |
| **Total** | **19** | **19** | **6** | **44** |

**All 19 High-severity risks must be mitigated and verified before the Foundation Architecture Package is marked production-ready.**

## Phase 3 — Multi-Tenancy

Circlate uses the **Database-per-Tenant** model. Each company tenant receives its own isolated PostgreSQL database, its own MinIO storage bucket, and its own Keycloak realm.

### Database-per-Tenant: Benefits and Drawbacks

| Aspect | Benefit | Drawback |
| --- | --- | --- |
| Isolation | Complete data separation — a bug cannot leak cross-tenant data | More databases to manage and monitor |
| Compliance | Per-tenant backup, restore, and deletion without touching other tenants | Schema migrations must run across all tenant DBs |
| Performance | No noisy-neighbour effect on query performance | Connection count grows with tenant count — requires PgBouncer |
| Customisation | Tenant-specific schema extensions possible (Enterprise tier) | Each tenant DB consumes base memory on Postgres |
| Security | Per-tenant encryption keys possible | Operational complexity for credential rotation |
| Recovery | Point-in-time restore for a single tenant without affecting others | Backup storage multiplies by tenant count |

**Recommendation: Database-per-Tenant.** For Circlate's target market (SMEs with strict data privacy expectations, government customers, oil & gas contractors with compliance mandates), the isolation guarantee justifies the operational overhead. PgBouncer connection pooling mitigates the connection count problem. Automated migration tooling (Flyway/EF Core migrations with tenant enumeration) handles schema propagation.

---

### Tenant Provisioning Process

**Trigger:** Customer completes company registration form and selects a plan (including Free).

**Orchestration:** `TenantProvisioningOrchestrator` service executes the following steps as a saga with compensating transactions on failure.

**Step-by-step provisioning flow:**

1. **Validate registration input** — company name, subdomain slug (uniqueness check), admin email, plan selection
2. **Reserve subdomain** — write `Tenant` record with status `Provisioning`; subdomain marked reserved
3. **Create Keycloak realm** — realm named `tenant-{subdomain}`; configure token lifetime, MFA policy, SMTP
4. **Create Keycloak admin user** — admin account with `SystemAdmin` role mapped
5. **Provision tenant database** — create PostgreSQL database `wos_{subdomain}`; run all EF Core migrations
6. **Seed reference data** — default leave types (Annual, Medical, Emergency), default departments (General), default shift (Standard 8–5)
7. **Provision MinIO bucket** — bucket named `wos-{subdomain}`; apply lifecycle policy (30-day temp file expiry)
8. **Create billing subscription** — call PocketPay API to create customer + subscription (trial or paid)
9. **Set tenant status to `Active`** — subdomain goes live
10. **Send welcome email** — admin receives login link, quick-start guide, and subdomain URL
11. **Create in-app onboarding checklist** — guided setup tasks presented on first login

**Failure compensation:** If any step fails, compensating actions run in reverse order (delete Keycloak realm, drop database, release subdomain). The failed provisioning is logged with the error step; the customer is shown a friendly retry screen.

---

### Customer Signup Flow

1. Customer visits `Circlate.app` → clicks **Start Free Trial** or **Get Started**
2. Registration form: company name, admin full name, work email, password, subdomain selection (auto-suggested from company name, editable)
3. Email verification — 6-digit OTP sent; must be verified within 15 minutes
4. Plan selection screen — Free / Business / Professional / Enterprise; credit card only required for paid plans
5. PocketPay checkout for paid plans; Free plan skips payment
6. Provisioning progress screen (animated; real-time WebSocket status updates from the orchestrator)
7. Redirect to `https://{subdomain}.Circlate.app` with onboarding wizard

---

### Trial Creation

- All paid plans begin with a **14-day free trial**; no credit card required for Business tier trial
- Professional and Enterprise tier trials require credit card at signup (card not charged until trial ends)
- Trial state stored in `Subscription.trial_ends_at`
- 7 days before expiry: email + in-app banner notification
- 1 day before expiry: email + push notification
- On expiry: plan downgrades to Free unless payment method confirmed
- Trial extension: System Admin can grant +7 days via admin panel (once per tenant)

---

### Subdomain Assignment

- Format: `{slug}.{projectname}.app` where slug is 3–30 characters, lowercase alphanumeric and hyphens
- Slug validation: not in reserved list (`admin`, `api`, `app`, `billing`, `mail`, `www`, `support`, `status`)
- Uniqueness enforced at the platform level (central subdomain registry table in the platform database)
- Custom domain support (Enterprise tier): CNAME verification via DNS TXT record; SSL via Let's Encrypt or customer-provided cert
- Subdomain routing: nginx/Traefik reverse proxy reads `Host` header → resolves `tenant_id` via `SubdomainResolver` → routes to application with `X-Tenant-Id` header injected

---

### Tenant Isolation

**Data isolation:**

- Each API request validated against `tenant_id` extracted from the JWT claim
- All EF Core queries automatically scoped with tenant-specific database connection string
- No shared application-layer caches that could mix tenant data
- MinIO presigned URLs scoped to tenant bucket; cross-bucket access is denied at policy level

**Network isolation (Mode A — SaaS):**

- All tenants share the same application pod fleet but are isolated at the data layer
- Keycloak realms are fully separate — users, roles, and tokens are not portable across tenants

**Compute isolation (Mode B — Dedicated Cloud / Mode C — Self-Hosted):**

- Single-tenant deployments have dedicated application, database, and storage containers
- No shared infrastructure with other customers

---

### Backup Strategy

| Component | Frequency | Retention | Method |
| --- | --- | --- | --- |
| Tenant PostgreSQL DB | Daily full + WAL continuous | 30 days rolling | pg\_dump + pgWAL archiving to object storage |
| MinIO buckets | Daily incremental | 90 days | MinIO mirror to secondary bucket / S3-compatible store |
| Keycloak realm config | Daily export | 30 days | Keycloak export API → JSON → object storage |
| Platform DB (subdomain registry, billing) | Daily full + WAL continuous | 90 days | Same as tenant DB |

**Backup storage location:**

- SaaS (Mode A): separate object storage bucket in a different availability zone
- Self-hosted (Mode C): customer-defined backup target via environment variable `BACKUP_STORAGE_URI` (supports S3, GCS, Azure Blob, local path)

**Backup encryption:** AES-256; backup encryption key stored in a separate secrets manager (HashiCorp Vault or Kubernetes Secret)

---

### Recovery Strategy

**RTO target:** 4 hours for full tenant restore; 1 hour for point-in-time restore of recent data

**RPO target:** 15 minutes (continuous WAL archiving)

**Recovery procedures:**

1. **Point-in-time recovery (PITR)** — restore tenant DB to any point within retention window using WAL replay; used for accidental data deletion
2. **Full tenant restore** — restore from daily pg\_dump; re-sync MinIO bucket from backup; re-import Keycloak realm config; update DNS if subdomain changed
3. **Partial restore** — restore specific tables (e.g. attendance records) using pg\_restore with `--table` flag; merge into live DB with conflict resolution
4. **Disaster recovery (Mode A)** — if primary region fails, promote read replica in secondary region; update DNS; estimated 2-hour promotion time
5. **Self-hosted customer recovery** — documented runbook provided; Circlate provides `restore.sh` script in the Docker Compose package

**Recovery testing:** Monthly automated restore test on a randomly selected tenant (staging environment); results logged and reviewed by DevOps.

---

### Deployment Mode Architecture Summary

| Concern | Mode A (SaaS) | Mode B (Dedicated) | Mode C (Self-Hosted) |
| --- | --- | --- | --- |
| Database | DB-per-tenant, shared cluster | Single DB, dedicated cluster | Single DB, customer-managed |
| Storage | Shared MinIO cluster, per-tenant bucket | Dedicated MinIO instance | Customer-provided S3-compatible |
| Auth | Shared Keycloak, per-tenant realm | Dedicated Keycloak | Customer-managed Keycloak |
| Routing | Subdomain → nginx → app | Direct | Direct or customer reverse proxy |
| Backups | Managed by Circlate | Managed by Circlate | Customer responsibility (tooling provided) |
| Air-gap support | No | Optional | Yes |

## Phase 4 — Module Definitions

### MODULE 1 — Employee Management

**Tier availability:** Free and above

**Purpose:** The canonical record of every person employed by the company. All other modules reference employee records — attendance, leave, expenses, compliance.

**Features:**

**Employee Profile**

- Personal details: full name, preferred name, IC/passport number, nationality, gender, date of birth, photo
- Employment details: employee number (auto-generated), hire date, employment type, position, department, reporting manager, employment status, probation end date
- Contact info: work email, personal email, mobile phone, work phone, home address
- Emergency contacts: up to 3 contacts with name, relationship, phone
- Bank details: bank name, account number (encrypted at rest; visible to HR/Finance only)
- Custom fields: HR-configurable additional fields per tenant (e.g. IC expiry, driver's licence, work permit number)

**Employment History**

- Timeline of position changes, department transfers, promotions
- Each entry: effective date, previous position, new position, reason, approved by
- Read-only audit trail; no deletion

**Skills (linked to Skills module)**

- Employee's rated skills displayed on profile
- Link to full Skills Matrix view

**Certifications (linked to Training Compliance module)**

- Summary of compliance status and upcoming certificate expiries on profile

**Documents (linked to Document Management module)**

- Contract, offer letter, ID copies visible per access permission

**Onboarding Workflow**

- Checklist assigned on employee creation: add photo, fill bank details, complete emergency contact, sign policy acknowledgement
- Completion percentage shown to HR and the employee

**Offboarding Workflow**

- Triggered on termination: asset return request raised, leave balance calculation, access revocation, final document generation

---

### MODULE 2 — Organisation Management

**Tier availability:** Free and above

**Features:**

**Departments**

- Hierarchical department tree (parent/child departments)
- Each department: name, code, parent department, manager, cost centre
- Unlimited depth

**Teams**

- Sub-groups within departments
- Each team: name, department, team lead, members\[\]

**Positions**

- Job title registry with grade and department
- Headcount budget per position (approved vs filled)
- Manager flag: designates position as a manager role for approval routing

**Reporting Lines**

- Employee-to-manager mapping with effective date
- Supports matrix reporting (employee can have both a line manager and a dotted-line manager)
- Used for leave and expense approval routing

**Organisation Chart**

- Interactive tree visualisation on web
- Pan, zoom, search, click to view employee card
- Export to PNG or PDF
- Mobile: collapsible tree view

**Headcount Planning**

- Dashboard view: approved headcount vs filled positions by department
- Open positions (unfilled): link to create job posting in Recruitment module

---

### MODULE 3 — Recruitment ATS

**Tier availability:** Business and above

**Features:**

**Job Postings**

- Create job posting: title, department, position, employment type, description, requirements, salary band (optional), closing date
- Status: Draft / Open / Closed / On Hold
- Internal-only or external posting

**Kanban Pipeline Board**

- Columns: Applied → Screening → Interview → Assessment → Offer → Hired / Rejected
- Drag-and-drop cards between stages
- Each card: candidate name, source, applied date, days in stage indicator
- Bulk actions: advance multiple candidates, send rejection emails
- Filter by: job posting, assignee, source, date range

**Candidate Profiles**

- Name, contact details, source, resume (PDF/DOCX upload stored in MinIO)
- Linked applications (a candidate can apply to multiple postings)
- Notes visible to all recruiters on the same job

**Interview Management**

- Schedule interview: interviewer(s), date/time, format (Phone/Video/In-Person), location/link
- Interview outcome: Proceed / Hold / Reject with notes
- Calendar view of all scheduled interviews

**Pipeline Reporting**

- Conversion rates by stage
- Time-to-hire (days from applied to hired)
- Source effectiveness (candidates and hires by source)
- Open roles vs pipeline volume

**Offer Management**

- Create offer: salary, start date, offer expiry
- Status tracking: Sent / Accepted / Rejected / Expired
- On acceptance: triggers employee creation workflow in Employee module

---

### MODULE 4 — Attendance

**Tier availability:** Free and above

**Clock-in Methods:**

1. **QR Attendance** — employee scans a unique per-employee QR code (or company location QR code) using the mobile app. QR tokens rotate every 24 hours.
2. **GPS Attendance** — employee's device location recorded on clock-in; HR configures acceptable office geofence radius (default 100 m).
3. **QR + GPS** — both required simultaneously; highest assurance mode.
4. **Manual Entry** — HR can manually record attendance (e.g. paper register backup). Flagged as `Manual` in reports.

**Offline Sync**

- Clock-in attempts saved to local device storage when offline
- Sync queue transmitted when connection restored (up to 24-hour queue)
- Server-side idempotency key prevents duplicate records
- Conflict resolution: server timestamp wins; offline clock-in flagged as `Synced-Offline` in reports

**Work Patterns Supported:**

- Standard (fixed shift: e.g. 8:00–17:00 Mon–Fri)
- Flexible (core hours + window: e.g. arrive 7:00–10:00, leave 8h later)
- Shift work (rotating shifts with shift assignment calendar)
- Remote/Hybrid (clock-in from any location; GPS not required; flagged as Remote)

**Overtime Detection**

- Rules configured per shift: overtime threshold (e.g. >8h in a day, or clock-out after shift end + 30 min buffer)
- Overtime calculated in 15-minute increments
- Overtime report for manager review; optional approval flow

**Late Arrivals**

- Late threshold configurable per shift (e.g. clock-in > 5 min after shift start = Late)
- Late arrival event triggers notification to manager
- Late report shows frequency per employee over period

**Attendance Dashboard**

- Today's real-time attendance status across team/department
- Monthly calendar view per employee (Present / Late / Absent / Leave / Holiday / Remote)
- Attendance summary report: total days, absent days, late count, overtime hours

---

### MODULE 5 — Leave Management

**Tier availability:** Free and above

**Leave Types (configurable per tenant):**

| Type | Typical Days | Paid | Notes |
| --- | --- | --- | --- |
| Annual Leave | 14–21 | Yes | Configurable carry-over |
| Medical Leave | 14 | Yes | MC document optional/required toggle |
| Emergency Leave | 3 | Yes | No advance request |
| Maternity Leave | 60–90 | Yes | Country-specific |
| Paternity Leave | 7 | Yes | Country-specific |
| Unpaid Leave | Variable | No | Requires HR approval |
| Custom | Configurable | Configurable | Tenant-defined |

**Leave Request Flow:**

1. Employee submits request (mobile or web): leave type, dates, reason, attachment (for medical)
2. Push notification to approving manager
3. Manager approves / rejects with optional comment (one-tap on mobile)
4. Employee notified of outcome
5. On approval: balance deducted, attendance record updated to `Leave`
6. On rejection: balance unchanged, employee notified

**Leave Balance Management:**

- Annual accrual on employee anniversary or calendar year (configurable)
- Carry-over cap per leave type
- Balance visible to employee (available, taken, pending, carried over)
- HR can manually adjust balances with reason logged

**Leave Calendar:**

- Team/department calendar showing approved leave periods
- Manager visibility: who is on leave vs who is in
- Public holiday calendar imported per tenant locale (Brunei public holidays built-in; custom holidays addable)

---

### MODULE 6 — Expense Management

**Tier availability:** Business and above

**Expense Claim Flow:**

1. Employee creates claim: add one or more expense items (category, description, amount, date, receipt photo)
2. Submit claim for approval
3. Manager reviews and approves/rejects
4. If approved: claim moves to Finance queue
5. Finance approves and marks as Paid; optionally records payment reference

**Expense Items:**

- Category selection: Meals / Travel / Accommodation / Equipment / Training / Other
- Receipt: photo upload from mobile camera or file picker; stored in MinIO per tenant bucket
- Currency: BND default; multi-currency display (conversion for reporting)
- Description and merchant name fields

**Approval Workflow:**

- Two-step: Manager → Finance (configurable; can be single-step)
- Delegation: manager can delegate approval to another manager during leave
- Rejection with mandatory comment; employee can resubmit after editing

**Finance Export:**

- Export approved claims to CSV or Excel
- Columns: employee name, employee number, category, amount, claim date, approved date, payment ref
- Filtered by department, date range, status

---

### MODULE 7 — Performance Management

**Tier availability:** Professional and above

**Goal Management:**

- Employee and manager set goals collaboratively in a review cycle
- Goal structure: title, description, success metric, weight (%), target date, progress % (self-updated)
- Goal types: OKR (Objectives & Key Results) or KPI (Key Performance Indicator)
- Mid-cycle progress check-ins

**Review Cycles:**

- HR creates review cycle: name, type (Annual / Mid-Year / Probation / 360), period start/end, participants
- Cycle stages: Goal Setting → Mid-Year Check-in → Self Assessment → Manager Review → Calibration → Published
- HR controls stage advancement

**Review Form:**

- Self-assessment: employee rates own goals and provides comments
- Manager assessment: rates employee goals, provides overall rating and development commentary
- Overall rating: 1–5 scale (Needs Improvement / Developing / Meets Expectations / Exceeds Expectations / Outstanding)
- Finalised reviews locked from editing

**360 Feedback:**

- Employee nominates peers for feedback
- Anonymous peer responses (names hidden from employee; visible to HR)
- Aggregated feedback summary included in review

---

### MODULE 8 — Skills Matrix

**Tier availability:** Professional and above

**Skill Taxonomy:**

- HR defines skill categories (Technical, Soft Skills, Industry-Specific, etc.) and individual skills within each
- Proficiency scale: 1 Beginner → 5 Expert
- Skills linked to positions (required skills per position)

**Employee Skill Profile:**

- HR or manager rates employee on each relevant skill
- Self-assessment option (pending manager confirmation)
- History of skill rating changes over time

**Skills Matrix View:**

- Grid: employees (rows) × skills (columns)
- Cell: proficiency rating with colour coding (red = below required, amber = at minimum, green = exceeds)
- Filter by department, team, position
- Export to Excel

**Succession Planning:**

- HR marks positions as succession-critical
- Nominate candidates with readiness level (Ready Now / 1–2 Years / 3+ Years)
- Gap analysis: candidate skills vs position required skills

---

### MODULE 9 — Document Management

**Tier availability:** Free and above

**Document Library:**

- Company-level documents: policies, handbooks, templates
- Employee-level documents: contracts, offer letters, ID copies, certificates
- Folder structure: HR-defined categories

**Upload and Storage:**

- Accepted formats: PDF, DOCX, XLSX, JPG, PNG (max 50 MB)
- Stored in MinIO per-tenant bucket under `/documents/` prefix
- Virus scan on upload (ClamAV integration optional in self-hosted mode)

**Access Control:**

- HR visibility: all documents
- Employee visibility: documents explicitly flagged `is_employee_visible = true`
- Manager visibility: direct report documents (configurable)

**Version Control:**

- New upload = new version; previous versions retained
- Version history visible to HR

**Expiry Tracking:**

- Documents can have an expiry date (work permits, medical certificates)
- Alert sent 30 days before expiry

---

### MODULE 10 — Asset Management

**Tier availability:** Professional and above

**Asset Registry:**

- Asset record: asset tag (barcode/QR), name, category, brand, model, serial number, purchase date, purchase value, warranty expiry, condition, status, notes
- Categories: Phone / Laptop / Vehicle / Access Card / Tool / Other
- Status: Available / Assigned / Under Repair / Retired

**Assignment:**

- Assign asset to employee: effective date, expected return date, condition at assignment, acknowledgement notes
- Employee sees their assigned assets on profile
- Asset history: full assignment timeline

**Return:**

- Return process: condition at return, return date, HR notes
- Asset condition delta flagged for review (e.g. assigned as Good, returned as Damaged)
- Termination trigger: auto-raises asset return request for all assigned assets

---

### MODULE 11 — Announcements

**Tier availability:** Free and above

**Post Types:**

- Company-wide: all employees see it
- Department-targeted: employees in specified department(s) only
- Team-targeted: employees in specified team(s) only

**Rich Content:**

- Title, body (rich text: bold, italic, lists, links)
- Attachment: single file upload (PDF, image)
- Pinned announcements appear at top of feed

**Publishing:**

- Draft → Scheduled (optional publish\_at) → Published → Expired (optional expires\_at)
- Mobile push notification sent on publish to targeted employees

**Read Receipts:**

- Track which employees have opened the announcement
- Read rate % shown to HR
- Export list of employees who have not read (for follow-up)

---

### MODULE 12 — Helpdesk

**Tier availability:** Business and above

**Ticket Submission:**

- Employee submits via web or mobile: category (HR / IT / Facilities), subject, description, optional attachment
- Reference number auto-generated

**Ticket Categories and Routing:**

- HR tickets → assigned to HR team inbox
- IT tickets → assigned to IT team inbox
- Facilities tickets → assigned to Facilities inbox
- Auto-assignment by category; manual reassignment within team

**Ticket Lifecycle:**

- Open → In Progress → Resolved → Closed
- Comment thread on each ticket (employee and agent both visible)
- SLA tracking: configurable per category (e.g. HR = 2 business days, IT = 4 hours for Urgent)
- Escalation: auto-escalate if no response within SLA window

**Agent View:**

- Queue by category
- Filter by status, priority, age
- Bulk close/resolve
- Average resolution time report

## Phase 5 — Training Compliance

**This is NOT an LMS.** Circlate does not deliver course content. It tracks whether employees have completed required training, holds their certificates, monitors expiry dates, and reports compliance status to managers and HR. Training delivery happens with external providers; Circlate records the evidence.

### Core Concepts

| Concept | Definition |
| --- | --- |
| Training Provider | External organisation delivering the training (e.g. Red Crescent, NIOSH) |
| Course | A specific training programme with a defined validity period (e.g. First Aid — valid 2 years) |
| Compliance Requirement | A rule linking a Course to a Department or Position, with a required-by date |
| Training Record | An employee's record of completing a Course: completion date, expiry, certificate file |
| Compliance Status | Computed state per employee per requirement: Compliant / Expiring Soon / Expired / Not Started |

### Examples of Tracked Training

| Course | Sector | Typical Validity |
| --- | --- | --- |
| First Aid (Occupational) | All sectors | 2 years |
| Food Handling / Food Safety | F&B, Hospitality | 1 year |
| Working at Height | Construction, O&G | 2 years |
| Fire Safety (Basic) | All sectors | 3 years |
| H2S Safety (Hydrogen Sulphide) | Oil & Gas | 2 years |
| BOSIET (Basic Offshore Safety) | Oil & Gas Offshore | 4 years |
| HUET (Helicopter Underwater Escape) | Oil & Gas Offshore | 4 years |
| Defensive Driving | Construction, Security | 3 years |
| Security Guard Licence | Security | 1 year |
| Forklift Operator Licence | Manufacturing, Warehousing | 3 years |
| Confined Space Entry | Construction, O&G | 2 years |

---

### Data Model

**TrainingProvider**

- id, name, accreditation\_body, contact\_email, contact\_phone, website, notes

**Course**

- id, name, provider\_id, description, category, validity\_months, is\_mandatory\_globally, created\_by, is\_active
- Category: Safety / Compliance / Licence / Technical / Soft Skills

**ComplianceRequirement**

- id, course\_id, scope\_type (Department / Position / All), scope\_ids\[\], required\_by\_date (deadline for new hires), is\_active
- Multiple requirements can reference the same course (e.g. First Aid required for Department: Construction AND Position: Site Supervisor)

**TrainingRecord**

- id, employee\_id, course\_id, provider\_id, completion\_date, expiry\_date, certificate\_url (MinIO ref), status, uploaded\_by, notes
- Status: Active / Expired / Revoked

**ComplianceAlert**

- id, employee\_id, course\_id, training\_record\_id, alert\_type (90Day / 60Day / 30Day / Expired), scheduled\_at, sent\_at, channels\[\]

---

### Compliance Requirement Setup Workflow

1. **Compliance Admin opens Training Compliance module**
2. **Creates or selects a Training Provider** — name, accreditation body, contact details
3. **Creates a Course** — name, description, provider, category, validity period (months)
4. **Creates a Compliance Requirement** — links course to scope:
   - Scope: All Employees / Specific Departments / Specific Positions
   - Required-by date: how soon new hires must complete (e.g. within 30 days of hire)
5. **Requirement activates** — Compliance Matrix automatically recalculates for all in-scope employees
6. **Employees with no existing record** appear as `Not Started` immediately

---

### Certificate Upload Workflow (Employee)

1. Employee receives notification: "Your First Aid certificate expires in 30 days"
2. Employee attends training with external provider, receives physical/digital certificate
3. Employee opens Circlate mobile app → Training → My Certificates
4. Taps **Upload Certificate** next to the course
5. Selects photo from camera or file picker (PDF/JPG/PNG)
6. Enters: Completion date, Expiry date, Training provider (pre-populated from requirement)
7. Submits → certificate uploaded to MinIO; Training Record created with status `Pending Verification`
8. HR/Compliance Admin receives notification: "Wafi Muhamad uploaded First Aid certificate — pending verification"
9. Admin reviews: opens certificate file, verifies details match
10. Admin approves or rejects with note
11. On approval: Training Record status → `Active`; Compliance Status → `Compliant`; expiry alerts scheduled
12. On rejection: employee notified with admin's reason; prompted to re-upload

---

### Certificate Upload Workflow (HR on behalf of employee)

1. HR opens employee profile → Training Records tab
2. Clicks **Add Training Record**
3. Selects course, enters completion date and expiry date
4. Uploads certificate file
5. Record created as `Active` immediately (no approval step — HR action is authoritative)

---

### Expiry Tracking and Alert Workflow

**Alert schedule:** Daily cron job (`ExpiryAlertScheduler`) runs at 06:00 tenant timezone.

**For each active Training Record:**

- If expiry\_date = today + 90 days → dispatch `90Day` alert (if not already sent)
- If expiry\_date = today + 60 days → dispatch `60Day` alert
- If expiry\_date = today + 30 days → dispatch `30Day` alert
- If expiry\_date = today → dispatch `Expired` alert
- If expiry\_date < today → update record status to `Expired`; update compliance status to `Expired`

**Alert channels:**

- **Employee:** push notification (mobile) + in-app notification + email
- **Direct manager:** email notification listing direct reports with expiring certs
- **Compliance Admin:** daily digest of all alerts sent that day (configurable)

**Alert content (example — 30-day alert):**

> "Your First Aid certificate expires on 15 Dec 2026. Please renew and upload the new certificate before the expiry date to remain compliant."

---

### Compliance Matrix

The compliance matrix is the central compliance view — a grid showing every in-scope employee against every compliance requirement for their department/position.

**Matrix dimensions:**

- Rows: Employees (filterable by department, position, manager)
- Columns: Active compliance requirements applicable to employee's department or position

**Cell values:**

| Status | Display | Meaning |
| --- | --- | --- |
| Compliant | Green | Active record, not expiring within 90 days |
| Expiring Soon | Amber | Active record, expiry within 90 days |
| Expired | Red | Record expired |
| Not Started | Grey | No record on file |
| Pending | Blue | Certificate uploaded, awaiting admin verification |
| N/A | — | Requirement does not apply to this employee's scope |

**Matrix interactions:**

- Click cell → view training record details or upload prompt
- Filter by status (show only Red + Amber rows)
- Export matrix to Excel (full grid with employee details and status per column)
- Print-friendly view for audit presentation

---

### Department / Position Requirements View

**Purpose:** HR and Compliance Admin can see which courses are required for each department or position, and the aggregate compliance rate.

**Department Compliance Dashboard:**

- Department name
- Total employees in scope
- Required courses (count)
- Compliance rate % (employees fully compliant / total in scope)
- Breakdown by status: Compliant / Expiring / Expired / Not Started
- Drill-down to list of non-compliant employees

---

### Compliance Reporting

**Report 1 — Overall Compliance Summary**

- Tenant-wide: total employees, fully compliant %, by-status breakdown
- Filter by department, position, course, date range

**Report 2 — Non-Compliance Report**

- Lists every employee with at least one Expired or Not Started requirement
- Columns: employee name, department, course, status, expiry date, days overdue
- Export to CSV/PDF; use as audit evidence

**Report 3 — Upcoming Expiries**

- Certificates expiring in the next 30 / 60 / 90 days
- Useful for proactive training scheduling

**Report 4 — Training History**

- Complete training record timeline per employee
- All completed courses, providers, dates, certificate links

---

### Manager Compliance View

- Manager sees compliance status for direct reports only (not full company)
- Dashboard widget on Manager Dashboard: team compliance rate, red/amber count with link to drill-down
- Manager receives weekly email digest if any direct reports are non-compliant
- Manager cannot upload or approve certificates (HR/Compliance Admin only) — view-only by default; configurable

---

### Integration with Other Modules

| Module | Integration |
| --- | --- |
| Employees | On `EmployeeOnboarded` event: apply applicable compliance requirements based on department/position; create `Not Started` records |
| Notifications | All alerts dispatched via Notifications BC |
| Documents | Certificate files stored via Document Management MinIO infrastructure |
| Reporting | Compliance reports embedded via Metabase with tenant-scoped data source |
| Organisation | Requirement scope resolves against current department/position assignments |

## Phase 6 — Security

### Authentication

**Authority: Keycloak**

Keycloak is the single authentication authority. All authentication flows — username/password, SSO, MFA — go through Keycloak. The Circlate application trusts Keycloak-issued JWTs and never stores passwords directly.

**Authentication flows supported:**

- Username + password (standard form login)
- TOTP (Time-based One-Time Password) via authenticator app — optional for employees, enforceable by HR
- SMS OTP — configurable per tenant (requires SMS provider integration; Phase 2)
- SSO — OIDC and SAML 2.0 federation (Enterprise tier); supports Azure AD, Google Workspace, Okta
- Magic link — email-based passwordless login (optional; Phase 2)

**Token strategy:**

- Access token: short-lived (15 minutes); JWT signed with realm RS256 key
- Refresh token: 8 hours; stored in HTTP-only cookie on web; in secure storage on mobile
- Token claims: `sub` (user id), `tenant_id`, `roles[]`, `email`, `exp`
- Token validation: every API request validates JWT signature and expiry via Keycloak JWKS endpoint (cached with 5-minute TTL)

**Password policy (configurable per tenant, enforced by Keycloak):**

- Minimum length: 8 characters
- Complexity: uppercase + lowercase + number required
- History: cannot reuse last 5 passwords
- Expiry: configurable (default: none; HR can enforce 90-day rotation)
- Lockout: 5 failed attempts → 15-minute lockout

---

### Authorisation — RBAC Design

Authorisation uses Role-Based Access Control (RBAC). Roles are defined at the platform level and assigned per tenant. Each role carries a set of permissions scoped to resources and actions.

**Role hierarchy:**

| Role | Description |
| --- | --- |
| System Admin | Platform-level admin (SaaS only); manages tenants, billing, global config |
| Company Admin | Full company configuration, billing, user management within own tenant |
| HR Manager | Full HR access: employees, recruitment, leave, compliance, documents |
| Recruiter | Recruitment module only: job postings, candidates, pipeline |
| Finance | Expense approval, billing visibility, finance reports |
| Compliance Admin | Training compliance: courses, requirements, certificate approval |
| Manager | View + approve for direct reports: leave, expenses, attendance, performance |
| Employee | Self-service only: own profile, attendance, leave, expenses, documents |

**Manager scope:** Managers can only access data for their direct reports (and optionally sub-reports if configured). The `ReportingLine` table determines their access scope — not role alone.

---

### Permissions Matrix

| Resource | Employee | Manager | HR Manager | Recruiter | Finance | Compliance Admin | Company Admin |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Own profile | Read/Edit | — | — | — | — | — | — |
| All employee profiles | — | Read (direct reports) | Full CRUD | — | Read | Read | Full CRUD |
| Organisation structure | Read | Read | Full CRUD | Read | Read | Read | Full CRUD |
| Attendance — own | Read | — | — | — | — | — | — |
| Attendance — team | — | Read + Manual entry | Full CRUD | — | — | — | Full CRUD |
| Leave — own | Submit/Cancel | — | — | — | — | — | — |
| Leave — team | — | Approve/Reject | Full CRUD | — | — | — | Full CRUD |
| Leave types / balances | Read own balance | Read team balance | Full CRUD | — | — | — | Full CRUD |
| Recruitment | — | — | Full CRUD | Full CRUD | — | — | Full CRUD |
| Expenses — own | Submit/View | — | — | — | — | — | — |
| Expenses — team | — | Approve/Reject | View | — | Approve/View | — | Full CRUD |
| Performance — own | Submit self-review | — | — | — | — | — | — |
| Performance — team | — | Submit manager review | Full CRUD | — | — | — | Full CRUD |
| Skills | View own | View team | Full CRUD | — | — | — | Full CRUD |
| Training records — own | Upload cert | — | — | — | — | — | — |
| Training records — team | — | View | Full CRUD | — | — | Full CRUD | Full CRUD |
| Compliance requirements | — | — | Read | — | — | Full CRUD | Full CRUD |
| Assets — own | View assigned | — | — | — | — | — | — |
| Assets — all | — | — | Read | — | — | — | Full CRUD |
| Documents — own | View (if visible) | — | — | — | — | — | — |
| Documents — all | — | — | Full CRUD | — | — | — | Full CRUD |
| Announcements | Read | Create (team) | Full CRUD | — | — | — | Full CRUD |
| Helpdesk — own tickets | Submit/View | — | — | — | — | — | — |
| Helpdesk — all tickets | — | — | Manage HR queue | — | — | — | Full CRUD |
| Reports | — | Team reports | All reports | Pipeline only | Expense reports | Compliance reports | All reports |
| Billing / subscription | — | — | — | — | View invoices | — | Full CRUD |
| System config | — | — | — | — | — | — | Full CRUD |

---

### Audit Logging

**Every write operation in the system is logged** in a dedicated `audit_log` table per tenant database.

**Audit log record:**

- `id` — UUID
- `tenant_id`
- `actor_user_id` — who performed the action
- `actor_role` — their role at time of action
- `action` — verb: CREATE / UPDATE / DELETE / APPROVE / REJECT / LOGIN / LOGOUT / EXPORT
- `resource_type` — e.g. Employee, LeaveRequest, TrainingRecord
- `resource_id` — the affected record's UUID
- `before_snapshot` — JSON of record state before change (nullable for CREATE)
- `after_snapshot` — JSON of record state after change (nullable for DELETE)
- `ip_address`
- `user_agent`
- `occurred_at` — UTC timestamp

**Retention:** 7 years (configurable per tenant; Enterprise tier can configure longer retention).

**Sensitive field masking:** Bank account numbers, IC numbers, and salary data are masked in snapshots (last 4 chars visible; full value never logged).

**Audit log access:** Company Admin and HR Manager can search and export audit logs via the Security & Audit section of Settings. System Admin can query all tenants.

**Tamper protection:** Audit log rows are append-only (no UPDATE/DELETE permission on `audit_log` table in application role; only INSERT). Periodic hash-chain verification for Enterprise tier.

---

### Mobile Security

- JWT access token stored in Flutter `flutter_secure_storage` (iOS Keychain / Android Keystore)
- Refresh token stored in encrypted secure storage; not in `SharedPreferences`
- Certificate pinning (optional; configurable for Enterprise tier)
- Biometric authentication: app can require FaceID/TouchID/fingerprint before showing sensitive screens (configurable by Company Admin)
- Screen capture prevention on sensitive screens (profile, documents, pay info) via Flutter `secure_flag`
- Offline data: only attendance clock-in queue cached locally; employee profile data is never cached to disk
- App timeout: auto-lock after 15 minutes of inactivity (configurable)
- Root/jailbreak detection: warn user; Company Admin can enforce denial (Phase 2)

---

### API Security

- All API endpoints require a valid JWT (`Authorization: Bearer <token>`)
- Rate limiting: 100 requests/minute per authenticated user; 20 requests/minute for unauthenticated endpoints
- CORS: restricted to `*.{projectname}.app` and configured custom domains
- HTTPS enforced; HTTP redirects to HTTPS; HSTS header set
- Input validation: all request DTOs validated with FluentValidation; validation errors return 400 with structured error body
- SQL injection prevention: EF Core parameterised queries only; raw SQL prohibited in application code
- File upload security: MIME type validation, extension whitelist, virus scan hook (ClamAV optional)
- Webhook endpoints: HMAC-SHA256 signature verification for PocketPay webhooks
- API versioning: `/api/v1/`; breaking changes require a new version
- Secrets management: connection strings and API keys in environment variables; never in source code

---

### Document Security

- All documents stored in MinIO per-tenant bucket
- Files accessed via signed URLs (15-minute expiry); direct bucket access not exposed to clients
- Bucket policy: application service account has read/write; no public access
- Employee-visible flag controls whether a document appears in employee's self-service view
- Document download logged to audit log
- HR-only documents (bank details, salary letters) are never returned in employee API responses, regardless of URL guessing

---

### Data Privacy

- IC numbers and passport numbers: encrypted at rest using column-level encryption (AES-256)
- Salary / bank account data: encrypted at rest; role-restricted in API layer
- Right to erasure: `Employee` soft-delete with configurable hard-delete after retention period; audit log retained but PII anonymised
- Data export: HR can export all employee data as JSON/CSV (PDPO/GDPR compliance tool)
- Data residency: tenant's database provisioned in the region selected at signup; no cross-region data replication without explicit consent

## Phase 7 — UI/UX Design

### Design Philosophy

Circlate is designed to feel like the tools the best software teams use — not like enterprise HR software. The goal is a product that an employee picks up and uses without training, that a manager checks every morning without dread, and that HR builds workflows in without calling support.

**Inspiration:** Linear (precision, keyboard-first), Stripe (clarity, density without clutter), Notion (flexibility, calm), GitHub (information hierarchy), Vercel (dark/light mode done right).

**Anti-patterns to avoid:** SAP/Oracle nested accordion menus, excessive modal dialogues, 40-column tables with horizontal scroll, alert banners that never disappear, mandatory wizard flows that cannot be skipped.

---

### Design System

**Foundation:** ShadCN UI + Tailwind CSS. ShadCN provides accessible, composable primitives. Tailwind enforces constraint-based spacing and colour.

#### Colour Palette

**Light Mode:**

| Token | Hex | Usage |
| --- | --- | --- |
| `--background` | #FFFFFF | Page background |
| `--foreground` | #0A0A0A | Primary text |
| `--card` | #F9F9F9 | Card / panel background |
| `--card-foreground` | #0A0A0A | Card text |
| `--border` | #E5E5E5 | Dividers, input borders |
| `--input` | #FFFFFF | Input background |
| `--primary` | #18181B | Primary action (buttons) |
| `--primary-foreground` | #FAFAFA | Text on primary |
| `--secondary` | #F4F4F5 | Secondary buttons, tags |
| `--muted` | #F4F4F5 | Muted backgrounds |
| `--muted-foreground` | #71717A | Placeholder, helper text |
| `--accent` | #F4F4F5 | Hover states |
| `--destructive` | #EF4444 | Delete, error states |
| `--success` | #22C55E | Compliant, approved |
| `--warning` | #F59E0B | Expiring soon, pending |
| `--info` | #3B82F6 | Informational states |

**Dark Mode:** Automatic via `prefers-color-scheme`; full dark palette provided with `--background: #09090B`, `--card: #18181B`, `--border: #27272A`.

**Brand Accent (tenant-configurable for white-label):**

- Default: `#18181B` (near-black) with `#FAFAFA` contrast
- Enterprise tenants can override with their brand colour via Company Settings → Branding

#### Semantic Colour Usage

| State | Colour | Example |
| --- | --- | --- |
| Success / Approved / Compliant | Green #22C55E | Leave approved badge, compliance cell |
| Warning / Expiring / Pending | Amber #F59E0B | Cert expiring badge, pending approval |
| Danger / Rejected / Expired | Red #EF4444 | Expired cert, rejected expense |
| Info / Scheduled / In Progress | Blue #3B82F6 | Scheduled announcement, ticket in progress |
| Neutral / Draft / N/A | Grey #71717A | Draft post, N/A compliance cell |

---

#### Typography

**Font stack:** `Inter` (Google Fonts) → `system-ui` → `sans-serif`

| Scale | Size | Weight | Line Height | Usage |
| --- | --- | --- | --- | --- |
| `text-2xl` | 24px | 700 | 32px | Page titles |
| `text-xl` | 20px | 600 | 28px | Section headings |
| `text-lg` | 18px | 600 | 28px | Card headings |
| `text-base` | 16px | 400 | 24px | Body text |
| `text-sm` | 14px | 400 | 20px | Secondary text, table cells |
| `text-xs` | 12px | 400 | 16px | Labels, badges, captions |

**Rules:**

- Maximum line length: 65 characters for body text paragraphs
- Never use `font-weight: 300` (thin) in UI — insufficient contrast at small sizes
- Monospace (`font-mono`) only for IDs, codes, and technical values

---

#### Spacing System

Tailwind's 4px base unit (`1 = 4px`). All layout spacing uses multiples of 4.

| Token | px | Usage |
| --- | --- | --- |
| `space-1` | 4px | Tight element gaps (icon + label) |
| `space-2` | 8px | Within-card internal spacing |
| `space-3` | 12px | Form field gaps |
| `space-4` | 16px | Card padding, section gaps |
| `space-6` | 24px | Between cards |
| `space-8` | 32px | Section padding |
| `space-12` | 48px | Page padding (desktop) |

**Radius:** `rounded-md` (6px) for inputs and cards; `rounded-full` for badges and avatars only.

---

### Component Library

All components built on ShadCN primitives. Key custom components:

**Avatar** — 32px / 40px / 48px circle; initials fallback when no photo; online indicator dot variant

**Badge** — status indicator; variants: `default`, `success`, `warning`, `destructive`, `outline`; always `text-xs font-medium`

**DataTable** — sortable, filterable, paginated table component with: column visibility toggle, row selection, bulk actions bar, inline search, sticky header; built on TanStack Table

**KanbanBoard** — drag-and-drop column board; cards with assignee avatar, stage duration badge; powered by `@dnd-kit`

**StatsCard** — metric + label + optional trend (up/down arrow with %) + sparkline variant

**CommandPalette** — `Cmd+K` / `Ctrl+K` global search; searches employees, documents, announcements; navigates to any module

**Sidebar** — collapsible; icons only when collapsed (tooltip on hover); keyboard-navigable; active state: `bg-accent` left border highlight

**Sheet** — right-side drawer (480px wide); used for record detail / edit forms; preferred over full-page navigation for quick actions

**Timeline** — chronological activity feed; used in employment history, audit log, ticket comments

**OrgChartNode** — employee card for org tree: photo, name, title, direct report count; expandable

---

### Navigation

**Desktop layout:**

```
[Sidebar: 240px] | [Main content area: flex-1]
```

Sidebar structure:

- Company logo + name (top)
- Global search bar
- Module navigation (grouped):
  - People: Employees, Organisation, Recruitment
  - Workforce: Attendance, Leave
  - Finance: Expenses
  - Compliance: Training, Skills
  - Performance: Goals, Reviews
  - Operations: Assets, Documents
  - Communication: Announcements, Helpdesk
  - Settings
- Current user avatar + name + role (bottom)
- Notification bell with count badge

**Module access** gated by tier: locked modules show a lock icon + upgrade prompt on hover.

**Breadcrumbs:** shown in page header for depth > 1 (e.g. Employees > Wafi Muhamad > Documents)

---

### Dashboard Framework

All dashboards composed from widget cards. HR, Manager, and Employee dashboards are pre-configured; Company Admin can rearrange (Phase 2).

**Widget grid:** 12-column CSS grid; widgets span 3, 4, 6, or 12 columns.

**Standard widgets:**

- Today's Attendance (live status ring)
- Pending Approvals (count + quick-action list)
- Leave Calendar (mini calendar with leave markers)
- Compliance Summary (compliance rate % with status bar)
- Recent Announcements (last 3 posts)
- Upcoming Birthdays / Anniversaries
- Headcount by Department (bar chart)
- Open Positions (Recruitment module)

---

### Responsive Behaviour

**Breakpoints:**

| Breakpoint | Width | Layout |
| --- | --- | --- |
| Mobile | < 768px | Single column; bottom nav bar |
| Tablet | 768px – 1024px | Sidebar collapses to icons; content fills |
| Desktop | > 1024px | Full sidebar + content |
| Wide | > 1440px | Max content width 1280px; centred |

**Mobile-specific patterns:**

- Bottom navigation bar (5 tabs: Home, Attendance, Leave, Approvals, Profile)
- Sheets replace sidebars for record detail
- Tables replaced by card lists
- Forms use full-screen flow with Back/Next navigation
- Touch target minimum: 44×44px

**Tablet patterns:**

- Sidebar icon-only (collapsed by default; tap to expand as overlay)
- Two-column layouts become single column for forms; two-panel for lists + detail

---

### Accessibility Standards

**Target: WCAG 2.1 AA compliance**

| Requirement | Implementation |
| --- | --- |
| Colour contrast | Minimum 4.5:1 for body text; 3:1 for large text and UI components |
| Keyboard navigation | All interactive elements reachable by Tab; focus ring always visible (outline-2 ring) |
| Screen reader support | ARIA labels on all icon-only buttons; role attributes on custom components |
| Form errors | Error messages associated with inputs via `aria-describedby`; not colour-only |
| Images | Alt text on all images; decorative images `alt=""` |
| Motion | Respect `prefers-reduced-motion`; disable animations globally when set |
| Language | `lang` attribute set on `<html>`; Malay (Phase 2) |
| Focus management | Modal and Sheet trap focus; return focus to trigger on close |

---

### Design Tokens — ShadCN CSS Variables

The complete token set is defined in `globals.css` as CSS custom properties and mapped to Tailwind via `tailwind.config.ts`. Tokens cover: background, foreground, card, popover, primary, secondary, muted, accent, destructive, border, input, ring, radius — in both `:root` (light) and `.dark` class variants. All ShadCN components reference these tokens, ensuring a consistent theme that respects the user's OS preference and tenant brand overrides.

## Phase 8 — Screen Design

All screens described as high-fidelity layout specifications. Dimensions follow the Phase 7 design system.

---

### SCREEN 01 — Login

**Layout:** Centred card (480px wide) on a background gradient (white → `#F9F9F9`). Logo centred above card.

**Elements:**

- Company/product logo (96px)
- Heading: "Sign in to Circlate" (text-2xl, font-bold)
- Subdomain input (pre-filled if accessed via `company.projectname.app`): greyed out, non-editable — shows company slug
- Email input (label: "Work email")
- Password input with show/hide toggle
- "Forgot password?" link (right-aligned, text-sm)
- Primary button: "Sign in" (full width)
- Divider: "or" separator
- SSO button: "Continue with SSO" (outline variant, only shown if tenant has SSO configured)
- Footer: "Don't have an account? Start free →"

**States:** Loading spinner on button during auth; error state shows inline red banner below button ("Invalid email or password"); MFA step replaces form with TOTP/OTP input after successful password.

---

### SCREEN 02 — Company Registration

**Layout:** Centred card (560px), multi-step progress indicator (4 steps) at top.

**Step 1 — Company Details:**

- Company name (input)
- Industry (select: Retail / F&B / Hospitality / Construction / O&G / Professional Services / Manufacturing / Security / Other)
- Company size (select: 1–10 / 11–30 / 31–100 / 101–300 / 300+)
- Subdomain (input with `.projectname.app` suffix rendered inline; real-time availability check)

**Step 2 — Admin Account:**

- Full name, work email, password (with strength meter), confirm password

**Step 3 — Plan Selection:** (see Screen 03)

**Step 4 — Verification:**

- "Check your email" illustration
- OTP input (6 digits, auto-focus, auto-advance per digit)
- Resend link with 60-second cooldown timer

---

### SCREEN 03 — Subscription Selection

**Layout:** Full-page pricing table; centred; 4 tier columns.

**Each tier card:**

- Tier name (Free / Business / Professional / Enterprise) — bold, large
- Price: "BND X/month" or "Free" — text-3xl
- Tagline: one line describing who it's for
- Feature list (8–10 bullet points with check icons)
- CTA button: "Start Free" / "Start 14-Day Trial" / "Contact Sales"
- Recommended badge on Business tier (amber outline)

**Toggle:** Monthly / Annual billing (annual = 2 months free; badge shows savings)

**FAQ accordion** below pricing table (3–4 common questions)

---

### SCREEN 04 — Employee Dashboard

**Layout:** Sidebar (240px) + content area. Mobile: bottom nav.

**Header strip (full-width):**

- "Good morning, \[Name\]" greeting
- Today's date and day

**Widget row 1 (3 cards):**

- Clock status: "You're clocked in — 3h 24m today" with Clock Out button
- Leave balance: Annual X days remaining / Medical X days remaining (mini donut chart)
- Pending: X approvals waiting (links to approval inbox)

**Widget row 2:**

- My schedule this week (mini calendar strip — 5 days; colour-coded: green = present, grey = weekend, blue = leave)
- Recent announcements (last 2 posts; title + date + "Read" link)

**Quick actions bar:**

- Clock In / Request Leave / Submit Expense / Raise a Ticket (icon + label buttons)

**My Training (if compliance required):**

- Compact list of upcoming cert expiries
- Red/amber badges

---

### SCREEN 05 — Manager Dashboard

**Layout:** Same sidebar. 12-column widget grid.

**Row 1 (3 columns each):**

- Team Attendance Today: ring chart (present / absent / on leave counts)
- Pending Approvals: stacked list of leave/expense requests needing action; each row: name, type, date, Approve/Reject inline
- Compliance Alerts: count of team members with expiring certs; link to Compliance Matrix

**Row 2 (6 + 6):**

- Team leave calendar this month (colour blocks per employee)
- Recent activity feed (team clock-ins, approvals, ticket submissions)

**Row 3:**

- Open positions in my department (links to Recruitment Kanban)

---

### SCREEN 06 — HR Dashboard

**Layout:** Dense information dashboard; 12-column grid.

**Top metrics strip (6 stat cards):** Total Employees | Active Today | On Leave | Open Positions | Compliance Rate % | Pending Expenses

**Left panel (8 cols):**

- Headcount trend: line chart (12 months)
- Department headcount: bar chart (approved vs filled)

**Right panel (4 cols):**

- Upcoming milestones: probation end dates, work permit expiries, anniversaries (next 14 days)
- Pending tasks: employees with incomplete onboarding checklists

---

### SCREEN 07 — Recruitment Kanban

**Layout:** Full-width horizontal scroll board.

**Header:**

- Job posting selector dropdown (or "All Postings" view)
- Filters: Stage, Assignee, Source, Date range
- "+ New Job Posting" button (right)
- Pipeline stats strip: Total Applications | Avg. Time to Hire | Hired this month

**Kanban Board:**

- 7 columns: Applied / Screening / Interview / Assessment / Offer / Hired / Rejected
- Each column header: stage name + card count badge
- Each card:
  - Candidate name (bold)
  - Source badge (LinkedIn / Direct / Referral)
  - Days in stage indicator (amber if > 7 days)
  - Assignee avatar
  - Quick action: "Move →" chevron
- Drag-and-drop between columns
- Click card: Sheet opens (candidate detail — resume, notes, interview history, action buttons)

---

### SCREEN 08 — Employee Profile

**Layout:** Profile header + tab navigation + tab content.

**Profile header:**

- Large avatar (96px) with upload overlay
- Name (text-2xl bold), job title (text-lg muted), department, employee number badge
- Status badge (Active / Probation / On Leave)
- Quick stats: Hire Date | Tenure | Direct Reports count
- Action buttons (HR-visible): Edit, Deactivate, Reset Password

**Tab navigation:** Personal | Employment | Documents | Training | Skills | Assets | History | Attendance | Leave

**Personal tab:**

- Two-column form layout: IC number, DOB, nationality, gender, marital status, home address, personal email, mobile
- Emergency contacts section (card per contact)
- Bank details section (masked; "Reveal" button with re-auth for Finance role)

**Employment tab:**

- Current position, department, manager, employment type, start date, probation end, work schedule
- Compensation band (HR/Finance only)
- Employment history timeline (position changes, transfers, promotions)

---

### SCREEN 09 — Attendance Dashboard

**Layout:** Sidebar + content; tabbed: Overview / My Attendance / Team (manager view)

**Overview tab:**

- Date navigator (prev/next day; date picker)
- Real-time employee attendance list: avatar + name + clock-in time + method badge (QR / GPS) + status badge
- Summary row: X Present / X Late / X Absent / X On Leave

**My Attendance tab:**

- Monthly calendar view: each day coloured by status
- Monthly summary: total working days / present / late / absent / overtime hours
- Overtime request button

**Daily detail panel (Sheet):**

- Clock-in time, clock-out time, total hours, method, GPS map pin (if applicable)

---

### SCREEN 10 — Leave Requests

**Layout:** Split: left panel = request form / right panel = team calendar

**Leave request form:**

- Leave type selector (chips/segmented control)
- Date range picker (calendar inline)
- Working days count (auto-calculated, excluding public holidays)
- Reason text area
- Attachment upload (for medical leave)
- Submit button with balance preview: "This will use 2 of your 14 remaining Annual Leave days"

**Team calendar panel:**

- Monthly calendar
- Colour overlay per employee for approved leave
- My pending requests shown in dashed outline

**Leave balance summary (top of page):**

- Card per leave type: Available / Taken / Pending / Carry-over

---

### SCREEN 11 — Expense Claims

**Layout:** List + Sheet detail

**Claims list:**

- Table: Date submitted | Description | Amount | Status badge | Approver
- Status filter tabs: All / Pending / Approved / Paid / Rejected
- "+ New Claim" button

**New claim Sheet (480px):**

- Claim name/description
- Add expense item button → item row: category selector, description, amount, date, receipt upload (camera/file)
- Multiple items per claim
- Total amount auto-summed
- Submit button

**Item receipt viewer:**

- Thumbnail preview with expand-to-full overlay
- Remove item option

---

### SCREEN 12 — Training Compliance Matrix

**Layout:** Full-width table with frozen first column.

**Header controls:**

- Filter: Department selector | Position selector | Status filter (Compliant / Expiring / Expired / Not Started)
- Export button
- Last calculated timestamp

**Matrix table:**

- Row 1 (header): Employee Name | \[Course 1\] | \[Course 2\] | \[Course 3\] … (one column per active requirement)
- Each data cell: coloured status badge (Green / Amber / Red / Grey / Blue)
- Click cell: Sheet opens with training record detail + upload option
- Row average: "X/Y compliant" at row end
- Column footer: compliance rate % per course

---

### SCREEN 13 — Certification Tracking

**Layout:** Employee-centric view (from employee profile → Training tab) OR course-centric view (from Compliance module)

**Employee Training tab:**

- List of all requirements applicable to this employee
- Each row: Course name | Provider | Completed date | Expiry date | Status badge | Certificate (download link) | Actions
- "Upload Certificate" button per row (if not compliant)

**Course-centric view (Compliance Admin):**

- Select course → see all employees with that course in scope
- Table: Employee | Department | Status | Expiry date | Days until expiry
- Sort by expiry date ascending (soonest expiry first)

---

### SCREEN 14 — Skills Matrix

**Layout:** Similar to Compliance Matrix — full-width grid.

**Controls:** Department / Team filter | Export

**Grid:**

- Rows: Employees
- Columns: Skills (grouped by category)
- Cells: proficiency dots (1–5 filled circles) with colour (green = meets/exceeds required, red = below required, grey = not assessed)
- Required level shown as a threshold line on the cell

**Gap analysis panel (right Sheet):**

- Select a position → shows required skills vs team average
- Radar chart: required vs actual

---

### SCREEN 15 — Organisation Chart

**Layout:** Full-screen canvas with floating controls (zoom, fit, search)

**Node design:**

- Card (160×80px): avatar (40px) | name | title | department
- Connecting lines: straight with right-angle connectors
- Colour by department (subtle left border)

**Interactions:**

- Pan: click + drag
- Zoom: scroll wheel; pinch on mobile
- Click node: side panel opens with employee quick view + "View Profile" link
- Search: filters nodes by name/title
- Expand/collapse subtrees

**Export:** PNG / PDF button in top-right controls

---

### SCREEN 16 — Document Library

**Layout:** Sidebar folder tree (left) + document list (right)

**Folder tree:** Company Policies / Contracts / Certificates / Templates / Custom folders

**Document list:**

- Table: Name | Category | Employee | Uploaded | Expiry | Actions
- Quick preview: click document name → PDF/image preview in overlay
- Upload button: drag-and-drop zone or file picker
- Version history: clock icon → Sheet with version list

---

### SCREEN 17 — Asset Management

**Layout:** List + detail Sheet

**Asset list table:**

- Asset tag | Name | Category | Status badge | Assigned to | Condition | Actions
- Filter: Category / Status / Assigned employee
- "+ Add Asset" button

**Asset detail Sheet:**

- Full asset record
- Assignment history timeline
- Current assignee card with return button
- Photo upload for asset

---

### SCREEN 18 — Company Announcements

**Layout:** Feed (card list) with compose panel

**Feed:**

- Pinned announcements at top (yellow left border)
- Remaining posts in reverse chronological order
- Each card: title | author avatar | posted date | targeting badge (All / Sales Dept) | read receipt count
- Unread posts have bold title + blue left border

**Compose (HR/Manager):**

- Full-page editor: title, rich body, targeting selector, attachment, schedule toggle, pin toggle

---

### SCREEN 19 — Manager Approvals

**Layout:** Tabbed approval inbox.

**Tabs:** All | Leave | Expenses | Overtime | Other

**Each request row:**

- Employee avatar + name | Request type | Date range / amount | Days ago | Approve / Reject inline buttons
- Expand row: shows full detail without opening separate page
- Reject: requires comment input
- Bulk actions: select multiple → approve all

**Empty state:** Illustration + "You're all caught up — no pending approvals."

---

### SCREEN 20 — Helpdesk

**Employee view:**

- My tickets list (number, subject, status, last updated)
- "+ New Ticket" button → form: category, subject, description, priority, attachment
- Ticket detail: conversation thread, status badge, reference number

**Agent view (HR/IT/Facilities):**

- Queue tabs by category
- Each ticket: requester, subject, priority badge, age, assigned to
- Filter: Status / Priority / Assignee
- Ticket detail: full thread, internal notes (private), status change, assign

---

### MOBILE SCREENS

### SCREEN M01 — Mobile Dashboard

**Layout:** Scroll view; bottom nav (5 tabs: Home / Attendance / Leave / Approvals / Profile)

**Home feed:**

- Greeting card: "Good morning, \[Name\] — Monday 10 Nov 2026"
- Clock in / out card: large prominent button with current status
- Attendance summary: today's hours
- 2 pending approvals banner (if manager)
- Latest announcement card
- Leave balance chips

---

### SCREEN M02 — Mobile Attendance

**Primary action:** Dominant circular "Clock In" / "Clock Out" button (full-width pill, 56px height, primary colour)

**Below button:**

- Current status: "Clocked in at 08:34 AM — 3h 12m"
- Method indicator: QR / GPS / QR+GPS badge
- Today's record: in time, out time, total hours

**My Attendance tab:**

- Monthly calendar grid; colour per day
- Tap day: bottom sheet with detail

---

### SCREEN M03 — QR Scanner

**Layout:** Full-screen camera view with overlay

**Overlay:**

- Square scan target (animated corner indicators)
- Label: "Scan your attendance QR code"
- Cancel button (X, top-left)

**After scan:**

- Success: green checkmark animation + "Clocked in at 08:34 AM" + haptic feedback
- Error: red X animation + error message ("QR code expired — please request a new one")
- Offline: amber indicator + "Saved offline — will sync when connected"

---

### SCREEN M04 — GPS Validation

**Layout:** Map view (Google Maps / Mapbox) centred on employee's current location.

**Elements:**

- Employee pin (blue, animated pulse)
- Office geofence circle (green if inside, red if outside)
- Distance label: "42m from office (within 100m — OK)" or "350m from office — outside allowed area"
- "Clock In Here" button (enabled only if inside geofence or remote mode)
- Remote mode toggle: "I'm working remotely today" (exempt from geofence)

---

### SCREEN M05 — Mobile Leave Requests

**Layout:** Full-screen form flow

**Step 1:** Leave type selector (card grid with icons) **Step 2:** Date range picker (calendar; tap start → tap end) **Step 3:** Details (reason text area, attachment for medical leave) **Step 4:** Confirm screen showing: leave type, dates, days count, balance after, manager who will approve; Submit button

**My Leave tab:**

- Balance cards (swipeable horizontal scroll: one card per leave type)
- Request history list

---

### SCREEN M06 — Mobile Expense Claims

**Layout:** Scrollable claim form

**Add items flow:**

1. Category selector (icon grid: Meals / Travel / Accommodation / Equipment / Training / Other)
2. Amount input (large numeric keypad)
3. Receipt capture: camera button (auto-opens camera) or gallery picker
4. Thumbnail preview with tick overlay once captured
5. Date and description fields
6. "Add another item" link

**Claim summary at bottom:**

- Total amount
- "Submit for Approval" button

---

### SCREEN M07 — Mobile Profile

**Layout:** Scroll view

**Header:**

- Full-screen-width gradient banner
- Circular avatar (96px, centred, overlapping banner bottom)
- Name, title, department

**Sections (expandable):**

- Personal details
- My documents (list with download links)
- My training / certificates (compliance status chips)
- My assets (assigned items list)
- Settings (notifications, PIN/biometric, app version)
- Sign Out button (destructive, bottom of list)

## Phase 7B — UX Design Principles & Workflow Guidelines

These principles govern every design decision in Circlate. They were defined after reviewing the target user: an HR manager who lives in Excel, a manager who runs their team on WhatsApp, an employee who has never used business software. Every screen must pass the **WhatsApp test**: if the core action is not as obvious as sending a message, simplify it.

---

### Workflow Design Principles

**Design for the non-technical majority.** The platform must be fully usable by:

- HR personnel comfortable with spreadsheets
- Managers who operate through email and messaging apps
- Employees on mobile with no prior system training

**Seven design mandates — in priority order:**

| # | Mandate | What it means in practice |
| --- | --- | --- |
| 1 | Sensible Defaults | Pre-fill fields wherever possible. Leave type defaults to Annual Leave. Expense category defaults to the most recently used. QR+GPS mode is off by default for SMEs (QR only). |
| 2 | Guided Actions | Never show a blank form. Show the action the user probably wants next. After clock-in, show today's schedule. After leave approval, show who else is off that week. |
| 3 | Wizard-Based Processes | Multi-step tasks (new employee, new job posting, expense claim) are step-by-step flows — never a single complex form. Progress indicator always visible. |
| 4 | Large Actionable Controls | Primary actions use full-width buttons on mobile (minimum 56px height). Icon-only buttons are never used for primary actions. |
| 5 | Simple Language | No system terminology exposed to users. "Attendance Record" → "Today's Check-In". "Leave Balance Accrual" → "Days Available". "Compliance Requirement" → "Required Training". |
| 6 | Clear Status Indicators | Every item has a visible status. Leave requests are Pending / Approved / Rejected — always shown as a coloured badge, never inferred from an absence of data. |
| 7 | Contextual Help | Each screen has a "?" help trigger showing a 2–3 sentence plain-English explanation of what the screen does and what the user should do. Available without leaving the screen. |

---

### Decision-Oriented Design

Circlate surfaces answers — not data. Users should never need to navigate multiple modules to answer a business question.

**Rule:** Every dashboard widget must answer a named business question directly on the surface. If answering the question requires a click, that click must be the last one.

**Examples:**

**"Why is Ali absent today?"** Don't show: Attendance module → filter by employee → check today's record. Show on the Manager Dashboard:

> **Ali Hassan — Absent Today** No clock-in recorded as of 09:15 AM Manager notified at 09:00 AM \[View Attendance History\] \[Contact Ali\]

**"Which work permits expire soon?"** Don't show: HR module → Documents → filter by type → sort by expiry. Show on the HR Dashboard:

> **4 Work Permits Expiring Within 30 Days** \[View Employees\]

**"Can I approve this leave request?"** Don't show: Leave module → pending → open request → check calendar → check team. Show on the Approval screen:

> **Nurul Ain requests Annual Leave — 18–22 Nov (3 working days)** Team coverage: 2 of 5 staff available that week — coverage is adequate Leave balance: 8 days remaining after this request \[Approve\] \[Reject with Comment\]

**Implementation requirement:** Every approval action card must show the decision context (coverage, balance, impact) alongside the approve/reject action. Users must never need to open another screen to make an informed decision.

---

### Low Complexity UX

The following systems operate completely behind the interface. Users must never be asked to understand, configure, or interact with them directly:

- Attendance Engine (clock-in/out processing, overtime detection)
- Presence Engine (GPS/QR validation, geofence logic)
- Rules Engine (shift rules, leave accrual logic)
- Overtime Calculation Logic
- Workflow Configuration
- Geofence Configuration
- Compliance Architecture

These systems are configured by System/Company Admins in a dedicated **Administration** area that is hidden from day-to-day navigation. Operational users (Employee, Manager) never encounter them.

**Terminology mapping — never use system terms in the UI:**

| System term (internal) | User-facing label |
| --- | --- |
| AttendanceRecord | Today's Check-In / Attendance |
| LeaveBalance.accrual | Days Available |
| ComplianceRequirement | Required Training |
| GeofenceRadius | Office Location |
| OvertimeThreshold | Extra Hours |
| TrainingRecord.expiryDate | Certificate Expiry |
| EmploymentRecord.probationEndDate | Confirmation Date |

---

### Minimal Click Requirements

All core user activities are optimised to the following targets. These are hard UX constraints — if a redesign exceeds the click target, the design must be revised.

| Activity | Max Actions | Target Time | Design Pattern |
| --- | --- | --- | --- |
| Employee Clock-In | 2 taps | < 5 seconds | Tap app → Clock In button on home screen. QR scan or GPS auto-validates. Done. |
| Leave Application | 3 actions | < 60 seconds | Type → Date range → Submit. Leave type pre-selected to most common. |
| Expense Submission | 4 actions | < 2 minutes | Category → Photo → Amount → Submit. Receipt auto-fills amount (Phase 2 OCR). |
| Manager Approval | 2 actions | < 15 seconds | Open notification → Approve. Context shown inline. No navigation required. |
| Document Generation | 3 actions | < 60 seconds | Select employee → Select template → Generate. Download link appears immediately. |

**Enforcement mechanism:** Each of these flows is prototyped and click-tested before development begins. Any flow exceeding the target is redesigned, not shipped.

---

### Dashboard-First Design

Information is surfaced before users search for it. Each role's dashboard is pre-configured with the widgets most relevant to their responsibilities.

**Employee Dashboard — answers "What do I need to do or know today?"**

- Today's attendance status (Clocked In / Not Yet / On Leave)
- Leave balance (days available, next expiry if carry-over)
- Pending claims (expenses awaiting approval)
- Upcoming training expiries (next cert expiry with days remaining)
- Required actions (incomplete onboarding, unsigned documents)

**Manager Dashboard — answers "What needs my attention today?"**

- Absent employees (names, reason if known, contact shortcut)
- Pending leave requests (count + inline approve/reject)
- Pending overtime requests
- Coverage risks (days with <50% team presence in next 14 days)
- Training expiries (direct reports with certs expiring in 30 days)
- Work permit / licence expiries (direct reports)

**HR Dashboard — answers "What is the company's operational health today?"**

- Expiring work permits (count, 30/60/90-day buckets, view list)
- Attendance issues (employees with 3+ absences this month, late patterns)
- Pending employee actions (incomplete onboarding, unsigned policies)
- Certification risks (dept compliance rate, non-compliant count by dept)
- Recruitment pipeline (open positions, candidates by stage, stalled applications)
- Upcoming confirmations (employees completing probation in next 30 days)

**Executive Dashboard — answers "How is our workforce performing?"**

- Headcount trend (this month vs last 6 months)
- Turnover rate (rolling 12 months, by department)
- Overtime trends (cost/hours by department; month-on-month)
- Absenteeism rate (% absent per month, against industry benchmark)
- Compliance risk score (% non-compliant employees; red if >10%)
- Workforce capacity (available headcount vs required shifts this week)

---

### Role-Adaptive Interface

The navigation and feature set shown to a user adapts entirely to their role. A user is never shown menu items, buttons, or data that do not apply to their responsibilities.

| Role | Navigation Scope | Hidden from view |
| --- | --- | --- |
| Employee | Home, Attendance, My Leave, My Expenses, My Documents, My Training, Help | All HR, Recruitment, Compliance Admin, Finance screens |
| Manager | Employee dashboard + Team Attendance, Team Leave, Approvals, Team Compliance | HR admin, Recruitment admin, Finance, System config |
| HR | Full HR suite | Executive analytics, System infrastructure |
| Recruiter | Recruitment module only | HR records, Payroll, System config |
| Finance | Expenses approval, Invoices | Recruitment, Performance, Compliance |
| Compliance Admin | Training Compliance module | Recruitment, Performance, Expenses |
| Company Admin | All modules + Settings | Platform-level admin |
| Executive | Executive Dashboard (read-only analytics) | Operational data entry screens |

**Rule:** Role assignment is set once per user. If an employee becomes a manager, their role is updated — not supplemented. No role stacking in the UI (a manager who is also an employee gets the Manager view, not both).

---

### Configuration Without Complexity

Advanced configuration is available but hidden from operational users. The separation is enforced at the navigation level.

**Operational layer (day-to-day screens):** Employees, Attendance, Leave, Expenses, Recruitment, Training, Assets, Announcements, Approvals, Helpdesk.

**Administration layer (Settings → Advanced):** Visible only to Company Admin and System Admin. Contains:

- Workforce rules (shift definitions, overtime thresholds, late arrival grace periods)
- Geofence settings (office locations, allowed radius)
- Leave type configuration (accrual rules, carry-over limits, approval chains)
- Compliance requirements (which courses are required for which departments/positions)
- Notification rules (which events trigger which alerts)
- Approval workflow configuration (single vs two-step, delegation rules)
- Integration settings (SSO, API keys)

**UI principle:** Administration screens use a different visual treatment (lighter header colour, breadcrumb showing "Settings → Advanced → ...") to signal to users that they are outside day-to-day operations.

---

### User Adoption Benchmark

The usability target: **a user comfortable with Microsoft Excel, email, and WhatsApp should perform any common task with no formal training.**

| Task | Adoption design |
| --- | --- |
| Add Employee | Wizard: 5 steps, pre-filled where possible, optional fields collapsed by default |
| Approve Leave | Push notification → one-tap approve; full context in the notification card |
| Generate Employment Letter | Employee profile → Documents tab → "Generate Letter" → select template → download in < 60s |
| Review Attendance | Manager Dashboard widget shows today's absent/present/late count; drill-down with one tap |
| Find Expiring Permits | HR Dashboard widget: "4 Work Permits Expiring" with direct link to employee list |
| Generate Reports | Reports module: pre-built named reports ("Monthly Attendance", "Leave Summary", "Compliance Status") — select, set date range, export |

**Onboarding:** Every new Circlate tenant receives:

1. A guided setup wizard on first login (5–7 steps: add logo, invite employees, configure leave types)
2. Demo data seeded on request ("Load sample data") to let HR explore the platform before going live
3. In-app tooltips on first visit to each module
4. A "Getting Started" checklist widget on the dashboard until all setup steps are complete

## Phase 9 — Database Design

Circlate uses the **database-per-tenant** model (see Phase 3). Two database tiers exist: a **Platform Database** (single, shared) and **Tenant Databases** (one per company). All schemas below are PostgreSQL.

---

### Platform Database

Holds only cross-tenant data: subdomain registry, billing, and global configuration. Never holds employee or operational data.

**platform.tenants**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
company_name     VARCHAR(255) NOT NULL
subdomain        VARCHAR(60)  NOT NULL UNIQUE
status           VARCHAR(30)  NOT NULL  -- Provisioning|Active|Suspended|Deleted
tier             VARCHAR(30)  NOT NULL  -- Free|Business|Professional|Enterprise
region           VARCHAR(10)  NOT NULL  -- BN|MY|SG|ID
created_at       TIMESTAMPTZ  NOT NULL DEFAULT now()
updated_at       TIMESTAMPTZ  NOT NULL DEFAULT now()
deleted_at       TIMESTAMPTZ

INDEX idx_tenants_subdomain (subdomain)
INDEX idx_tenants_status    (status)
```

**platform.subscriptions**

```
id                     UUID PRIMARY KEY
tenant_id              UUID NOT NULL REFERENCES platform.tenants(id)
plan                   VARCHAR(30) NOT NULL
billing_cycle          VARCHAR(10) NOT NULL  -- Monthly|Annual
status                 VARCHAR(30) NOT NULL  -- Trialing|Active|PastDue|Cancelled
trial_ends_at          TIMESTAMPTZ
current_period_start   TIMESTAMPTZ NOT NULL
current_period_end     TIMESTAMPTZ NOT NULL
pocketpay_customer_id  VARCHAR(100)
pocketpay_sub_id       VARCHAR(100)
created_at             TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at             TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_subscriptions_tenant  (tenant_id)
INDEX idx_subscriptions_status  (status)
INDEX idx_subscriptions_period  (current_period_end)
```

**platform.invoices**

```
id             UUID PRIMARY KEY
tenant_id      UUID NOT NULL REFERENCES platform.tenants(id)
subscription_id UUID NOT NULL REFERENCES platform.subscriptions(id)
amount_cents   INTEGER NOT NULL
currency       VARCHAR(3) NOT NULL DEFAULT 'BND'
status         VARCHAR(20) NOT NULL  -- Draft|Issued|Paid|Void
pdf_url        TEXT
issued_at      TIMESTAMPTZ
paid_at        TIMESTAMPTZ
created_at     TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_invoices_tenant  (tenant_id)
INDEX idx_invoices_status  (status, issued_at)
```

**platform.webhook\_events**

```
id               UUID PRIMARY KEY
source           VARCHAR(50)  NOT NULL  -- pocketpay
event_type       VARCHAR(100) NOT NULL
payload          JSONB        NOT NULL
idempotency_key  VARCHAR(255) UNIQUE
processed        BOOLEAN      NOT NULL DEFAULT FALSE
processed_at     TIMESTAMPTZ
error            TEXT
received_at      TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_webhook_events_key        (idempotency_key)
INDEX idx_webhook_events_unprocessed (processed, received_at) WHERE processed = FALSE
```

---

### Tenant Database Schema

Each tenant database (`wos_{subdomain}`) contains all operational tables. `tenant_id` columns are not present — isolation is enforced by connection routing.

---

#### Identity & Users

**users**

```
id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
keycloak_id     VARCHAR(100) NOT NULL UNIQUE
email           VARCHAR(255) NOT NULL UNIQUE
full_name       VARCHAR(255) NOT NULL
status          VARCHAR(20)  NOT NULL DEFAULT 'Active'  -- Active|Inactive|Locked
created_at      TIMESTAMPTZ  NOT NULL DEFAULT now()
updated_at      TIMESTAMPTZ  NOT NULL DEFAULT now()

INDEX idx_users_keycloak (keycloak_id)
INDEX idx_users_email    (email)
```

**user\_roles**

```
id          UUID PRIMARY KEY
user_id     UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE
role        VARCHAR(50) NOT NULL  -- Employee|Manager|HR|Recruiter|Finance|ComplianceAdmin|CompanyAdmin
assigned_at TIMESTAMPTZ NOT NULL DEFAULT now()
assigned_by UUID REFERENCES users(id)

UNIQUE (user_id, role)
INDEX idx_user_roles_user (user_id)
```

---

#### Organisation

**departments**

```
id                   UUID PRIMARY KEY DEFAULT gen_random_uuid()
name                 VARCHAR(255) NOT NULL
code                 VARCHAR(50)  UNIQUE
parent_department_id UUID REFERENCES departments(id)
manager_id           UUID REFERENCES employees(id)
cost_centre          VARCHAR(100)
status               VARCHAR(20) NOT NULL DEFAULT 'Active'
created_at           TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at           TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_departments_parent  (parent_department_id)
INDEX idx_departments_manager (manager_id)
```

**teams**

```
id            UUID PRIMARY KEY DEFAULT gen_random_uuid()
name          VARCHAR(255) NOT NULL
department_id UUID NOT NULL REFERENCES departments(id)
team_lead_id  UUID REFERENCES employees(id)
created_at    TIMESTAMPTZ NOT NULL DEFAULT now()
```

**positions**

```
id                UUID PRIMARY KEY DEFAULT gen_random_uuid()
title             VARCHAR(255) NOT NULL
department_id     UUID NOT NULL REFERENCES departments(id)
grade             VARCHAR(50)
is_manager_role   BOOLEAN NOT NULL DEFAULT FALSE
headcount_budget  INTEGER NOT NULL DEFAULT 0
headcount_filled  INTEGER NOT NULL DEFAULT 0
status            VARCHAR(20) NOT NULL DEFAULT 'Active'
created_at        TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_positions_department (department_id)
```

---

#### Employees

**employees**

```
id                UUID PRIMARY KEY DEFAULT gen_random_uuid()
user_id           UUID UNIQUE REFERENCES users(id)
employee_number   VARCHAR(20) NOT NULL UNIQUE
first_name        VARCHAR(100) NOT NULL
last_name         VARCHAR(100) NOT NULL
preferred_name    VARCHAR(100)
ic_number         BYTEA  -- AES-256 encrypted
passport_number   BYTEA  -- AES-256 encrypted
nationality       VARCHAR(100)
gender            VARCHAR(20)
date_of_birth     DATE
photo_url         TEXT
status            VARCHAR(20) NOT NULL DEFAULT 'Active'
                  -- Active|Probation|OnLeave|Resigned|Terminated
created_at        TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at        TIMESTAMPTZ NOT NULL DEFAULT now()
deleted_at        TIMESTAMPTZ

INDEX idx_employees_number  (employee_number)
INDEX idx_employees_status  (status)
INDEX idx_employees_name    (last_name, first_name)
```

**employee\_employment**

```
id                UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id       UUID NOT NULL REFERENCES employees(id)
position_id       UUID REFERENCES positions(id)
department_id     UUID NOT NULL REFERENCES departments(id)
reporting_manager_id UUID REFERENCES employees(id)
employment_type   VARCHAR(30) NOT NULL  -- FullTime|PartTime|Contract|Intern
hire_date         DATE NOT NULL
probation_end_date DATE
confirmation_date DATE
end_date          DATE
salary_band       VARCHAR(50)
work_email        VARCHAR(255)
status            VARCHAR(20) NOT NULL DEFAULT 'Active'
effective_from    DATE NOT NULL
created_at        TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_emp_employment_employee  (employee_id, effective_from DESC)
INDEX idx_emp_employment_dept      (department_id)
INDEX idx_emp_employment_manager   (reporting_manager_id)
INDEX idx_emp_employment_probation (probation_end_date) WHERE probation_end_date IS NOT NULL
```

**employee\_contacts**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id      UUID NOT NULL REFERENCES employees(id) ON DELETE CASCADE
contact_type     VARCHAR(20) NOT NULL  -- Personal|Emergency
personal_email   VARCHAR(255)
mobile_phone     VARCHAR(30)
work_phone       VARCHAR(30)
home_address     TEXT
is_primary       BOOLEAN NOT NULL DEFAULT FALSE
relationship     VARCHAR(100)  -- for emergency contacts
name             VARCHAR(255)  -- for emergency contacts

INDEX idx_emp_contacts_employee (employee_id)
```

**employee\_bank\_details**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id      UUID NOT NULL REFERENCES employees(id) ON DELETE CASCADE
bank_name        VARCHAR(255) NOT NULL
account_number   BYTEA NOT NULL  -- AES-256 encrypted
account_name     VARCHAR(255)
is_active        BOOLEAN NOT NULL DEFAULT TRUE
created_at       TIMESTAMPTZ NOT NULL DEFAULT now()

UNIQUE (employee_id) WHERE is_active = TRUE
```

---

#### Attendance

**shifts**

```
id           UUID PRIMARY KEY DEFAULT gen_random_uuid()
name         VARCHAR(255) NOT NULL
start_time   TIME NOT NULL
end_time     TIME NOT NULL
days_of_week INTEGER[] NOT NULL  -- 1=Mon...7=Sun
is_flexible  BOOLEAN NOT NULL DEFAULT FALSE
flex_window_minutes INTEGER  -- clock-in window before/after start_time
overtime_threshold_minutes INTEGER NOT NULL DEFAULT 480  -- 8 hours
late_grace_minutes INTEGER NOT NULL DEFAULT 5
is_active    BOOLEAN NOT NULL DEFAULT TRUE
created_at   TIMESTAMPTZ NOT NULL DEFAULT now()
```

**shift\_assignments**

```
id             UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id    UUID NOT NULL REFERENCES employees(id)
shift_id       UUID NOT NULL REFERENCES shifts(id)
effective_from DATE NOT NULL
effective_to   DATE
created_at     TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_shift_assign_employee (employee_id, effective_from DESC)
```

**attendance\_records**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id      UUID NOT NULL REFERENCES employees(id)
work_date        DATE NOT NULL
clock_in_time    TIMESTAMPTZ
clock_out_time   TIMESTAMPTZ
method           VARCHAR(20) NOT NULL  -- QR|GPS|QRandGPS|Manual|System
gps_lat_in       DECIMAL(10,7)
gps_lng_in       DECIMAL(10,7)
gps_lat_out      DECIMAL(10,7)
gps_lng_out      DECIMAL(10,7)
qr_token_used    VARCHAR(100)
regular_minutes  INTEGER
overtime_minutes INTEGER NOT NULL DEFAULT 0
status           VARCHAR(20) NOT NULL
                 -- Present|Late|Absent|Leave|Holiday|Remote
is_offline_sync  BOOLEAN NOT NULL DEFAULT FALSE
notes            TEXT
created_at       TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at       TIMESTAMPTZ NOT NULL DEFAULT now()

UNIQUE (employee_id, work_date)
INDEX idx_attendance_employee_date (employee_id, work_date DESC)
INDEX idx_attendance_date          (work_date)
INDEX idx_attendance_status        (status, work_date)
```

**office\_locations** (for GPS geofencing)

```
id          UUID PRIMARY KEY DEFAULT gen_random_uuid()
name        VARCHAR(255) NOT NULL
lat         DECIMAL(10,7) NOT NULL
lng         DECIMAL(10,7) NOT NULL
radius_m    INTEGER NOT NULL DEFAULT 100
is_active   BOOLEAN NOT NULL DEFAULT TRUE
created_at  TIMESTAMPTZ NOT NULL DEFAULT now()
```

---

#### Leave

**leave\_types**

```
id                    UUID PRIMARY KEY DEFAULT gen_random_uuid()
name                  VARCHAR(100) NOT NULL
code                  VARCHAR(20) UNIQUE
days_per_year         DECIMAL(5,1) NOT NULL
is_paid               BOOLEAN NOT NULL DEFAULT TRUE
carry_over_allowed    BOOLEAN NOT NULL DEFAULT FALSE
max_carry_over_days   DECIMAL(5,1)
requires_document     BOOLEAN NOT NULL DEFAULT FALSE
notice_days_required  INTEGER NOT NULL DEFAULT 0
is_active             BOOLEAN NOT NULL DEFAULT TRUE
created_at            TIMESTAMPTZ NOT NULL DEFAULT now()
```

**leave\_balances**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id      UUID NOT NULL REFERENCES employees(id)
leave_type_id    UUID NOT NULL REFERENCES leave_types(id)
year             INTEGER NOT NULL
entitled_days    DECIMAL(5,1) NOT NULL
taken_days       DECIMAL(5,1) NOT NULL DEFAULT 0
pending_days     DECIMAL(5,1) NOT NULL DEFAULT 0
carried_over_days DECIMAL(5,1) NOT NULL DEFAULT 0
updated_at       TIMESTAMPTZ NOT NULL DEFAULT now()

UNIQUE (employee_id, leave_type_id, year)
INDEX idx_leave_balances_employee (employee_id, year)
```

**leave\_requests**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id      UUID NOT NULL REFERENCES employees(id)
leave_type_id    UUID NOT NULL REFERENCES leave_types(id)
start_date       DATE NOT NULL
end_date         DATE NOT NULL
working_days     DECIMAL(5,1) NOT NULL
reason           TEXT
attachment_url   TEXT
status           VARCHAR(20) NOT NULL DEFAULT 'Pending'
                 -- Pending|Approved|Rejected|Cancelled
approved_by      UUID REFERENCES employees(id)
approved_at      TIMESTAMPTZ
rejection_note   TEXT
created_at       TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at       TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_leave_requests_employee (employee_id, start_date DESC)
INDEX idx_leave_requests_approver (approved_by)
INDEX idx_leave_requests_status   (status, created_at)
INDEX idx_leave_requests_dates    (start_date, end_date)
```

---

#### Recruitment

**job\_postings**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
title            VARCHAR(255) NOT NULL
department_id    UUID REFERENCES departments(id)
position_id      UUID REFERENCES positions(id)
employment_type  VARCHAR(30)
description      TEXT
requirements     TEXT
salary_min       DECIMAL(12,2)
salary_max       DECIMAL(12,2)
status           VARCHAR(20) NOT NULL DEFAULT 'Draft'
                 -- Draft|Open|OnHold|Closed
posted_at        TIMESTAMPTZ
closes_at        TIMESTAMPTZ
created_by       UUID NOT NULL REFERENCES users(id)
created_at       TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_job_postings_status (status, posted_at)
INDEX idx_job_postings_dept   (department_id)
```

**candidates**

```
id          UUID PRIMARY KEY DEFAULT gen_random_uuid()
full_name   VARCHAR(255) NOT NULL
email       VARCHAR(255)
phone       VARCHAR(50)
resume_url  TEXT
source      VARCHAR(50)  -- Direct|Referral|LinkedIn|JobStreet|Agency
notes       TEXT
created_at  TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_candidates_email (email)
```

**applications**

```
id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
candidate_id    UUID NOT NULL REFERENCES candidates(id)
job_posting_id  UUID NOT NULL REFERENCES job_postings(id)
stage           VARCHAR(30) NOT NULL DEFAULT 'Applied'
                -- Applied|Screening|Interview|Assessment|Offer|Hired|Rejected
assigned_to     UUID REFERENCES users(id)
stage_changed_at TIMESTAMPTZ NOT NULL DEFAULT now()
rejection_reason TEXT
created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at      TIMESTAMPTZ NOT NULL DEFAULT now()

UNIQUE (candidate_id, job_posting_id)
INDEX idx_applications_posting (job_posting_id, stage)
INDEX idx_applications_stage   (stage, stage_changed_at)
```

**interviews**

```
id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
application_id  UUID NOT NULL REFERENCES applications(id)
scheduled_at    TIMESTAMPTZ NOT NULL
format          VARCHAR(30) NOT NULL  -- Phone|Video|InPerson|Technical
location        TEXT
interviewer_ids UUID[] NOT NULL
outcome         VARCHAR(20)  -- Proceed|Hold|Reject
notes           TEXT
created_by      UUID NOT NULL REFERENCES users(id)
created_at      TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_interviews_application (application_id)
INDEX idx_interviews_scheduled   (scheduled_at)
```

---

#### Expenses

**expense\_claims**

```
id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id     UUID NOT NULL REFERENCES employees(id)
title           VARCHAR(255) NOT NULL
total_amount    DECIMAL(12,2) NOT NULL DEFAULT 0
currency        VARCHAR(3) NOT NULL DEFAULT 'BND'
status          VARCHAR(30) NOT NULL DEFAULT 'Draft'
                -- Draft|Submitted|ManagerApproved|FinanceApproved|Paid|Rejected
submitted_at    TIMESTAMPTZ
payment_ref     VARCHAR(100)
paid_at         TIMESTAMPTZ
created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at      TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_expense_claims_employee (employee_id, created_at DESC)
INDEX idx_expense_claims_status   (status, submitted_at)
```

**expense\_items**

```
id           UUID PRIMARY KEY DEFAULT gen_random_uuid()
claim_id     UUID NOT NULL REFERENCES expense_claims(id) ON DELETE CASCADE
category     VARCHAR(50) NOT NULL
description  TEXT
amount       DECIMAL(12,2) NOT NULL
expense_date DATE NOT NULL
merchant     VARCHAR(255)
receipt_url  TEXT
created_at   TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_expense_items_claim (claim_id)
```

**expense\_approvals**

```
id           UUID PRIMARY KEY DEFAULT gen_random_uuid()
claim_id     UUID NOT NULL REFERENCES expense_claims(id)
step         INTEGER NOT NULL  -- 1=Manager, 2=Finance
approver_id  UUID NOT NULL REFERENCES users(id)
action       VARCHAR(20) NOT NULL  -- Approved|Rejected
comment      TEXT
actioned_at  TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_expense_approvals_claim (claim_id)
```

---

#### Training Compliance

**training\_providers**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
name             VARCHAR(255) NOT NULL
accreditation    VARCHAR(255)
contact_email    VARCHAR(255)
contact_phone    VARCHAR(50)
website          TEXT
is_active        BOOLEAN NOT NULL DEFAULT TRUE
created_at       TIMESTAMPTZ NOT NULL DEFAULT now()
```

**courses**

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
name             VARCHAR(255) NOT NULL
provider_id      UUID REFERENCES training_providers(id)
description      TEXT
category         VARCHAR(50) NOT NULL  -- Safety|Compliance|Licence|Technical
validity_months  INTEGER NOT NULL
is_mandatory_globally BOOLEAN NOT NULL DEFAULT FALSE
is_active        BOOLEAN NOT NULL DEFAULT TRUE
created_at       TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_courses_provider (provider_id)
INDEX idx_courses_category (category)
```

**compliance\_requirements**

```
id                UUID PRIMARY KEY DEFAULT gen_random_uuid()
course_id         UUID NOT NULL REFERENCES courses(id)
scope_type        VARCHAR(20) NOT NULL  -- All|Department|Position
scope_ids         UUID[]  -- department_ids or position_ids; NULL if All
required_within_days INTEGER  -- days after hire to complete
is_active         BOOLEAN NOT NULL DEFAULT TRUE
created_at        TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_comp_req_course (course_id)
```

**training\_records**

```
id                UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id       UUID NOT NULL REFERENCES employees(id)
course_id         UUID NOT NULL REFERENCES courses(id)
provider_id       UUID REFERENCES training_providers(id)
completion_date   DATE NOT NULL
expiry_date       DATE
certificate_url   TEXT
status            VARCHAR(20) NOT NULL DEFAULT 'PendingVerification'
                  -- PendingVerification|Active|Expired|Revoked
uploaded_by       UUID NOT NULL REFERENCES users(id)
verified_by       UUID REFERENCES users(id)
verified_at       TIMESTAMPTZ
notes             TEXT
created_at        TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at        TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_training_records_employee (employee_id)
INDEX idx_training_records_course   (course_id)
INDEX idx_training_records_expiry   (expiry_date, status) WHERE status = 'Active'
```

**compliance\_alerts**

```
id                 UUID PRIMARY KEY DEFAULT gen_random_uuid()
employee_id        UUID NOT NULL REFERENCES employees(id)
course_id          UUID NOT NULL REFERENCES courses(id)
training_record_id UUID REFERENCES training_records(id)
alert_type         VARCHAR(20) NOT NULL  -- Day90|Day60|Day30|Expired
scheduled_at       DATE NOT NULL
sent_at            TIMESTAMPTZ
channels           VARCHAR(20)[] NOT NULL  -- Push|Email|InApp

UNIQUE (employee_id, course_id, alert_type, scheduled_at)
INDEX idx_comp_alerts_unsent (sent_at, scheduled_at) WHERE sent_at IS NULL
```

---

#### Assets

**assets**

```
id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
asset_tag       VARCHAR(100) NOT NULL UNIQUE
name            VARCHAR(255) NOT NULL
category        VARCHAR(50) NOT NULL  -- Phone|Laptop|Vehicle|AccessCard|Tool|Other
brand           VARCHAR(100)
model           VARCHAR(100)
serial_number   VARCHAR(100) UNIQUE
purchase_date   DATE
purchase_value  DECIMAL(12,2)
warranty_expiry DATE
condition       VARCHAR(20) NOT NULL DEFAULT 'Good'  -- New|Good|Fair|Damaged
status          VARCHAR(20) NOT NULL DEFAULT 'Available'
                -- Available|Assigned|UnderRepair|Retired
notes           TEXT
created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at      TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_assets_status   (status)
INDEX idx_assets_category (category)
```

**asset\_assignments**

```
id                UUID PRIMARY KEY DEFAULT gen_random_uuid()
asset_id          UUID NOT NULL REFERENCES assets(id)
employee_id       UUID NOT NULL REFERENCES employees(id)
assigned_date     DATE NOT NULL
expected_return   DATE
actual_return     DATE
condition_out     VARCHAR(20) NOT NULL
condition_in      VARCHAR(20)
acknowledgement   TEXT
assigned_by       UUID NOT NULL REFERENCES users(id)
returned_to       UUID REFERENCES users(id)
created_at        TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_asset_assign_asset    (asset_id, actual_return)
INDEX idx_asset_assign_employee (employee_id, actual_return)
```

---

#### Documents

**documents**

```
id                   UUID PRIMARY KEY DEFAULT gen_random_uuid()
name                 VARCHAR(255) NOT NULL
category             VARCHAR(50) NOT NULL
employee_id          UUID REFERENCES employees(id)  -- NULL = company-wide
uploaded_by          UUID NOT NULL REFERENCES users(id)
current_version      INTEGER NOT NULL DEFAULT 1
is_employee_visible  BOOLEAN NOT NULL DEFAULT FALSE
expiry_date          DATE
tags                 TEXT[]
created_at           TIMESTAMPTZ NOT NULL DEFAULT now()
updated_at           TIMESTAMPTZ NOT NULL DEFAULT now()
deleted_at           TIMESTAMPTZ

INDEX idx_documents_employee (employee_id)
INDEX idx_documents_expiry   (expiry_date) WHERE expiry_date IS NOT NULL AND deleted_at IS NULL
```

**document\_versions**

```
id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
document_id     UUID NOT NULL REFERENCES documents(id) ON DELETE CASCADE
version_number  INTEGER NOT NULL
file_key        TEXT NOT NULL  -- MinIO object key
file_name       TEXT NOT NULL
content_type    VARCHAR(100) NOT NULL
size_bytes      BIGINT NOT NULL
uploaded_by     UUID NOT NULL REFERENCES users(id)
uploaded_at     TIMESTAMPTZ NOT NULL DEFAULT now()

UNIQUE (document_id, version_number)
INDEX idx_doc_versions_document (document_id, version_number DESC)
```

---

#### Audit Log

**audit\_log** (append-only; application role has INSERT only)

```
id               UUID PRIMARY KEY DEFAULT gen_random_uuid()
actor_user_id    UUID NOT NULL REFERENCES users(id)
actor_role       VARCHAR(50) NOT NULL
action           VARCHAR(30) NOT NULL
                 -- CREATE|UPDATE|DELETE|APPROVE|REJECT|LOGIN|LOGOUT|EXPORT|VIEW
resource_type    VARCHAR(100) NOT NULL
resource_id      UUID
before_snapshot  JSONB
after_snapshot   JSONB
ip_address       INET
user_agent       TEXT
occurred_at      TIMESTAMPTZ NOT NULL DEFAULT now()

INDEX idx_audit_log_actor        (actor_user_id, occurred_at DESC)
INDEX idx_audit_log_resource     (resource_type, resource_id, occurred_at DESC)
INDEX idx_audit_log_occurred_at  (occurred_at DESC)
-- Partitioned by month for large tenants (Phase 2)
```

---

### Key Database Conventions

| Convention | Rule |
| --- | --- |
| Primary keys | UUID v4 (`gen_random_uuid()`); never sequential integers |
| Timestamps | All stored as `TIMESTAMPTZ` (UTC); displayed in tenant timezone at app layer |
| Soft deletes | `deleted_at TIMESTAMPTZ` column; queries filter `WHERE deleted_at IS NULL` |
| Encrypted columns | Sensitive PII stored as `BYTEA` (AES-256-GCM); encryption key per tenant in secrets manager |
| Enums | Stored as `VARCHAR` with CHECK constraints, not PostgreSQL ENUM type (easier to extend) |
| JSON | `JSONB` for schema-flexible payloads (audit snapshots, webhook payloads, custom fields) |
| Array columns | `UUID[]` and `VARCHAR[]` used sparingly; prefer junction tables for large sets |
| Indexes | Partial indexes used extensively for status-filtered queries; covering indexes for hot read paths |
| Naming | snake\_case; tables plural; foreign keys `{table_singular}_id` |
| Migrations | Managed by EF Core Migrations; each migration has `Up()` and `Down()`; run on startup in Docker Compose |

## Phase 10 — API Design

All APIs are RESTful, versioned at `/api/v1/`, and secured with Keycloak-issued JWTs. Every response follows a consistent envelope. The base URL for SaaS is `https://{subdomain}.circlate.app/api/v1`.

**Standard response envelope:**

```json
{
  "success": true,
  "data": { ... },
  "meta": { "page": 1, "pageSize": 20, "total": 142 },
  "errors": null
}
```

**Error envelope:**

```json
{
  "success": false,
  "data": null,
  "errors": [
    { "code": "VALIDATION_ERROR", "field": "email", "message": "Invalid email format" }
  ]
}
```

---

### Authentication APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| POST | `/auth/login` | Initiate login; redirects to Keycloak | Public |
| POST | `/auth/callback` | Keycloak OIDC callback; issues session | Public |
| POST | `/auth/refresh` | Refresh access token | Refresh token |
| POST | `/auth/logout` | Revoke tokens; end session | Bearer |
| POST | `/auth/mfa/enrol` | Enrol TOTP device | Bearer |
| POST | `/auth/mfa/verify` | Verify TOTP code | Partial auth |
| POST | `/auth/password/reset-request` | Send password reset email | Public |
| POST | `/auth/password/reset` | Complete password reset | Reset token |

---

### Tenant APIs (Platform-level, System Admin only)

| Method | Endpoint | Description |
| --- | --- | --- |
| GET | `/platform/tenants` | List all tenants (paginated) |
| POST | `/platform/tenants` | Provision new tenant |
| GET | `/platform/tenants/{id}` | Get tenant detail |
| PATCH | `/platform/tenants/{id}` | Update tenant config |
| POST | `/platform/tenants/{id}/suspend` | Suspend tenant |
| POST | `/platform/tenants/{id}/restore` | Restore suspended tenant |
| DELETE | `/platform/tenants/{id}` | Mark tenant for deletion (soft) |

---

### Billing APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/billing/subscription` | Get current tenant subscription | CompanyAdmin |
| POST | `/billing/subscription/upgrade` | Upgrade to higher tier | CompanyAdmin |
| POST | `/billing/subscription/downgrade` | Downgrade tier | CompanyAdmin |
| POST | `/billing/subscription/cancel` | Cancel subscription | CompanyAdmin |
| GET | `/billing/invoices` | List invoices (paginated) | CompanyAdmin/Finance |
| GET | `/billing/invoices/{id}` | Get invoice detail + PDF URL | CompanyAdmin/Finance |
| POST | `/billing/webhooks/pocketpay` | Receive PocketPay webhook events | HMAC-verified |

---

### Employee APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/employees` | List employees (paginated, filterable) | HR/Manager |
| POST | `/employees` | Create employee | HR |
| GET | `/employees/{id}` | Get employee profile | HR/Manager(direct report)/Employee(self) |
| PATCH | `/employees/{id}` | Update employee record | HR |
| DELETE | `/employees/{id}` | Soft-delete (terminate) employee | HR |
| GET | `/employees/{id}/employment` | Employment history | HR |
| POST | `/employees/{id}/employment` | Add employment record | HR |
| GET | `/employees/{id}/documents` | List employee documents | HR/Employee(visible only) |
| POST | `/employees/{id}/documents` | Upload document | HR |
| GET | `/employees/me` | Current user's employee profile | Employee |
| PATCH | `/employees/me` | Update own profile (limited fields) | Employee |
| GET | `/employees/me/onboarding` | Get onboarding checklist | Employee |
| POST | `/employees/me/onboarding/{taskId}/complete` | Mark onboarding task done | Employee |
| GET | `/employees/search` | Full-text search employees | HR/Manager |

---

### Organisation APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/organisation/departments` | List departments (tree) | All |
| POST | `/organisation/departments` | Create department | HR/CompanyAdmin |
| PATCH | `/organisation/departments/{id}` | Update department | HR/CompanyAdmin |
| DELETE | `/organisation/departments/{id}` | Delete department | HR/CompanyAdmin |
| GET | `/organisation/positions` | List positions | All |
| POST | `/organisation/positions` | Create position | HR/CompanyAdmin |
| PATCH | `/organisation/positions/{id}` | Update position | HR/CompanyAdmin |
| GET | `/organisation/chart` | Org chart tree (full) | All |
| GET | `/organisation/headcount` | Headcount by department | HR/Manager |
| GET | `/organisation/teams` | List teams | All |
| POST | `/organisation/teams` | Create team | HR/CompanyAdmin |

---

### Recruitment APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/recruitment/jobs` | List job postings | HR/Recruiter |
| POST | `/recruitment/jobs` | Create job posting | HR/Recruiter |
| GET | `/recruitment/jobs/{id}` | Get job posting detail | HR/Recruiter |
| PATCH | `/recruitment/jobs/{id}` | Update job posting | HR/Recruiter |
| POST | `/recruitment/jobs/{id}/close` | Close job posting | HR/Recruiter |
| GET | `/recruitment/jobs/{id}/applications` | List applications for a job | HR/Recruiter |
| GET | `/recruitment/candidates` | List all candidates | HR/Recruiter |
| POST | `/recruitment/candidates` | Create candidate | HR/Recruiter |
| GET | `/recruitment/candidates/{id}` | Get candidate profile | HR/Recruiter |
| POST | `/recruitment/applications` | Submit application | HR/Recruiter |
| PATCH | `/recruitment/applications/{id}/stage` | Move application to stage | HR/Recruiter |
| POST | `/recruitment/applications/{id}/interviews` | Schedule interview | HR/Recruiter |
| PATCH | `/recruitment/interviews/{id}` | Update interview outcome | HR/Recruiter |
| POST | `/recruitment/applications/{id}/offer` | Create offer | HR |
| POST | `/recruitment/offers/{id}/accept` | Accept offer → triggers employee creation | HR |
| GET | `/recruitment/pipeline/stats` | Pipeline conversion rates, time-to-hire | HR/Recruiter |

---

### Attendance APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| POST | `/attendance/clock-in` | Record clock-in event | Employee |
| POST | `/attendance/clock-out` | Record clock-out event | Employee |
| POST | `/attendance/sync` | Bulk offline sync upload | Employee |
| GET | `/attendance/me` | My attendance records (date range) | Employee |
| GET | `/attendance/me/today` | My attendance for today | Employee |
| GET | `/attendance/team` | Team attendance (manager) | Manager |
| GET | `/attendance/team/today` | Team attendance today (live) | Manager |
| GET | `/attendance` | All attendance records | HR |
| PATCH | `/attendance/{id}` | Manual correction | HR |
| GET | `/attendance/qr-token` | Generate/get current QR token | Employee |
| GET | `/attendance/shifts` | List shifts | HR/Manager |
| POST | `/attendance/shifts` | Create shift | HR |
| PATCH | `/attendance/shifts/{id}` | Update shift | HR |
| POST | `/attendance/shift-assignments` | Assign employee to shift | HR |
| POST | `/attendance/overtime/{id}/approve` | Approve overtime request | Manager |

---

### Leave APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/leave/types` | List leave types | All |
| POST | `/leave/types` | Create leave type | HR |
| PATCH | `/leave/types/{id}` | Update leave type | HR |
| GET | `/leave/balances/me` | My leave balances | Employee |
| GET | `/leave/balances/{employeeId}` | Employee leave balances | HR/Manager |
| POST | `/leave/requests` | Submit leave request | Employee |
| GET | `/leave/requests/me` | My leave requests | Employee |
| GET | `/leave/requests/pending` | Pending approvals (manager inbox) | Manager |
| GET | `/leave/requests` | All leave requests | HR |
| GET | `/leave/requests/{id}` | Get request detail | HR/Manager/Employee(own) |
| POST | `/leave/requests/{id}/approve` | Approve leave | Manager/HR |
| POST | `/leave/requests/{id}/reject` | Reject leave with comment | Manager/HR |
| DELETE | `/leave/requests/{id}` | Cancel leave request | Employee(own, if Pending) |
| GET | `/leave/calendar` | Team leave calendar | Manager/HR |
| POST | `/leave/balances/{employeeId}/adjust` | Manual balance adjustment | HR |

---

### Expense APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/expenses/claims/me` | My expense claims | Employee |
| POST | `/expenses/claims` | Create claim | Employee |
| GET | `/expenses/claims/{id}` | Get claim detail | Employee(own)/Manager/Finance |
| PATCH | `/expenses/claims/{id}` | Update draft claim | Employee(own, if Draft) |
| POST | `/expenses/claims/{id}/submit` | Submit claim for approval | Employee |
| DELETE | `/expenses/claims/{id}` | Delete draft claim | Employee(own, if Draft) |
| POST | `/expenses/claims/{id}/items` | Add expense item | Employee |
| DELETE | `/expenses/claims/{id}/items/{itemId}` | Remove expense item | Employee |
| POST | `/expenses/receipts/upload` | Upload receipt image | Employee |
| GET | `/expenses/claims/pending` | Pending approvals | Manager/Finance |
| POST | `/expenses/claims/{id}/approve` | Manager/Finance approve | Manager/Finance |
| POST | `/expenses/claims/{id}/reject` | Reject with comment | Manager/Finance |
| POST | `/expenses/claims/{id}/mark-paid` | Mark as paid | Finance |
| GET | `/expenses/export` | Export approved claims CSV | Finance |

---

### Training Compliance APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/compliance/providers` | List training providers | HR/ComplianceAdmin |
| POST | `/compliance/providers` | Create provider | ComplianceAdmin |
| GET | `/compliance/courses` | List courses | All |
| POST | `/compliance/courses` | Create course | ComplianceAdmin |
| PATCH | `/compliance/courses/{id}` | Update course | ComplianceAdmin |
| GET | `/compliance/requirements` | List compliance requirements | HR/ComplianceAdmin |
| POST | `/compliance/requirements` | Create requirement | ComplianceAdmin |
| PATCH | `/compliance/requirements/{id}` | Update requirement | ComplianceAdmin |
| GET | `/compliance/matrix` | Full compliance matrix | HR/ComplianceAdmin |
| GET | `/compliance/matrix/department/{deptId}` | Dept compliance summary | HR/Manager |
| GET | `/compliance/records/me` | My training records | Employee |
| GET | `/compliance/records/{employeeId}` | Employee training records | HR/ComplianceAdmin/Manager |
| POST | `/compliance/records` | Add training record (HR) | HR/ComplianceAdmin |
| POST | `/compliance/records/upload` | Employee certificate upload | Employee |
| POST | `/compliance/records/{id}/verify` | Verify uploaded certificate | ComplianceAdmin/HR |
| POST | `/compliance/records/{id}/reject` | Reject certificate upload | ComplianceAdmin/HR |
| GET | `/compliance/alerts/upcoming` | Upcoming expiry alerts | HR/ComplianceAdmin |
| GET | `/compliance/reports/non-compliant` | Non-compliance report | HR/ComplianceAdmin |

---

### Performance APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/performance/cycles` | List review cycles | HR |
| POST | `/performance/cycles` | Create review cycle | HR |
| PATCH | `/performance/cycles/{id}/advance` | Advance cycle to next stage | HR |
| GET | `/performance/goals/me` | My goals | Employee |
| POST | `/performance/goals` | Create goal | Employee/Manager |
| PATCH | `/performance/goals/{id}` | Update goal progress | Employee |
| GET | `/performance/reviews/me` | My reviews | Employee |
| POST | `/performance/reviews/{id}/self-assess` | Submit self-assessment | Employee |
| POST | `/performance/reviews/{id}/manager-assess` | Submit manager assessment | Manager |

---

### Skills APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/skills` | List all skills (taxonomy) | All |
| POST | `/skills` | Create skill | HR |
| GET | `/skills/matrix` | Skills matrix (all employees) | HR |
| GET | `/skills/matrix/department/{deptId}` | Dept skills matrix | HR/Manager |
| GET | `/skills/employees/{employeeId}` | Employee skill profile | HR/Manager/Employee(own) |
| POST | `/skills/employees/{employeeId}` | Rate employee skill | HR/Manager |
| GET | `/skills/succession` | Succession plans | HR |
| POST | `/skills/succession` | Create succession plan | HR |

---

### Assets APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/assets` | List all assets | HR/CompanyAdmin |
| POST | `/assets` | Create asset | HR/CompanyAdmin |
| GET | `/assets/{id}` | Asset detail + assignment history | HR/CompanyAdmin |
| PATCH | `/assets/{id}` | Update asset | HR/CompanyAdmin |
| POST | `/assets/{id}/assign` | Assign to employee | HR |
| POST | `/assets/{id}/return` | Record return | HR |
| GET | `/assets/employee/{employeeId}` | Employee assigned assets | HR/Employee(own) |

---

### Announcements APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/announcements` | List announcements (targeted to me) | Employee |
| GET | `/announcements/all` | All announcements | HR/CompanyAdmin |
| POST | `/announcements` | Create announcement | HR/Manager |
| PATCH | `/announcements/{id}` | Update announcement | HR |
| DELETE | `/announcements/{id}` | Delete announcement | HR |
| POST | `/announcements/{id}/publish` | Publish immediately | HR |
| POST | `/announcements/{id}/read` | Mark as read | Employee |
| GET | `/announcements/{id}/receipts` | Read receipt list | HR |

---

### Helpdesk APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| POST | `/helpdesk/tickets` | Submit ticket | Employee |
| GET | `/helpdesk/tickets/me` | My tickets | Employee |
| GET | `/helpdesk/tickets` | All tickets (agent view) | HR/CompanyAdmin |
| GET | `/helpdesk/tickets/{id}` | Ticket detail + comments | Employee(own)/HR |
| PATCH | `/helpdesk/tickets/{id}/status` | Update ticket status | HR |
| POST | `/helpdesk/tickets/{id}/assign` | Assign ticket | HR |
| POST | `/helpdesk/tickets/{id}/comments` | Add comment | Employee(own)/HR |

---

### Notification APIs

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/notifications` | In-app notification feed | Employee |
| POST | `/notifications/{id}/read` | Mark notification as read | Employee |
| POST | `/notifications/read-all` | Mark all as read | Employee |
| POST | `/notifications/push/register` | Register FCM/APNs device token | Employee |
| DELETE | `/notifications/push/deregister` | Remove device token on logout | Employee |

---

### Reporting APIs (Metabase proxy)

| Method | Endpoint | Description | Auth |
| --- | --- | --- | --- |
| GET | `/reports` | List available report dashboards | HR/Manager/Finance |
| GET | `/reports/{slug}/embed-url` | Get signed Metabase embed URL | Role-scoped |
| POST | `/reports/export` | Export named report to CSV/PDF | HR/Finance |

---

### Webhook Endpoints

| Method | Endpoint | Caller | Verification |
| --- | --- | --- | --- |
| POST | `/webhooks/pocketpay` | PocketPay | HMAC-SHA256 header signature |

**PocketPay events handled:**

- `subscription.created` → activate tenant
- `subscription.renewed` → extend period
- `subscription.payment_failed` → trigger grace period
- `subscription.cancelled` → schedule suspension
- `invoice.paid` → mark invoice paid
- `invoice.created` → store invoice record

---

### API Conventions

| Convention | Detail |
| --- | --- |
| Versioning | URI versioning: `/api/v1/`; breaking changes get `/api/v2/` |
| Pagination | `?page=1&pageSize=20`; response includes `meta.total`, `meta.page`, `meta.pageSize` |
| Filtering | Query params: `?status=Active&departmentId=uuid&search=keyword` |
| Sorting | `?sortBy=createdAt&sortDir=desc` |
| Date format | ISO 8601: `2026-11-10T08:34:00Z` |
| File uploads | Multipart form-data to dedicated upload endpoints; returns MinIO-signed URL |
| Idempotency | POST endpoints accept `Idempotency-Key` header; safe to retry |
| Rate limiting | 100 req/min authenticated; 429 response with `Retry-After` header |
| CORS | Restricted to `*.circlate.app` + configured custom domains |
| Health | `GET /health` returns `{"status":"ok","version":"1.4.2"}` — no auth required |

## Phase 11 — Infrastructure

### Development Environment

Every developer runs the full stack locally using Docker Compose. No external services required beyond Docker Desktop.

**Prerequisites:** Docker Desktop 4.x, Make (optional), 8 GB RAM minimum.

**Local service ports:**

| Service | Port | Notes |
| --- | --- | --- |
| Next.js frontend | 3000 | Hot reload via `npm run dev` |
| ASP.NET Core API | 5000 | HTTPS via dev cert |
| PostgreSQL (platform) | 5432 |  |
| PostgreSQL (dev tenant) | 5433 | Pre-seeded with demo data |
| Keycloak | 8080 | Admin console: :8080/admin |
| MinIO | 9000 / 9001 | S3 API / Console |
| Metabase | 3001 |  |
| Redis | 6379 | Cache + job queue |
| MailHog | 8025 | Catches outbound email in dev |

---

### Docker Compose — Development

**`docker-compose.yml` service overview:**

```yaml
services:

  postgres-platform:
    image: postgres:16
    environment:
      POSTGRES_DB: circlate_platform
      POSTGRES_USER: circlate
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - postgres_platform_data:/var/lib/postgresql/data
    ports: ["5432:5432"]

  postgres-tenant:
    image: postgres:16
    environment:
      POSTGRES_DB: wos_devtenant
      POSTGRES_USER: circlate
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - postgres_tenant_data:/var/lib/postgresql/data
    ports: ["5433:5432"]

  keycloak:
    image: quay.io/keycloak/keycloak:24.0
    command: start-dev --import-realm
    environment:
      KC_DB: postgres
      KC_DB_URL: jdbc:postgresql://postgres-platform:5432/circlate_platform
      KC_DB_USERNAME: circlate
      KC_DB_PASSWORD: ${POSTGRES_PASSWORD}
      KEYCLOAK_ADMIN: admin
      KEYCLOAK_ADMIN_PASSWORD: ${KEYCLOAK_ADMIN_PASSWORD}
    volumes:
      - ./infra/keycloak/realm-export.json:/opt/keycloak/data/import/realm.json
    ports: ["8080:8080"]
    depends_on: [postgres-platform]

  minio:
    image: minio/minio:latest
    command: server /data --console-address ":9001"
    environment:
      MINIO_ROOT_USER: ${MINIO_ACCESS_KEY}
      MINIO_ROOT_PASSWORD: ${MINIO_SECRET_KEY}
    volumes:
      - minio_data:/data
    ports: ["9000:9000", "9001:9001"]

  redis:
    image: redis:7-alpine
    ports: ["6379:6379"]

  metabase:
    image: metabase/metabase:v0.50
    environment:
      MB_DB_TYPE: postgres
      MB_DB_DBNAME: metabase
      MB_DB_HOST: postgres-platform
      MB_DB_USER: circlate
      MB_DB_PASS: ${POSTGRES_PASSWORD}
    ports: ["3001:3000"]
    depends_on: [postgres-platform]

  mailhog:
    image: mailhog/mailhog:latest
    ports: ["1025:1025", "8025:8025"]

  api:
    build: ./src/backend
    environment:
      ASPNETCORE_ENVIRONMENT: Development
      ConnectionStrings__Platform: "Host=postgres-platform;..."
      Keycloak__Authority: "http://keycloak:8080/realms/circlate-platform"
      MinIO__Endpoint: "minio:9000"
      Redis__ConnectionString: "redis:6379"
    ports: ["5000:5000"]
    depends_on: [postgres-platform, postgres-tenant, keycloak, minio, redis]

  frontend:
    build: ./src/frontend
    environment:
      NEXT_PUBLIC_API_URL: "http://localhost:5000/api/v1"
    ports: ["3000:3000"]
    depends_on: [api]
```

---

### Docker Compose — Self-Hosted (Mode C)

The self-hosted package is a standalone `docker-compose.yml` distributed to customers. It includes:

- All services above (minus MailHog; uses customer SMTP)
- Traefik reverse proxy with automatic HTTPS via Let's Encrypt
- Automated DB migration on startup
- Health checks on all services
- Volume mounts for persistent data
- `.env.example` template with all required configuration

**Customer startup:**

```bash
curl -L https://get.circlate.app/self-hosted | bash
# or
git clone https://github.com/circlate/self-hosted
cd self-hosted
cp .env.example .env
# Edit .env with DOMAIN, SMTP settings, secrets
docker compose up -d
```

**Estimated first-run time:** < 5 minutes on a modern VPS (2 vCPU, 4 GB RAM minimum).

---

### Cloud Deployment — Oracle Cloud Infrastructure (OCI)

**Recommended primary cloud for Brunei/ASEAN deployments** — OCI has an APAC region (Singapore, Tokyo, Sydney) and competitive free-tier compute for early-stage operation.

**Architecture:**

| Component | OCI Service |
| --- | --- |
| Compute | OCI Compute (VM.Standard.E4.Flex) or OKE (Kubernetes) |
| Load Balancer | OCI Load Balancer (Layer 7, SSL termination) |
| Database | OCI Database Service for PostgreSQL (managed) or self-managed on Compute |
| Object Storage | OCI Object Storage (S3-compatible; MinIO SDK compatible) |
| DNS | OCI DNS + Cloudflare for CDN/DDoS protection |
| Secrets | OCI Vault |
| Container Registry | OCI Container Registry (OCIR) |
| Monitoring | OCI Monitoring + OCI Logging |

**Network design:**

- VCN (10.0.0.0/16) with public subnet (load balancer) and private subnet (app + database)
- Security List: allow 443 inbound from 0.0.0.0/0 to load balancer only; all other traffic internal
- NAT Gateway for outbound internet from private subnet

**Scaling strategy:**

- Horizontal scaling: add API server instances behind the load balancer (stateless; sessions in Redis)
- Database scaling: read replicas for reporting queries; PgBouncer connection pooler in front of write primary
- Tenant DB distribution: multiple PostgreSQL instances; tenant registry tracks which host each DB lives on

---

### Cloud Deployment — Google Cloud Platform (GCP)

**Alternative/secondary cloud option:**

| Component | GCP Service |
| --- | --- |
| Compute | Cloud Run (serverless containers) or GKE Autopilot |
| Database | Cloud SQL for PostgreSQL |
| Object Storage | Google Cloud Storage (MinIO SDK compatible via S3 adapter) |
| Load Balancer | Global HTTP(S) Load Balancer |
| DNS | Cloud DNS |
| Secrets | Secret Manager |
| Container Registry | Artifact Registry |
| Monitoring | Cloud Monitoring + Cloud Logging + Error Reporting |

**Cloud Run advantage:** Zero-to-scale billing (pay per request); ideal for early SaaS where tenant count is low and traffic is bursty.

---

### Kubernetes (Optional — Mode C Enterprise)

For Enterprise self-hosted deployments that require Kubernetes:

**Helm chart** provided at `charts/circlate/`:

- Deployments: `api`, `frontend`, `keycloak`, `minio`, `redis`, `metabase`
- Services and Ingress (nginx-ingress or Traefik)
- PersistentVolumeClaims for PostgreSQL and MinIO
- Secrets managed via Kubernetes Secrets or external-secrets-operator (Vault integration)
- HorizontalPodAutoscaler on `api` deployment (CPU 70% threshold)
- Namespace: `circlate`

---

### Monitoring

| Layer | Tool | Key Metrics |
| --- | --- | --- |
| Application | Serilog → OpenTelemetry → Grafana | API p95/p99 latency, error rate, request rate |
| Infrastructure | Prometheus + Grafana | CPU, memory, disk I/O, network |
| Database | pg\_stat\_statements + pgBadger | Slow queries, lock contention, connection count |
| Uptime | Uptime Robot (external) | HTTP 200 check every 60s per tenant subdomain |
| Error tracking | Sentry (ASP.NET Core + Next.js) | Unhandled exceptions with stack traces |
| Mobile crash | Firebase Crashlytics | Flutter crash reports by OS/version |

**Alerting thresholds (PagerDuty / OpsGenie):**

- API error rate > 1% over 5 minutes → P2 alert
- Database CPU > 80% for 10 minutes → P2 alert
- Any tenant health check failing > 2 minutes → P1 alert
- Disk usage > 85% → P2 alert

---

### Logging

**Log levels:** Trace / Debug / Info / Warning / Error / Fatal

**Structured logging:** All logs emitted as JSON via Serilog. Fields: `timestamp`, `level`, `service`, `tenant_id`, `user_id`, `request_id`, `message`, `exception`.

**Log pipeline:**

- Application → stdout → Docker logging driver → Loki (Grafana Cloud or self-hosted)
- Logs searchable via Grafana Explore
- Retention: 30 days hot; 1 year cold (object storage)

**Log scrubbing:** PII fields (email, name, IC number) are masked in log output at the logger middleware level before emission.

---

### Backups (Cloud)

| Data | Frequency | Retention | Storage |
| --- | --- | --- | --- |
| Tenant PostgreSQL | Continuous WAL + daily pg\_dump | 30 days | OCI Object Storage / GCS |
| Platform PostgreSQL | Continuous WAL + daily | 90 days | OCI Object Storage / GCS |
| MinIO (documents) | Daily mirror (mc mirror) | 90 days | Secondary bucket, different region |
| Keycloak realms | Daily export | 30 days | Object storage |

**Automated restore test:** Monthly cron restores a randomly selected tenant DB to a staging environment and verifies row counts; result logged and emailed to DevOps.

---

### Disaster Recovery

| Scenario | RTO | RPO | Action |
| --- | --- | --- | --- |
| Single API pod crash | < 30 s | 0 | Kubernetes restarts pod automatically |
| Primary DB failure | < 2 h | 15 min | Promote read replica; update connection string |
| Full region failure | < 4 h | 1 h | Restore from backup to secondary region; update DNS |
| Data corruption (tenant) | < 1 h | 15 min | PITR restore from WAL |
| Self-hosted customer failure | Customer-managed | Customer-managed | Runbook + restore script provided |

**DR runbook** stored in `docs/runbooks/disaster-recovery.md` in the repository. Updated with every infrastructure change.

## Phase 12 — CI/CD

All pipelines run on **GitHub Actions**. The monorepo has three top-level packages: `src/backend`, `src/frontend`, `src/mobile`. Each has its own workflow. A shared `deploy.yml` orchestrates production deployments.

---

### Repository Structure

```
circlate/
├── src/
│   ├── backend/          # ASP.NET Core 9 solution
│   ├── frontend/         # Next.js app
│   └── mobile/           # Flutter app
├── infra/
│   ├── docker-compose.yml
│   ├── keycloak/
│   └── helm/
├── docs/
└── .github/
    └── workflows/
        ├── backend.yml
        ├── frontend.yml
        ├── mobile-android.yml
        ├── mobile-ios.yml
        └── deploy.yml
```

---

### Backend Pipeline — `backend.yml`

**Triggers:** Push to `main` or any `feature/**` branch; pull request to `main`.

**Path filter:** Only runs when `src/backend/**` changes.

```yaml
name: Backend CI
on:
  push:
    branches: [main, 'feature/**']
    paths: ['src/backend/**']
  pull_request:
    branches: [main]
    paths: ['src/backend/**']

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_PASSWORD: test
          POSTGRES_DB: circlate_test
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports: ['5432:5432']

    steps:
      - uses: actions/checkout@v4

      - name: Setup .NET 9
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '9.0.x'

      - name: Restore dependencies
        run: dotnet restore
        working-directory: src/backend

      - name: Build
        run: dotnet build --no-restore --configuration Release
        working-directory: src/backend

      - name: Run unit tests
        run: dotnet test --no-build --configuration Release --filter Category=Unit
        working-directory: src/backend

      - name: Run integration tests
        run: dotnet test --no-build --configuration Release --filter Category=Integration
        working-directory: src/backend
        env:
          ConnectionStrings__Platform: "Host=localhost;Port=5432;Database=circlate_test;Username=postgres;Password=test"

      - name: Publish artifact
        if: github.ref == 'refs/heads/main'
        run: dotnet publish --configuration Release --output ./publish
        working-directory: src/backend

      - name: Build Docker image
        if: github.ref == 'refs/heads/main'
        run: |
          docker build -t ${{ secrets.REGISTRY_URL }}/circlate-api:${{ github.sha }} src/backend
          docker push ${{ secrets.REGISTRY_URL }}/circlate-api:${{ github.sha }}
          docker tag ${{ secrets.REGISTRY_URL }}/circlate-api:${{ github.sha }} \
                     ${{ secrets.REGISTRY_URL }}/circlate-api:latest
          docker push ${{ secrets.REGISTRY_URL }}/circlate-api:latest
```

**Quality gates:** Build must pass, all tests green, Docker image must push before deploy is triggered.

---

### Frontend Pipeline — `frontend.yml`

**Triggers:** Push to `main` or `feature/**`; PR to `main`. Path filter: `src/frontend/**`.

```yaml
name: Frontend CI
jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js 20
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
          cache-dependency-path: src/frontend/package-lock.json

      - name: Install dependencies
        run: npm ci
        working-directory: src/frontend

      - name: Type check
        run: npx tsc --noEmit
        working-directory: src/frontend

      - name: Lint
        run: npm run lint
        working-directory: src/frontend

      - name: Run tests
        run: npm test -- --coverage
        working-directory: src/frontend

      - name: Build
        run: npm run build
        working-directory: src/frontend
        env:
          NEXT_PUBLIC_API_URL: ${{ secrets.STAGING_API_URL }}

      - name: Build Docker image
        if: github.ref == 'refs/heads/main'
        run: |
          docker build -t ${{ secrets.REGISTRY_URL }}/circlate-frontend:${{ github.sha }} src/frontend
          docker push ${{ secrets.REGISTRY_URL }}/circlate-frontend:${{ github.sha }}
```

---

### Flutter Pipeline — `mobile-android.yml`

**Triggers:** Push to `main`; PR to `main`. Path filter: `src/mobile/**`.

```yaml
name: Mobile Android Build
jobs:
  build-android:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Java 17
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Setup Flutter
        uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.24.x'
          channel: 'stable'

      - name: Flutter pub get
        run: flutter pub get
        working-directory: src/mobile

      - name: Flutter analyze
        run: flutter analyze
        working-directory: src/mobile

      - name: Flutter test
        run: flutter test
        working-directory: src/mobile

      - name: Build APK (debug — PR builds)
        if: github.event_name == 'pull_request'
        run: flutter build apk --debug
        working-directory: src/mobile

      - name: Build APK (release — main only)
        if: github.ref == 'refs/heads/main'
        run: |
          flutter build apk --release \
            --dart-define=API_URL=${{ secrets.API_URL }}
        working-directory: src/mobile
        env:
          ANDROID_KEYSTORE_B64: ${{ secrets.ANDROID_KEYSTORE_B64 }}
          ANDROID_KEY_ALIAS: ${{ secrets.ANDROID_KEY_ALIAS }}
          ANDROID_KEY_PASSWORD: ${{ secrets.ANDROID_KEY_PASSWORD }}
          ANDROID_STORE_PASSWORD: ${{ secrets.ANDROID_STORE_PASSWORD }}

      - name: Upload APK artifact
        if: github.ref == 'refs/heads/main'
        uses: actions/upload-artifact@v4
        with:
          name: circlate-android-${{ github.sha }}
          path: src/mobile/build/app/outputs/flutter-apk/app-release.apk
          retention-days: 30

      - name: Upload to Google Play (internal track)
        if: github.ref == 'refs/heads/main'
        uses: r0adkll/upload-google-play@v1
        with:
          serviceAccountJsonPlainText: ${{ secrets.GOOGLE_PLAY_SERVICE_ACCOUNT }}
          packageName: app.circlate.mobile
          releaseFiles: src/mobile/build/app/outputs/flutter-apk/app-release.apk
          track: internal
```

---

### Flutter Pipeline — `mobile-ios.yml`

**Triggers:** Push to `main` only. Runs on `macos-latest` (required for Xcode).

```yaml
name: Mobile iOS Build
jobs:
  build-ios:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Flutter
        uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.24.x'
          channel: 'stable'

      - name: Flutter pub get
        run: flutter pub get
        working-directory: src/mobile

      - name: Install Apple certificates
        uses: apple-actions/import-codesign-certs@v3
        with:
          p12-file-base64: ${{ secrets.APPLE_DISTRIBUTION_CERT_P12_B64 }}
          p12-password: ${{ secrets.APPLE_CERT_PASSWORD }}

      - name: Install provisioning profile
        uses: apple-actions/download-provisioning-profiles@v3
        with:
          bundle-id: app.circlate.mobile
          profile-type: IOS_APP_STORE
          issuer-id: ${{ secrets.APPSTORE_ISSUER_ID }}
          api-key-id: ${{ secrets.APPSTORE_KEY_ID }}
          api-private-key: ${{ secrets.APPSTORE_PRIVATE_KEY }}

      - name: Build IPA
        run: |
          flutter build ipa --release \
            --dart-define=API_URL=${{ secrets.API_URL }} \
            --export-options-plist=ios/ExportOptions.plist
        working-directory: src/mobile

      - name: Upload to TestFlight
        uses: apple-actions/upload-testflight-build@v1
        with:
          app-path: src/mobile/build/ios/ipa/Circlate.ipa
          issuer-id: ${{ secrets.APPSTORE_ISSUER_ID }}
          api-key-id: ${{ secrets.APPSTORE_KEY_ID }}
          api-private-key: ${{ secrets.APPSTORE_PRIVATE_KEY }}
```

---

### Deploy Pipeline — `deploy.yml`

**Triggers:** Completion of both `backend.yml` and `frontend.yml` on `main`.

```yaml
name: Deploy to Production
on:
  workflow_run:
    workflows: ["Backend CI", "Frontend CI"]
    branches: [main]
    types: [completed]

jobs:
  deploy:
    if: ${{ github.event.workflow_run.conclusion == 'success' }}
    runs-on: ubuntu-latest
    environment: production   # requires manual approval in GitHub Environments
    steps:
      - name: Deploy API to OCI / Cloud Run
        run: |
          # Update container image tag in Kubernetes/Cloud Run service
          kubectl set image deployment/circlate-api \
            api=${{ secrets.REGISTRY_URL }}/circlate-api:${{ github.sha }}
          kubectl rollout status deployment/circlate-api

      - name: Deploy Frontend to OCI / Cloud Run
        run: |
          kubectl set image deployment/circlate-frontend \
            frontend=${{ secrets.REGISTRY_URL }}/circlate-frontend:${{ github.sha }}
          kubectl rollout status deployment/circlate-frontend

      - name: Run post-deploy smoke tests
        run: |
          curl -f https://health.circlate.app/api/v1/health
          # Additional smoke test scripts

      - name: Notify Slack on success
        if: success()
        uses: 8398a7/action-slack@v3
        with:
          status: success
          text: "Circlate deployed: ${{ github.sha }}"
```

**Manual approval gate:** GitHub Environments `production` requires a designated reviewer to approve before the deploy step runs. Prevents automatic production deploys from unreviewed changes.

---

### Release Management

| Branch | Purpose | Deploy target |
| --- | --- | --- |
| `feature/**` | Developer feature branches | No deploy; CI only |
| `main` | Integration branch; always deployable | Staging auto-deploy |
| `release/vX.Y.Z` | Release candidate | Staging → manual promote to Production |
| `hotfix/**` | Emergency production fixes | Fast-track to Production after CI |

**Versioning:** Semantic versioning (SemVer). Git tags trigger release builds. `CHANGELOG.md` updated per release using conventional commits.

**Rollback:** Deploy pipeline stores previous image tag. Rollback is `kubectl set image` with the prior SHA — executes in < 2 minutes.

---

### Artifact Strategy

| Artifact | Storage | Retention |
| --- | --- | --- |
| Docker images (API, Frontend) | OCI Container Registry / GCP Artifact Registry | 90 days; latest 10 tags kept |
| Android APK | GitHub Actions Artifacts | 30 days |
| iOS IPA | TestFlight (via App Store Connect) | 90 days |
| Test reports | GitHub Actions Artifacts | 7 days |
| Coverage reports | Codecov | Indefinite (trend tracking) |

**Secrets management:** All secrets stored in GitHub Actions Secrets (repository-level for most; environment-level for production deploy secrets). Never hardcoded or logged.

## Phase 13 — Implementation Roadmap

### Strategy: MVP First

Circlate is built in two waves. **Wave 1 (MVP)** delivers the core platform that an SME can run their workforce on day one. **Wave 2** delivers the professional and analytical modules that drive retention and upsell. No Wave 2 module is started until Wave 1 is production-stable.

**MVP scope:** Tenant Management · Authentication · Organisation · Employees · Documents · Attendance (QR + GPS) · Leave · Recruitment ATS · Expenses · Mobile App · Billing (PocketPay)

**Wave 2 scope:** Training Compliance · Skills Matrix · Asset Management · Performance Management · Metabase Reporting · Helpdesk · Announcements · Executive Dashboard

---

### Wave 1 — MVP

#### Sprint 0 — Foundation (2 weeks)

**Goal:** Infrastructure standing, CI/CD running, authentication working end-to-end.

| Task | Owner |
| --- | --- |
| Monorepo setup: `src/backend`, `src/frontend`, `src/mobile` | Tech Lead |
| Docker Compose dev environment (all services) | DevOps |
| GitHub Actions: backend + frontend pipelines | DevOps |
| Keycloak realm setup: dev + staging realms, roles, client config | Backend |
| ASP.NET Core 9 solution skeleton: Clean Architecture layers, CQRS scaffolding | Backend |
| Next.js 15 project: Tailwind + ShadCN + base layout | Frontend |
| Flutter project: BLoC architecture, routing, auth flow | Mobile |
| Platform database: EF Core migrations for `tenants`, `subscriptions` | Backend |
| OCI / GCP staging environment provisioned | DevOps |
| Subdomain resolver middleware | Backend |

**Exit criteria:** Dev can log in via Keycloak on localhost; CI builds pass; staging environment accessible.

---

#### Sprint 1 — Tenant Provisioning & Auth (2 weeks)

**Goal:** A company can self-register, get a subdomain, and log in.

| Task | Owner |
| --- | --- |
| Company registration API + wizard UI (Steps 1–2: company details + admin account) | Full Stack |
| Email verification (OTP via MailHog dev / SMTP prod) | Backend |
| `TenantProvisioningOrchestrator` saga (DB create, MinIO bucket, Keycloak realm, seed data) | Backend |
| Provisioning progress WebSocket feed | Backend + Frontend |
| Login screen (web) with Keycloak redirect | Frontend |
| Subdomain routing (nginx/Traefik config) | DevOps |
| Onboarding wizard (post-login: logo, timezone, leave types) | Frontend |
| Company Admin settings page (basic: name, logo, timezone) | Frontend |

**Exit criteria:** Full self-signup flow works in staging end-to-end. Admin receives welcome email, can log in, sees empty dashboard.

---

#### Sprint 2 — Organisation & Employees (2 weeks)

**Goal:** HR can structure the company and add employees.

| Task | Owner |
| --- | --- |
| Departments API + CRUD UI | Full Stack |
| Positions API + UI | Full Stack |
| Teams API + UI | Full Stack |
| Employee create/edit form (wizard: Personal → Employment → Contact → Emergency) | Full Stack |
| Employee list (DataTable: search, filter, sort, paginate) | Frontend |
| Employee profile page (all tabs) | Frontend |
| Reporting lines (manager assignment on employment record) | Backend + Frontend |
| Org chart visualisation (tree render, pan/zoom) | Frontend |
| Employee number auto-generation | Backend |
| User account creation on employee creation (Keycloak user + `Employee` role) | Backend |
| Employee invite email (login link + temp password) | Backend |

**Exit criteria:** HR can create a 50-employee company with departments, positions, and an org chart. Each employee can log in.

---

#### Sprint 3 — Attendance (2 weeks)

**Goal:** Employees can clock in via QR and GPS. Managers see real-time attendance.

| Task | Owner |
| --- | --- |
| Shift definition API + UI | Full Stack |
| Shift assignment (employee to shift) | Full Stack |
| QR token generation (rotating 24h) | Backend |
| Clock-in/out API (QR + GPS + QR+GPS modes) | Backend |
| Attendance record creation + overtime/late detection logic | Backend |
| Attendance dashboard (web): today's status, real-time feed | Frontend |
| Monthly attendance calendar (web) | Frontend |
| Manual attendance correction (HR) | Full Stack |
| Office location (geofence) configuration | Full Stack |
| Flutter: QR scanner screen (camera + scan logic) | Mobile |
| Flutter: GPS clock-in screen (map + geofence display) | Mobile |
| Flutter: mobile clock-in/out buttons on home screen | Mobile |
| Offline sync queue (mobile → server) | Mobile + Backend |

**Exit criteria:** Employee on mobile scans QR, clocks in in < 5 seconds. Manager sees live dashboard. Offline sync works after 24h disconnect.

---

#### Sprint 4 — Leave Management (2 weeks)

**Goal:** Employees request leave on mobile; managers approve with one tap.

| Task | Owner |
| --- | --- |
| Leave type configuration UI (admin) | Full Stack |
| Leave balance initialisation on employee creation | Backend |
| Public holiday calendar (Brunei built-in; custom holiday add) | Full Stack |
| Leave request API + web form | Full Stack |
| Manager approval API + push notification | Backend |
| Leave calendar (team/dept view, web) | Frontend |
| Leave balance display (web + mobile) | Full Stack |
| Flutter: leave request wizard (3-step, < 60s target) | Mobile |
| Flutter: manager approval screen (one-tap) | Mobile |
| Deputy assignment on leave request (optional field; covered-by display on leave list) | Full Stack |
| Attendance integration: approved leave marks attendance as Leave | Backend |

**Exit criteria:** Full leave request → approval → balance deduction cycle in < 60 seconds on mobile.

---

#### Sprint 5 — Document Management (2 weeks)

**Goal:** HR can upload and manage documents. Employees see their own docs.

| Task | Owner |
| --- | --- |
| MinIO integration service (upload, presigned URL, delete) | Backend |
| Document upload API + drag-and-drop UI | Full Stack |
| Document library (folder tree + list) | Frontend |
| Document categories and visibility flags | Backend + Frontend |
| Version control (upload new version, version history list) | Full Stack |
| Document expiry tracking + 30-day alert | Backend |
| Employee-visible documents on profile tab | Frontend |
| Flutter: document list + download | Mobile |
| Document generation: Employment Letter template (HTML → PDF via headless browser) | Backend + Frontend |

**Exit criteria:** HR generates an employment letter for an employee in < 60 seconds. Employee downloads it on mobile.

---

#### Sprint 6 — Hiring (3 weeks)

**Goal:** End-to-end hiring flow — from job posting to onboarded employee, including work pass tracking and certification handoff.

> **Public-facing module name:** Hiring (not "ATS")

##### Bounded Context Notes

- Candidate documents uploaded during hiring **migrate automatically to the employee record on hire confirmation** — no re-upload
- Certifications (diplomas, professional certs) are **created as structured records from candidate uploads** — issuing body, cert number, expiry
- Nationality determines work pass requirement automatically via tenant-configured `LocalNationalities` list — no manual flag
- Hiring participants (Hiring Manager, Interviewers, Offer Approver) are `EmployeeId` FKs on the job posting, interview record, and offer respectively

##### Domain Entities

| Entity | Key Fields |
| --- | --- |
| `JobPosting` | TenantId, Title, Department, HiringManagerId (FK->Employee), Stage, IsOpen |
| `Candidate` | TenantId, FullName, Email, Nationality, LinkedJobPostingId |
| `Application` | CandidateId, JobPostingId, Stage, Notes |
| `Interview` | ApplicationId, ScheduledAt, InterviewerIds[], Notes, Outcome |
| `Offer` | ApplicationId, Salary, Currency, StartDate, ApproverId (FK->Employee), Status, AcceptedAt |
| `WorkPassApplication` | OfferId, PassType, AppliedAt, ApprovedAt, PassNumber, ExpiresAt, DocumentId (FK->Document) |
| `OnboardingChecklist` | EmployeeId, Tasks (name, dueDate, completedAt, assignedToId) |
| `Certification` | EmployeeId, Name, IssuingBody, CertNumber, IssuedAt, ExpiresAt, DocumentId (FK->Document) |

##### Work Pass Types (Brunei)

| Type | Condition |
| --- | --- |
| Employment Pass | Professional/managerial foreign hire |
| Temporary Employment Pass (TEP) | Skilled/semi-skilled foreign hire |
| None | Nationality in tenant `LocalNationalities` list (e.g. Brunei Citizen, Brunei PR) |

##### Pipeline Stages

```
Job Posted -> Screening -> Interview -> Offer -> Work Pass (if required) -> Onboarding -> Hired
```

Work Pass stage is skipped automatically for local nationals.

##### Hiring Participants

| Role | Assigned On | Responsibility |
| --- | --- | --- |
| Hiring Manager | Job posting creation | Owns the requisition, makes final call |
| Interviewer(s) | Per interview record | Notified on assignment, submits outcome |
| Offer Approver | Offer creation | Must approve before offer letter is sent (optional per tenant) |

##### Tasks

| Task | Owner |
| --- | --- |
| Domain entities + DB migration (all 8 entities above) | Backend |
| Job posting API + create/edit UI | Full Stack |
| Candidate profile API + UI (with nationality field) | Full Stack |
| Application API (stage transitions with participant notifications) | Backend |
| Kanban board UI (stages as columns, drag-and-drop) | Frontend |
| Candidate document upload (CV, passport, certs, diplomas) | Full Stack |
| Interview scheduling + interviewer assignment UI | Full Stack |
| Offer creation + approver assignment + offer letter PDF | Full Stack |
| Nationality check -> work pass flow insertion | Backend |
| Work pass application tracking UI | Frontend |
| On-hire: document migration to employee record | Backend |
| On-hire: certification records created from candidate uploads | Backend |
| Onboarding checklist (task list, assignee, due date) | Full Stack |
| Pipeline stats (conversion rates, time-to-hire, open roles) | Full Stack |
| Tenant config: LocalNationalities list (Admin) | Full Stack |

**Exit criteria:** Foreign candidate moves from Applied to Hired; work pass step present and tracked; candidate documents visible on employee profile post-hire; onboarding checklist assigned and completable.

---

#### Sprint 7 — Expenses (2 weeks)

**Goal:** Employees submit expense claims on mobile; two-step approval.

| Task | Owner |
| --- | --- |
| Expense claim API (create, submit, approve, reject, pay) | Backend |
| Expense item API + receipt upload | Backend |
| Expense list + detail UI (web) | Frontend |
| Approval workflow (Manager → Finance, configurable) | Backend |
| Approval inbox (manager + finance views) | Frontend |
| Finance export (CSV) | Backend + Frontend |
| Flutter: expense claim wizard (category → photo → amount → submit, < 2 min) | Mobile |
| Flutter: receipt camera capture + thumbnail preview | Mobile |

**Exit criteria:** Employee submits expense from photo to submission in < 2 minutes. Finance marks paid. CSV exports correctly.

---

#### Sprint 8 — Billing & Announcements (2 weeks)

**Goal:** PocketPay billing live. Announcement module complete. MVP feature-complete.

| Task | Owner |
| --- | --- |
| PocketPay gateway integration (create customer, subscription, charge) | Backend |
| Subscription plan selection UI (pricing page) | Frontend |
| Trial-to-paid conversion flow | Full Stack |
| Payment webhook handler (all events) | Backend |
| Invoice storage + PDF generation | Backend |
| Billing settings page (plan, invoices, payment method) | Frontend |
| Announcements API (create, publish, target, read receipt) | Backend |
| Announcement feed UI + compose UI | Frontend |
| Flutter: announcement feed on home screen | Mobile |
| Push notification: FCM (Android) + APNs (iOS) setup | Mobile + Backend |

**Exit criteria:** Customer completes paid subscription on staging. Webhook updates subscription state. First company announcement sent with push notifications received on mobile.

---

#### Sprint 9 — Polish, Security & Launch Prep (2 weeks)

**Goal:** Production-ready. Hardened, tested, monitored.

| Task | Owner |
| --- | --- |
| RBAC enforcement audit (all APIs tested against permissions matrix) | Backend |
| Audit log implementation (all write operations) | Backend |
| Rate limiting + CORS config in production | Backend |
| PII encryption (IC, bank account) | Backend |
| WCAG 2.1 AA audit + fixes (focus rings, ARIA, contrast) | Frontend |
| Load testing (k6): 500 concurrent users, all critical endpoints | DevOps |
| Penetration test (basic: OWASP Top 10 checklist) | Security |
| Self-hosted Docker Compose package + documentation | DevOps |
| App Store submission (iOS TestFlight external beta) | Mobile |
| Google Play submission (closed testing track) | Mobile |
| Monitoring setup: Grafana dashboards, Sentry, Crashlytics | DevOps |
| Onboarding wizard refinement (guided tour, demo data seeder) | Full Stack |
| Marketing site: circlate.app landing page | Frontend |

**Exit criteria:** Penetration test passed. Load test passes. Apps approved on TestFlight external. Self-hosted works on fresh VPS. Marketing site live.

---

### MVP Launch Milestone — End of Sprint 9

**Expected timeline:** 18 weeks from Sprint 0 start.

**Deliverables at launch:**

- Circlate SaaS live at `circlate.app`
- iOS app on TestFlight (App Store submission in progress)
- Android app on Google Play (open testing)
- Self-hosted Docker Compose package available
- Free tier: fully functional
- Business tier: Recruitment + Expenses unlocked
- PocketPay billing live
- 5 pilot customers onboarded (Brunei)

---

### Wave 2 — Post-MVP Modules

#### Sprint 10–11 — Training Compliance (4 weeks)

- Course + provider registry
- Compliance requirement setup
- Training record management + certificate upload
- Expiry alert scheduler (cron)
- Compliance matrix view
- HR + manager compliance dashboards
- Mobile: certificate upload from camera
- Metabase: compliance reports

#### Sprint 12 — Skills Matrix (2 weeks)

- Skill taxonomy management
- Employee skill rating (HR + manager)
- Skills matrix grid view
- Gap analysis + succession planning
- Export to Excel

#### Sprint 13 — Asset Management (2 weeks)

- Asset registry + CRUD
- Assignment + return workflow
- Termination trigger (auto asset return request)
- Mobile: view assigned assets

#### Sprint 14–15 — Performance Management (4 weeks)

- Review cycle creation + stage management
- Goal setting (OKR/KPI)
- Self-assessment + manager review forms
- 360 feedback
- Rating + overall review

#### Sprint 16 — Helpdesk (2 weeks)

- Ticket submission (web + mobile)
- HR/IT/Facilities queues
- SLA tracking
- Comment thread
- Agent dashboard

#### Sprint 17 — Metabase Reporting & Executive Dashboard (2 weeks)

- Metabase shared service setup
- Row-level security per tenant data source
- 10 pre-built named reports (Headcount, Attendance, Leave, Expenses, Compliance, Turnover, Overtime, Recruitment Pipeline, Skills Gap, Asset Inventory)
- Executive Dashboard (read-only analytics role)
- Signed embed URL API

#### Sprint 18 — Enterprise Features (2 weeks)

- SSO: Azure AD + Google Workspace OIDC/SAML2 Keycloak federation
- White-label: tenant brand colour override, custom domain with CNAME verification
- API access: developer portal, API key management
- Audit log search + export UI
- Self-hosted Kubernetes Helm chart + documentation

---

### Full Timeline Summary

| Phase | Sprints | Weeks | Key Deliverable |
| --- | --- | --- | --- |
| Foundation | S0 | 1–2 | Infrastructure + CI/CD |
| Tenant + Auth | S1 | 3–4 | Self-signup live |
| Org + Employees | S2 | 5–6 | 50-employee company |
| Attendance | S3 | 7–8 | QR/GPS clock-in live |
| Leave | S4 | 9–10 | Mobile leave + approval |
| Documents | S5 | 11–12 | Letter generation |
| Recruitment | S6 | 13–14 | Kanban ATS live |
| Expenses | S7 | 15–16 | Mobile expense claims |
| Billing + Announce | S8 | 17–18 | PocketPay + push notifications |
| Launch Prep | S9 | 19–20 | Production hardening + store submission |
| **MVP Launch** |  | **Week 20** | **Circlate v1.0 live** |
| Training Compliance | S10–11 | 21–24 | Compliance matrix |
| Skills + Assets | S12–13 | 25–28 | Skills matrix + asset tracking |
| Performance | S14–15 | 29–32 | Review cycles |
| Helpdesk + Reporting | S16–17 | 33–36 | Metabase + Executive Dashboard |
| Enterprise | S18 | 37–38 | SSO + white-label |
| **v2.0 Feature-Complete** |  | **Week 38** | **Full platform live** |

---

### Team Composition (Recommended)

| Role | Count | Covers |
| --- | --- | --- |
| Tech Lead / Backend Senior | 1 | Architecture, backend, code review |
| Backend Engineer | 1 | APIs, domain logic, integrations |
| Full Stack Engineer | 1 | Features spanning both layers |
| Frontend Engineer | 1 | React/Next.js, design system |
| Flutter Engineer | 1 | Mobile app (iOS + Android) |
| DevOps / Infra | 0.5 | CI/CD, cloud, monitoring |
| Product / QA | 0.5 | Acceptance testing, backlog |

**Total:** \~6 FTE. Scales to 8–10 FTE post-MVP for Wave 2 acceleration.

---

### Definition of Done

A story is Done when:

1. Code reviewed and approved (at least 1 reviewer)
2. Unit tests written and passing
3. Integration tests passing in CI
4. Feature tested against acceptance criteria in staging
5. API endpoint documented (OpenAPI spec updated)
6. No P1/P2 bugs open against the story
7. RBAC permissions verified for all roles in scope
8. Audit log entries verified for all write operations
9. Mobile: tested on iOS Simulator + Android Emulator minimum; physical device for QR/GPS flows
﻿
---

## BC-20 · Workforce Time Management

> **Status:** Approved — ARB Review Passed
> **Wave:** 2 · Professional Tier
> **Author:** Principal Architect
> **Date:** 2026-11-11
> **Depends on:** BC-07 Attendance, BC-10 Org Chart, BC-09 Expenses (authority model)

---

### 1. Business Analysis

#### Problem Statement

Attendance tracking (BC-07) confirms *presence* — it records when an employee arrives and departs. It answers "Was Ahmad here on Tuesday?" It does not answer "What was Ahmad working on Tuesday, and for how long?" These are fundamentally different questions: the first feeds payroll compliance; the second feeds project billing, resource planning, and performance analysis.

ASEAN SMEs in professional services (consulting, legal, engineering, government contracting) must allocate time against engagements for client billing and internal cost accounting. No credible Workforce OS for this segment can omit timesheets.

#### Business Outcomes

| # | Outcome | Metric |
|---|---------|--------|
| 1 | HR/Finance can produce a labour cost report per project without manual spreadsheets | Report generated < 5 min, zero manual data entry |
| 2 | Employees submit weekly timesheets with < 5 min effort | Submission rate > 90% by end of quarter 1 |
| 3 | Managers approve/reject timesheets without leaving Circlate | Approval turnaround median < 24 h |
| 4 | Integration with Payroll module uses timesheet-verified hours for overtime calculation | Payroll diff < 1% vs attendance-only baseline |
| 5 | Professional-tier upsell: 40% of Starter tenants convert within 6 months of GA | Revenue tracked via subscription events |

#### Stakeholder Map

| Role | Pain | Gain |
|------|------|------|
| Employee | Filling timesheets in Excel, emailing to manager | One-click weekly submission from mobile or web |
| Project Manager | No visibility of team allocation without chasing | Real-time burn dashboard, over/under alerts |
| Finance | Manual reconciliation of hours to billing runs | API export to billing system, locked timesheet audit trail |
| HR | Overtime disputes, no audit log | Immutable correction history with reason codes |
| Tenant Admin | No config control over approval chains | Policy-based rules: who approves, escalation timeout |

#### Regulatory Context (Brunei)

- Employment Order 2009 §17–19: overtime records must be kept for three years
- Government contracts (PAPD guidelines): staff utilisation reports required for cost-reimbursable engagements
- PDN / PDPO (forthcoming): employee time records are personal data; retention and access rules apply

---

### 2. Bounded Context Definition

**BC-20 Workforce Time Management** is distinct from:

| BC | Responsibility | Boundary |
|----|----------------|---------|
| BC-07 Attendance | Presence recording (clock-in/out) | Supplies daily confirmed hours as a *read model* input to BC-20; does not own allocation |
| BC-09 Expenses | Cost claims, financial approval | Shares authority model but owns its own approval domain |
| BC-10 Org Chart | Reporting lines, position hierarchy | BC-20 queries for manager resolution; does not write to org chart |
| BC-18 Payroll (future) | Pay calculation | Consumes BC-20 approved timesheet summaries as payroll input via integration event |

**BC-20 owns:**
- Timesheet lifecycle (Draft → Submitted → Approved / Rejected → Locked)
- Project/task code catalogue
- Approval workflow definition per tenant policy
- Audit trail of all mutations
- Reporting aggregates (hours by project, by employee, by period)

**BC-20 does NOT own:**
- Clock-in / clock-out events (BC-07)
- Leave records (BC-05)
- Payroll disbursement (BC-18)

---

### 3. Ubiquitous Language

| Term | Definition |
|------|-----------|
| **Timesheet** | A collection of time entries for one employee covering a defined period (typically one week), subject to a single approval decision |
| **Time Entry** | One allocation line on a timesheet: date, project/task, hours, description |
| **Period** | The unit of a timesheet — weekly by default; configurable per tenant to bi-weekly or monthly |
| **Project Code** | A billable or internal cost code against which time is allocated |
| **Task** | An optional sub-code under a Project Code |
| **Submission** | The act of an employee finalising a draft timesheet and presenting it for manager approval |
| **Approval** | Manager's decision to Accept or Return a submitted timesheet |
| **Lock** | Immutable state after payroll processing; no further edits permitted |
| **Correction** | An HR-initiated override with a mandatory reason code, creating an audit entry |
| **Burn** | Accumulated approved hours against a Project Code budget, used in project planning |

---

### 4. Domain Model

```
TimesheetPeriodPolicy          Timesheet                    TimeEntry
─────────────────────          ─────────────────            ──────────────────
TenantId: Guid                 Id: Guid (PK)                Id: Guid (PK)
PeriodType: enum               TenantId: Guid               TimesheetId: Guid (FK)
  Weekly                       EmployeeId: Guid (FK)        Date: DateOnly
  BiWeekly                     PeriodStart: DateOnly        ProjectCodeId: Guid (FK)
  Monthly                      PeriodEnd: DateOnly          TaskId: Guid? (FK)
StartDayOfWeek: DayOfWeek      Status: TimesheetStatus      Hours: decimal (0.25 steps)
SubmissionDeadlineDays: int      Draft                      Description: string?
AutoReminderEnabled: bool        Submitted                  Source: EntrySource
AutoReminderHours: int           Approved                     Manual
                                 Rejected                     ImportedFromAttendance
                                 Locked                     CreatedAt: DateTime
                               SubmittedAt: DateTime?        UpdatedAt: DateTime
                               ReviewedAt: DateTime?         IsManualCorrection: bool
                               ReviewedBy: Guid?
                               Notes: string?

ProjectCode                    TimesheetApprovalPolicy       TimesheetAuditEntry
──────────────                 ───────────────────────       ──────────────────
Id: Guid (PK)                  TenantId: Guid (PK)           Id: Guid (PK)
TenantId: Guid                 ApproverResolution: enum      TimesheetId: Guid (FK)
Code: string                     DirectManager               ActorId: Guid
Name: string                     SpecificRole                Action: string
Description: string?             Disabled                   OldStatus: TimesheetStatus?
IsActive: bool                 EscalationEnabled: bool       NewStatus: TimesheetStatus?
IsBillable: bool               EscalationAfterHours: int     Reason: string?
Budget: decimal? (hours)       EscalationTargetRoleId: Guid? Timestamp: DateTime
StartDate: DateOnly?
EndDate: DateOnly?
ClientName: string?
ExternalCode: string?
```

#### Invariants

1. `Hours` per entry must be a multiple of 0.25 and in range [0.25, 24].
2. Sum of hours on a single date across all entries for one employee must not exceed 24.
3. A timesheet cannot be Submitted if any entry has 0 hours.
4. Only HR role may apply Correction to a Locked timesheet.
5. A Locked timesheet generates an immutable `TimesheetAuditEntry` before any override.
6. `PeriodStart` and `PeriodEnd` are computed from `TimesheetPeriodPolicy`; they cannot be edited directly.

---

### 5. Database Design

```sql
-- Timesheet period policy (one per tenant)
CREATE TABLE timesheet_period_policies (
    tenant_id        UUID PRIMARY KEY REFERENCES tenants(id),
    period_type      TEXT NOT NULL DEFAULT 'Weekly',
    start_dow        INT  NOT NULL DEFAULT 1,
    deadline_days    INT  NOT NULL DEFAULT 2,
    reminder_enabled BOOLEAN NOT NULL DEFAULT TRUE,
    reminder_hours   INT  NOT NULL DEFAULT 48
);

-- Project codes
CREATE TABLE project_codes (
    id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id     UUID NOT NULL REFERENCES tenants(id) ON DELETE CASCADE,
    code          TEXT NOT NULL,
    name          TEXT NOT NULL,
    description   TEXT,
    is_active     BOOLEAN NOT NULL DEFAULT TRUE,
    is_billable   BOOLEAN NOT NULL DEFAULT FALSE,
    budget_hours  NUMERIC(10,2),
    start_date    DATE,
    end_date      DATE,
    client_name   TEXT,
    external_code TEXT,
    created_at    TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    UNIQUE (tenant_id, code)
);

-- Tasks (sub-codes)
CREATE TABLE tasks (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    project_code_id UUID NOT NULL REFERENCES project_codes(id) ON DELETE CASCADE,
    name            TEXT NOT NULL,
    is_active       BOOLEAN NOT NULL DEFAULT TRUE
);

-- Timesheets
CREATE TABLE timesheets (
    id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id    UUID NOT NULL REFERENCES tenants(id) ON DELETE CASCADE,
    employee_id  UUID NOT NULL REFERENCES employees(id) ON DELETE CASCADE,
    period_start DATE NOT NULL,
    period_end   DATE NOT NULL,
    status       TEXT NOT NULL DEFAULT 'Draft',
    submitted_at TIMESTAMPTZ,
    reviewed_at  TIMESTAMPTZ,
    reviewed_by  UUID REFERENCES employees(id),
    notes        TEXT,
    created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at   TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    UNIQUE (tenant_id, employee_id, period_start)
);

-- Time entries (timesheets — distinct from BC-07 attendance time_entries)
CREATE TABLE time_entries_ts (
    id                   UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    timesheet_id         UUID NOT NULL REFERENCES timesheets(id) ON DELETE CASCADE,
    date                 DATE NOT NULL,
    project_code_id      UUID NOT NULL REFERENCES project_codes(id),
    task_id              UUID REFERENCES tasks(id),
    hours                NUMERIC(4,2) NOT NULL,
    description          TEXT,
    source               TEXT NOT NULL DEFAULT 'Manual',
    created_at           TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at           TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    is_manual_correction BOOLEAN NOT NULL DEFAULT FALSE
);

-- Approval policy
CREATE TABLE timesheet_approval_policies (
    tenant_id              UUID PRIMARY KEY REFERENCES tenants(id),
    approver_resolution    TEXT NOT NULL DEFAULT 'DirectManager',
    escalation_enabled     BOOLEAN NOT NULL DEFAULT FALSE,
    escalation_after_hours INT NOT NULL DEFAULT 48,
    escalation_role_id     UUID
);

-- Audit log
CREATE TABLE timesheet_audit_entries (
    id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    timesheet_id UUID NOT NULL REFERENCES timesheets(id) ON DELETE CASCADE,
    actor_id     UUID NOT NULL,
    action       TEXT NOT NULL,
    old_status   TEXT,
    new_status   TEXT,
    reason       TEXT,
    timestamp    TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_timesheets_tenant_employee ON timesheets (tenant_id, employee_id);
CREATE INDEX idx_timesheets_period ON timesheets (tenant_id, period_start, period_end);
CREATE INDEX idx_time_entries_ts_timesheet ON time_entries_ts (timesheet_id);
CREATE INDEX idx_time_entries_ts_project ON time_entries_ts (project_code_id, date);
CREATE INDEX idx_audit_timesheet ON timesheet_audit_entries (timesheet_id);
```

> **Note:** `time_entries_ts` is named to avoid collision with BC-07 `time_entries` (clock-in/out). A view `v_employee_daily_hours` can join both for a unified daily picture.

---

### 6. Approval Workflow

```
Employee                                     Manager / Approver
   |                                                 |
   | [completes entries]                             |
   |------ Submit ---------------------------------> |
   |                                           Notification
   |                                                 |
   |                                        [Reviews timesheet]
   |                                                 |
   |                    +---------------- Approve -> Approved -> auto-Lock at payroll
   | <-----------------+
   | [Returned]         +-------- Return (Reject) -> Rejected

If ApproverResolution = Disabled -> auto-Approve on Submit
If EscalationEnabled and no action after N hours -> escalate to role
```

#### Status Transitions

| From | To | Actor | Condition |
|------|-----|-------|-----------|
| Draft | Submitted | Employee | All entries valid |
| Submitted | Approved | Manager / HR | — |
| Submitted | Rejected | Manager / HR | Reason required |
| Rejected | Draft | Employee | Re-open for editing |
| Approved | Locked | System (payroll trigger) | Payroll run event |
| Locked | Locked* | HR only | Correction with mandatory reason; always writes audit entry first |

---

### 7. Domain Events

All events published via Outbox pattern to the internal message bus.

| Event | Trigger | Consumers |
|-------|---------|-----------|
| `TimesheetSubmitted` | Employee submits | Notification → manager, Audit |
| `TimesheetApproved` | Manager approves | Notification → employee, Audit, BC-18 Payroll stub |
| `TimesheetRejected` | Manager rejects | Notification → employee, Audit |
| `TimesheetLocked` | Payroll run | Audit |
| `TimesheetCorrected` | HR correction post-lock | Audit, BC-18 Payroll diff |
| `ProjectCodeCreated` | Admin creates code | Audit |
| `ProjectCodeDeactivated` | Admin deactivates | Notification → employees with open entries on that code |

#### Event Envelope

```json
{
  "eventId": "uuid",
  "eventType": "TimesheetSubmitted",
  "tenantId": "uuid",
  "occurredAt": "2026-11-11T08:00:00Z",
  "payload": {
    "timesheetId": "uuid",
    "employeeId": "uuid",
    "periodStart": "2026-11-10",
    "periodEnd": "2026-11-14"
  }
}
```

---

### 8. Notifications

| Trigger | Recipient | Channel | Template |
|---------|-----------|---------|---------|
| Timesheet submitted | Direct manager | In-app + email | "{{employee}} submitted timesheet for {{period}}. Review by {{deadline}}." |
| Approval overdue (escalation) | Escalation role | In-app + email | "Timesheet by {{employee}} unapproved for {{hours}}h. Escalated to you." |
| Timesheet approved | Employee | In-app | "Your timesheet for {{period}} was approved." |
| Timesheet rejected | Employee | In-app + email | "Your timesheet for {{period}} was returned: {{reason}}" |
| Submission deadline approaching | Employee | In-app | "Your timesheet for {{period}} is due in {{hours}}h." |
| Project code budget 80% consumed | Project owner | In-app + email | "{{code}} is at {{pct}}% of budget ({{used}}/{{budget}} hours)." |

---

### 9. API Design

Base path: `/api/timesheets`
Auth: Bearer JWT, `tid` claim for tenant isolation.

#### Timesheets

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/timesheets` | List own timesheets (employee) or all (manager/HR) with filters |
| GET | `/api/timesheets/{id}` | Get single timesheet with entries |
| POST | `/api/timesheets` | Create draft for a period (idempotent — returns existing if period exists) |
| POST | `/api/timesheets/{id}/submit` | Submit for approval |
| POST | `/api/timesheets/{id}/approve` | Manager/HR approve |
| POST | `/api/timesheets/{id}/reject` | Manager/HR reject (body: `{ "reason": "..." }`) |
| POST | `/api/timesheets/{id}/reopen` | Employee reopen after rejection -> Draft |
| POST | `/api/timesheets/{id}/correct` | HR correction on locked timesheet |
| GET | `/api/timesheets/{id}/audit` | Audit trail for a timesheet |

#### Time Entries

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/timesheets/{id}/entries` | List entries |
| POST | `/api/timesheets/{id}/entries` | Add entry |
| PUT | `/api/timesheets/{id}/entries/{entryId}` | Update entry |
| DELETE | `/api/timesheets/{id}/entries/{entryId}` | Remove entry |

#### Project Codes

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/project-codes` | List active codes (tenant-scoped) |
| POST | `/api/project-codes` | Create code (HR/Admin) |
| PUT | `/api/project-codes/{id}` | Update code |
| DELETE | `/api/project-codes/{id}` | Deactivate code (soft delete) |
| GET | `/api/project-codes/{id}/burn` | Hours burn summary |

#### Policy

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/timesheets/policy` | Get tenant period policy |
| PUT | `/api/timesheets/policy` | Update tenant period policy (Admin) |
| GET | `/api/timesheets/approval-policy` | Get approval policy |
| PUT | `/api/timesheets/approval-policy` | Update approval policy (Admin) |

#### Reporting

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/timesheets/reports/summary` | Hours by employee x project x period |
| GET | `/api/timesheets/reports/burn` | Project burn report |
| GET | `/api/timesheets/reports/export` | CSV export (Finance role) |

---

### 10. UI/UX Design

#### Employee: Weekly Timesheet View

```
+------------------------------------------------------------------+
|  Week 10-14 Nov 2026                            [Draft]  [Submit]|
+------------------+------+------+------+------+------+-----------+
| Project / Task   | Mon  | Tue  | Wed  | Thu  | Fri  |  Total    |
+------------------+------+------+------+------+------+-----------+
| PRJ-001 Portal   |  4   |  3.5 |  -   |  2   |  4   |  13.5 h  |
| PRJ-002 Support  |  -   |  -   |  4   |  2   |  -   |   6.0 h  |
| ADMIN-01 Admin   |  -   |  0.5 |  -   |  1   |  -   |   1.5 h  |
| [+ Add row]      |      |      |      |      |      |          |
+------------------+------+------+------+------+------+-----------+
| Total            |  4   |  4   |  4   |  5   |  4   |  21.0 h  |
+------------------+------+------+------+------+------+-----------+
```

- Cells are inline-editable (click to type)
- Hours from BC-07 attendance can be imported as a scaffold ("Import from attendance" button)
- Overtime cells highlighted amber
- Status pill: Draft / Submitted / Approved / Rejected / Locked
- Submit button disabled if any day total > 24

#### Manager: Approval Queue

```
+-----------------------------------------------------------+
|  Pending Approval (3)                                     |
+------------------+-----------------+------+---------------+
| Employee         | Period          | Hours| Actions       |
+------------------+-----------------+------+---------------+
| Ahmad Razif      | 10-14 Nov       | 38 h | [Review] [>]  |
| Nurul Ain        | 10-14 Nov       | 40 h | [Review] [>]  |
| Haji Zainol      | 3-7 Nov         | 35 h | [Review] [>]  |
+------------------+-----------------+------+---------------+
```

Review opens an inline panel showing the grid + comment box + Approve / Return buttons.

#### HR: Project Burn Dashboard

- Summary cards: Total billable hours this month / budget consumed %
- Table: Project Code | Budget | Used | Remaining | % | Trend
- Export to CSV button (Finance role only)

---

### 11. Reporting

| Report | Dimensions | Filters | Format |
|--------|-----------|---------|--------|
| Employee Timesheet Summary | Employee, Period, Project Code | Date range, Status, Department | Table + CSV |
| Project Burn | Project Code, Month | Date range, Billable flag | Bar chart + Table |
| Overtime Analysis | Employee, Week | Date range, Department | Table + CSV |
| Submission Rate | Employee, Month | Department | % gauge table |
| Approval Turnaround | Manager, Month | — | Median hours table |

**KPI Dashboard Widgets:**
- Hours logged this week (self)
- Pending approvals (manager)
- Project at risk (> 90% burn)
- Overdue timesheets (HR/Admin)

---

### 12. Subscription Packaging

| Feature | Starter | Professional | Enterprise |
|---------|---------|-------------|-----------|
| Attendance tracking (BC-07) | Yes | Yes | Yes |
| Basic timesheet (manual entry, weekly) | — | Yes | Yes |
| Manager approval workflow | — | Yes | Yes |
| Project code catalogue (up to 20 codes) | — | Yes | Yes |
| Unlimited project codes | — | — | Yes |
| Import from attendance | — | Yes | Yes |
| Escalation / approval policy config | — | — | Yes |
| Payroll integration (BC-18) | — | — | Yes |
| Burn dashboard | — | Yes | Yes |
| CSV export | — | Yes | Yes |
| API access (external billing integration) | — | — | Yes |

---

### 13. Delivery Roadmap

BC-20 is a Wave 2 capability (Professional Tier). These phases begin after MVP GA (Sprint 9) and run in parallel with or after the core Wave 2 roadmap, as a Professional/Enterprise tier track.

#### Phase 1 — Foundation (2 weeks)

| Task | Owner |
|------|-------|
| Domain entities, DB migration (timesheets, time_entries_ts, project_codes, tasks) | Backend |
| CQRS commands: CreateTimesheet, AddEntry, UpdateEntry, DeleteEntry, SubmitTimesheet | Backend |
| CQRS queries: GetTimesheets, GetTimesheetById | Backend |
| REST endpoints: timesheet CRUD + submit | Backend |
| Project Code CRUD endpoints | Backend |
| Weekly timesheet grid UI (read + inline edit) | Frontend |
| Project code management page (Admin) | Frontend |

#### Phase 2 — Approval & Policy (2 weeks)

| Task | Owner |
|------|-------|
| ApproveTimesheet, RejectTimesheet, ReopenTimesheet commands | Backend |
| Approval policy entity + endpoints | Backend |
| Manager approval queue UI | Frontend |
| Notifications: submitted, approved, rejected, deadline reminder | Backend |
| Escalation engine (background job, EscalationEnabled policy) | Backend |
| Employee reopen flow after rejection | Frontend |

#### Phase 3 — Reporting & Lock (2 weeks)

| Task | Owner |
|------|-------|
| Lock mechanism (triggered by payroll event stub) | Backend |
| HR correction flow (CorrectTimesheet command, audit entry) | Backend |
| Project burn report + dashboard widget | Full Stack |
| Employee timesheet summary report + CSV export | Backend + Frontend |
| Submission rate / approval turnaround KPIs | Backend |
| "Import from attendance" scaffold feature | Full Stack |

#### Phase 4 — Integration & Polish (2 weeks)

| Task | Owner |
|------|-------|
| Outbox pattern for domain events | Backend |
| BC-18 Payroll integration stub (TimesheetApproved event handler) | Backend |
| Mobile: timesheet view + submit + pull-to-refresh | Mobile |
| Mobile: manager approval swipe action | Mobile |
| Performance: index review, query optimisation | Backend |
| Security: RBAC audit, penetration test items | Backend |

---

### 14. Architecture Validation

#### Conformance to Circlate Clean Architecture

| Layer | BC-20 Component | Conforms? |
|-------|----------------|-----------|
| Domain | `Timesheet`, `TimeEntry`, `ProjectCode`, `Task`, `TimesheetAuditEntry` entities; `TimesheetStatus` enum; invariants as domain methods | Yes |
| Application | CQRS commands/queries via MediatR; `IAppDbContext` interface; no infrastructure imports | Yes |
| Infrastructure | EF Core configurations, Outbox publisher, background escalation job | Yes |
| API | Minimal API endpoint groups `/api/timesheets`, `/api/project-codes`; `RequireAuthorization()` on all; `GetTenantId(ctx)` for multi-tenancy | Yes |
| Frontend | Server components for page shell + data fetch; client components for timesheet grid interactivity | Yes |

#### Multi-tenancy

All queries and mutations are scoped by `TenantId` via `GetTenantId(HttpContext)`. Project codes, timesheets, and policies are tenant-isolated. No cross-tenant data leakage possible through any exposed endpoint.

#### Security

- **RBAC enforcement:** Employee can only view/edit own timesheets; Manager can approve/reject reports within their subtree (resolved via BC-10); HR can override any; Admin manages policy.
- **Locked timesheets:** Enforced at application layer — `CorrectTimesheetCommandHandler` checks `Status == Locked` before allowing correction, and always writes audit entry first.
- **Audit trail:** All status transitions write to `timesheet_audit_entries` before state change (consistent with event-sourcing lite pattern).
- **No clock drift attacks:** `Hours` validated server-side; daily cap (24h) enforced by domain invariant.

#### Scalability

- Timesheets are tenant-partitioned; horizontal sharding by `tenant_id` is straightforward when volume requires it.
- Approval queue query is indexed on `(tenant_id, status)` — O(log n) for typical SME workloads.
- Burn report is pre-aggregated nightly by a background job for tenants with > 50 project codes; real-time for smaller catalogues.

#### Integration Points

| System | Direction | Mechanism |
|--------|-----------|-----------|
| BC-07 Attendance | Inbound | Query attendance `time_entries` by employee + date range to scaffold timesheet entries |
| BC-10 Org Chart | Inbound | Query `GetManagerForEmployee` to resolve approver |
| BC-18 Payroll (future) | Outbound | `TimesheetApproved` / `TimesheetLocked` domain events via Outbox |
| External billing (ERP, Quickbooks) | Outbound | CSV export + optional webhook on `TimesheetLocked` |

#### Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| Employees bulk-enter fictitious hours | Medium | High | Manager approval gate; HR correction audit trail; anomaly flag if hours >> attendance hours by > 20% |
| Manager approval bottleneck | Low | Medium | Escalation timeout configurable; default 48 h; Disabled mode available for flat orgs |
| Table name collision with BC-07 `time_entries` | High (addressed) | High | Named `time_entries_ts`; view `v_employee_daily_hours` joins both |
| Phase 1–4 scope creep | Medium | Medium | Mobile deferred to Phase 4; API-first approach enables mobile to follow web |

---

*BC-20 Workforce Time Management — Principal Architect Sign-off: 2026-11-11*

