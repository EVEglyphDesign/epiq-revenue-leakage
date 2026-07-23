# Epiq Revenue-Leakage Model — Consolidated Canon

**Reference:** EVE-EPIQ-LEAK-MODEL-2026-07-19
**Author:** EVE Glyph Design
**Status:** Propose-only · consolidated source of truth
**Anchored to:** Tobias Polly, polly consulting e.U. — Discovery Business Brief & Discovery Architecture Extract (17 July 2026)

> This file is the single consolidated record of the revenue-leakage model,
> pulled together from the working threads. It is the base the team spins from.
> No SCS / Steel Cloud on any cover. No third-party file codes in the body.
> Attribution below EVE Glyph Design stays inside EGD copy.

---

## 1. Thesis (the one sentence said out loud in the room)

Revenue leakage in enterprise **services** is correctable — but only if you catch
it in the cycle it happens. The category has been serviced by consulting narratives
and dashboards. It has **not** been serviced by a reasoning agent grounded in the
client's own edit history. That is what this model is.

## 2. The stack is the story

- **LangGraph** — Router → Executor → Synthesizer reasoning agent
- **LangChain** — orchestration
- **Langfuse** — end-to-end trace / replay / audit (every answer replayable)
- **Azure AI Foundry** — in-tenant model deployment
- **Postgres mapping of DataSphere** — semantic bridge; agent reasons against a
  Postgres shape of `QM_SAPAI001` / `BFI_JournalSummary_R01` rather than fighting
  DataSphere directly
- **agent-api** in Azure Container Apps, delivered through the registered **Teams** tab

One engine, many lenses. Adding a lens is **configuration, not a new deployment.**

## 3. The reference-model claim

The same architecture — reasoning agent + semantic-layer mapping + trace-backed
delivery — applies to any pattern-analysis surface in the enterprise: revenue
leakage, procurement anomaly, warranty erosion, service-margin drift, contract-edit
exposure. **Revenue leakage is the first productized lens** because it maps directly
to P&L. Epiq is the highest-value near-term instance: services (leakage correctable
in-cycle), tenant already stood up, executive window closing.

## 4. Leakage taxonomy (L1–L6)

| Class | Definition | Where it manifests at Epiq |
|-------|------------|----------------------------|
| L1 | Profitability-visibility leakage | Delayed CO-PA / operating-concern activation; lost pre-activation segment reporting |
| L2 | Reconciliation-mismatch leakage | FI ↔ CO ↔ BW ↔ ACDOCA drift; BW-vs-ACDOCA mismatches in live tenant |
| L3 | Historical-attribution leakage | No auto backfill; DataSphere reconstitution vs. `QM_SAPAI001` via `BFI_JournalSummary_R01` |
| L4 | Document-splitting / master-data retrofit leakage | Reporting-truth effects when splitting activated post-conversion |
| L5 | Audit-trail / period-reconstruction leakage | Post-commitment edits; incomplete audit trails |
| L6 | Commercial-lane leakage | Resource-hour vs. submitted-invoice mismatch |

## 5. Finding schema (output shape)

Each finding is one sentence a finance reader can act on, plus a `langfuse_trace_id`
for replay. Per period, ranked and narrated:

- Which records were edited post-commitment
- Which editors touched them
- Which fields concentrate the changes
- Which patterns cluster (same editor + same field + same timing = probable
  systemic leak, not incident)
- Which of those patterns tie to identifiable P&L lines

## 6. Non-outputs (deliberate)

No aggregate figure. No P&L assertion. No benchmark claim. No output leaves the
tenant. Section titled **"Method, not commitment"** on purpose — putting a dollar
number into a revenue-leakage model is not something anyone in the enterprise space
would ever do.

## 7. Substrate status

Every component **Live / Deployed / Registered**. Delta to deliver the leakage lens
= **one question configuration**. No new SAP extraction, DataSphere space, Teams
registration, model deployment, or security review. Analysis-for-Office retirement
(two weeks, no incremental licensing) is the lived proof of retargeting economics.

## 8. Phasing

- **P0 — Configure** the revenue-leakage lens on the existing agent. No new infra.
- **P1 — Baseline** narrated leakage report against a closed prior period. The
  number executives point to.
- **P2 — In-cycle** correction against the current open period. The number that
  lands on the current P&L.
- **P3 — Second lens** candidate (procurement anomaly or margin drift) off the same
  substrate — proves the substrate claim, not just the leakage claim.

## 9. Decision requested

Green-light **P0 + P1**: leakage-lens configuration and the first narrated report
against a closed prior period.

---

*Pour le bien-être du peuple.*
