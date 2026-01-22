# System Design as Clinical Diagnosis  
## A Disciplined Framework for Architects and Senior Engineers

Most system failures are not caused by poor implementation.  
They are caused by **poor diagnosis**.

Medicine has dealt with this problem for centuries by formalizing how decisions are made under uncertainty. Software architecture—despite dealing with similarly complex, high-stakes systems—often skips this rigor.

This article presents a **5-step system design methodology**, explicitly grounded in **clinical diagnostic practice**, and demonstrates it through two worked examples.

---

## The 5-Step Diagnostic Model for System Design

1. **Discovery** – Chief Complaint & History of Present Illness  
2. **Contract** – Logical and Process Views (Diagnosis)  
3. **Mechanism** – Physical View (Treatment Selection)  
4. **Production Readiness** – Monitoring & Follow-Up  
5. **Synthesis** – Architecture Narrative & Tradeoffs  

---

## Step 1: Discovery — Chief Complaint & History of Present Illness

### Chief Complaint (Primary Business Pain)

In medicine:
> “Why is the patient here today?”

In system design:
> “What business failure is unacceptable?”

Examples:
- Revenue loss
- Regulatory exposure
- User trust erosion
- Operational fragility

If this cannot be stated clearly, no architecture work should begin.

---

### History of Present Illness — SOCRATES for Systems

Borrowed directly from clinical practice:

| SOCRATES | System Design Interpretation |
|--------|------------------------------|
| Site | Which domain or workflow |
| Onset | What changed (scale, usage, regulation) |
| Character | Latency, correctness, cost, fragility |
| Radiation | Downstream / upstream blast radius |
| Associations | Correlated failures or metrics |
| Timing | Constant vs bursty |
| Exacerbators | Load, retries, manual ops |
| Severity | SLO breach, revenue, risk |

This is where **scenarios, metrics, and non-functional requirements** become explicit.

---

### Past & Social History (Context)

Systems do not exist in isolation.

**Past History**
- Legacy systems
- Prior incidents
- Accumulated technical debt

**Social History**
- Team skills and size
- Deployment maturity
- Regulatory and vendor constraints

Architectures fail when they ignore context—not when they lack sophistication.

---

## Step 2: Contract — Logical & Process Views (Diagnosis)

This is the architectural equivalent of forming a **differential diagnosis**.

### Logical View
- Domain model
- Bounded contexts
- Data ownership
- API contracts

### Process View
- Interaction flows
- State transitions
- Failure propagation
- Trust boundaries (Zero Trust by default)

Contracts define **what the system guarantees**—and just as importantly, **what it does not**.

---

## Step 3: Mechanism — Physical View (Treatment Selection)

Only after diagnosis do clinicians choose treatment.

Architecturally, this means selecting:
- Compute models
- Communication patterns
- Storage technologies
- Cloud services and topology

Mechanisms must fit:
- The diagnosed problem
- Organizational constraints
- Risk tolerance

Novelty is not a virtue here—**fitness is**.

---

## Step 4: Production Readiness — Follow-Up

No clinician declares success at prescription time.

Architecture is incomplete without:
- Observability (metrics, logs, traces)
- SLOs and error budgets
- Rollback and recovery
- Capacity and failure testing
- Security and compliance validation

If a system cannot be diagnosed in production, it will fail silently—until it doesn’t.

---

## Step 5: Synthesis — The Architecture Narrative

The final output is not just diagrams.

It is a **defensible narrative**:
- Why this architecture exists
- Which tradeoffs were made
- What risks remain
- How the system evolves safely

---

# Worked Example 1: Global Payments Platform

### Chief Complaint
> “Payment failures and reconciliation mismatches are increasing as we expand internationally.”

### HPI (SOCRATES Highlights)
- **Site:** Authorization, settlement, reconciliation
- **Onset:** New regions added
- **Character:** Intermittent correctness failures
- **Radiation:** Accounting, customer support
- **Severity:** Revenue loss and audit risk

### Context
- Legacy reconciliation system
- Multiple PSPs
- Medium operational maturity
- Regional regulatory variation

### Diagnosis (Contracts)
- Payment Intent as system of record
- Immutable payment attempts
- Asynchronous settlement
- Explicit idempotency and retry semantics

### Mechanism
- Stateless authorization services
- Durable event log
- Async settlement pipelines
- Region-local writes with global reconciliation

### Production Readiness
- End-to-end tracing per payment
- Replayable failure handling
- Audit-grade logs

---

# Worked Example 2: Enterprise Identity & Access Platform

### Chief Complaint
> “Access incidents and permission drift are slowing teams and creating security risk.”

### HPI (SOCRATES Highlights)
- **Site:** Identity, authorization, provisioning
- **Onset:** Rapid team growth and SaaS adoption
- **Character:** Inconsistent access, manual overrides
- **Radiation:** Security, compliance, developer velocity
- **Severity:** High-risk security exposure

### Context
- Multiple identity sources
- Mixed cloud and on-prem systems
- Strong compliance requirements
- Limited IAM expertise across teams

### Diagnosis (Contracts)
- Central identity authority
- Clear separation: authentication vs authorization
- Policy-as-code contracts
- Explicit lifecycle states (provisioned, active, revoked)

### Mechanism
- Central IdP with federation
- Policy engine for authorization
- Event-driven provisioning/deprovisioning
- Immutable audit logs

### Production Readiness
- Access change observability
- Policy testing pipelines
- Automated drift detection

---

## Closing Thought

Great architects do not start with solutions.  
They start with **disciplined diagnostic reasoning**.

By borrowing from clinical medicine—chief complaint, structured history, context awareness, and cautious treatment—system design becomes:
- More resilient
- More explainable
- More aligned with reality

In both medicine and software, the guiding principle is the same:

> **First, do no harm. Then, build something that lasts.**
