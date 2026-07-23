# Revenue Leakage on the Epiq Finance Workstream

## Technical corrections and standing-narrative update

| | |
|---|---|
| **Client** | Epiq Systems — internal, existing engagement |
| **Workstream** | Finance — SAP S/4 + DataSphere edit-history reasoning |
| **Author** | EVE Glyph Design |
| **Anchor** | Tobias Polly, polly consulting e.U. — Discovery Business Brief (17 July 2026) |
| **Date** | 18 July 2026 |
| **Reference** | EVE-EPIQ-LEAK-CORR-2026-07-18 |
| **Status** | Propose-only — no scope creep, no relationship risk |

---

## 1 · Purpose

Tobias's Discovery Business Brief already names the capability cleanly for a
front-office reader: revenue leaks quietly through post-commitment edits; the
platform surfaces which records, which people, which fields, in plain language in
Teams, replayable end-to-end. That framing lands.

This document does one thing. It aligns Tobias's client-facing narrative with what is
actually live in the Epiq tenant today, so the story we tell inside Epiq matches the
boxes running in `epiq-financial-reports`. It introduces no new definitions and no
new scope. It is a technical alignment, not a redirection.

## 2 · What is already live, in Epiq's own terms

The engine described in Polly's Discovery Business Brief is running against SAP
DataSphere space **QM_SAPAI001**, reading ACDOCA edit history through the
**BFI_JournalSummary_R01** view. Delivery is the Teams tab already registered in
Epiq's tenant. Three question configurations are live:

- `ebitda_variance_analysis`
- `monthly_management_report`
- `postage_margin`

None of these is generic. They are the actual questions Epiq finance asks. The
Revenue Leakage framing is the umbrella over those three — not a replacement for
them, and not an additional configuration to fund.

## 3 · Corrections to the standing narrative

The Tobias brief speaks in the vendor-generic register that is right for a first-time
reader. The version we tell inside Epiq — to Adam Nigg's team, to finance leadership,
to a security reviewer already inside the tenant — should carry three technical
corrections that make the same story more precise.

| In the Tobias brief | For internal Epiq telling |
|---------------------|---------------------------|
| "Your live systems" | Specifically: SAP DataSphere space QM_SAPAI001, reading ACDOCA through BFI_JournalSummary_R01. |
| "AI reasoning engine" | LangGraph Router → Executor → Synthesizer, hosted in Azure Container Apps as agent-api, Azure AI Foundry model in-tenant. |
| "Answer in Microsoft Teams" | The registered Teams tab already stood up on the Epiq side; no new bot to approve. |
| "Every answer is replayable" | Langfuse end-to-end trace, retained per the audit policy already agreed for this workstream. |
| "One engine serves many uses" | Same LangGraph agent behind the three live configs; Revenue Leakage is a fourth lens on the same edit-history feed, not a fourth deployment. |

*Each entry is the concrete anchor for a line in Tobias's brief.*

## 4 · What Revenue Leakage adds — and what it does not

**Adds.** A ranked view of post-commitment edits on records already covered by the
three live configurations — which orders were edited most, which editors touched
them, which fields concentrate the changes, narrated in a sentence the finance reader
can act on. Same source adapter, same reasoning agent, same Teams surface, same
Langfuse trace.

**Does not add.** No new SAP extraction, no new DataSphere space, no new Teams
registration, no new model deployment, no new security review. The lens is a
configuration on the existing engine.

## 5 · The Analysis-for-Office corollary

The Epiq workstream retired the Analysis-for-Office dependency in two weeks with no
incremental licensing. That result belongs in the Revenue Leakage narrative as a
lived example of the retargeting economics Tobias describes in section 3 of the brief:

> The engine already exists. Pointing it at a Discovery system is a configuration
> change, not a new platform to design, buy, and de-risk. — Polly, Discovery Business Brief

AO was pointed at; AO was retired. The finance reader who wants a proof point already
has one inside the same tenant.

## 6 · The decision this asks for

None, from the client. This is an internal alignment so the next time Tobias's brief
circulates inside Epiq, the reader can find the sentence in the brief and the object
in the tenant without leaving the page. It preserves Tobias's language and Tobias's
authorship; it adds the internal reference marks.

---

### Proposal footer

**Mode.** Propose-only.

**Anchor to Tobias.** All framing preserved from Polly's Discovery Business Brief.
Author attribution unchanged. This is corrections to the client narrative, not a
rewrite of Tobias's work.

**Canon.** TOBIAS@CANON-NAMED-ENTITY-TOBIAS-00 (_pending-counsel). HARM-CLAUSE §3
propose-do-not-impose; §4 never-lose-the-archive.

© 2026 Dany Theriault. EVE "digital stem cell" glyph and glyph-based design
principles — all rights reserved. Stewardship of rights of use and assignment for
large public and institutional usage rests with the Pacific Utilities Design Council.
Published as a time-stamped record of authorship and intent.

*Pour le bien-être du peuple.*
