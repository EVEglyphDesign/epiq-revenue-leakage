# Discovery Architecture Extract — Revenue Leakage Reference Model

**Anchor:** Tobias Polly, polly consulting e.U. — Discovery Architecture Extract (17 July 2026)
**Author:** EVE Glyph Design
**Status:** Propose-only

> Foundation companion to [Document A](./DOCUMENT-A-corrections.md). This extract is
> the architecture backbone — the load-bearing parts of the engine, source-system
> details stripped out, showing how the same engine points at Discovery's own systems.

---

## 1 · The mandate, and what it now does

The system in this briefing was commissioned in **November 2025 under a single, narrow
mandate (RFQ 125)**: build a **zero-data-leakage AI agent** that reads the *edit
history* of enterprise transactions, tells a person in plain language which records
are being changed and by whom, and does it inside Microsoft Teams — all within a
locked-down network boundary so that no sensitive data leaves the customer's control.
That agent is live today. This extract strips the original design back to its
load-bearing parts, drops the details specific to any one source system, and shows how
the same engine points at Discovery's own systems.

The first thing the agent was pointed at was **booked orders**. Every time an order is
edited after it is committed — a price nudged down, a quantity trimmed, a discount
reopened — the change is recorded but rarely read. Aggregated across thousands of
records, those quiet edits are where booked revenue quietly leaks away. We now package
this capability as the **Revenue Leakage Model**: it ranks the records, editors, and
fields where post-commitment changes are eroding value, and narrates the pattern so a
non-technical reader can act on it. The finance workstream is the live proof; the
mechanism is general to *any* system where records are edited after a commitment is
made.

**What Discovery leaves with.** The engine already runs in production on one
workstream. Pointing it at a Discovery data source is a **configuration change, not a
new build** — the reasoning, the audit trail, the Teams delivery, and the security
posture are reused unchanged. That is the fast, low-risk path to a measurable P&L
result.

In one paragraph: content enters through a source adapter, a bounded AI agent reasons
over it and answers the user in Teams, and every answer is recorded end-to-end so a
human can replay exactly how it was produced. The agent does not change between use
cases — only the source in front of it and the questions asked of it do.

## 2 · The architecture, stripped to four parts

*SAP · custom systems · data lake*

```
  1. Source            2. Reasoning            3. Delivery
  adapter       →      LangGraph agent    →    Microsoft Teams
  edit history in      plan → retrieve         answer + cards
                       → narrate
                            ⋮
                   4. Observability — Langfuse records every
                   step; any answer can be replayed end-to-end

            (all inside a secure network boundary)
```

Four parts, each replaceable on its own:

- **Source adapter** — crosses the boundary from the customer's system into the
  platform and presents edit history in a single, uniform shape. The source behind it
  is interchangeable (Section 5).
- **Reasoning** — a bounded AI agent that plans what to fetch, fetches it, and writes
  the answer in plain language. This is the part that is reused unchanged across every
  use case (Section 3).
- **Delivery** — Microsoft Teams. Users ask in plain English and get a written answer
  plus a structured card; no new tool to learn, no SQL, no dashboard.
- **Observability** — Langfuse sits underneath everything and records each step, so
  any answer can be reconstructed and defended after the fact.

Standing the platform up for a new source reuses the top three parts wholesale; only
the source, the storage, and the model deployment are set per engagement.

| Component | For Discovery | What that involves |
|-----------|:-------------:|--------------------|
| Reasoning agent | **Live** | Reused unchanged — the same bounded agent |
| Teams delivery | **Live** | Same bot, cards, and streaming |
| Audit trail (Langfuse) | **Live** | Same end-to-end replay of every answer |
| Security boundary | **Live** | Same closed-network, customer-tenant posture |
| Source adapter | **Configured** | Point it at the chosen live Discovery system |
| Compute layer | **Configured** | Stand up the ephemeral DuckDB / graph layer |
| Model | **Configured** | Confirm the model deployment in-tenant |

*Table 1: Four parts are reused as-is; three are configured. None is a new build.*

## 3 · How it reasons, and why every answer is auditable

The agent follows a fixed three-step path rather than being left to improvise. That
choice is deliberate: a predictable path is cheaper to run, easier to budget, and —
critically for regulated data — fully auditable.

```
  Router                  Executor                Synthesizer
  reads the question,  →   fetches the data    →   turns results into
  plans the steps         the plan calls for       a plain-language answer
```

Three steps, three model calls, one answer — bounded every time. A worked example on
the Revenue Leakage workstream:

> **ANALYST ASKS**
> Where are we leaking the most revenue on last quarter's orders?
>
> **ANSWER**
> Order 4500012345 was edited 12 times after booking — the most this quarter. Eight
> of those changes reduced the net price, all by two editors. Across the quarter,
> discount and net-price fields account for 71% of post-booking edits, concentrated in
> three accounts. Those three are where booked revenue is leaking fastest.

Two properties make this safe to put in front of sensitive data:

- **Bounded and auditable.** The plan and every data lookup are stored with the
  answer. There is no open-ended loop of tool calls, so cost and behaviour are
  predictable and reviewable.
- **Zero data leakage, fully replayable.** The agent runs inside a closed network
  boundary, and Langfuse records each step end-to-end. When someone asks "how do I
  know the AI didn't make this up?", the honest answer is: replay it and see.

---

> Note: any further sections beyond §3 continue in the full extract. Add them here as
> they are brought in, so this file mirrors Tobias's complete architecture doc.

© 2026 Dany Theriault. EVE "digital stem cell" glyph and glyph-based design
principles — all rights reserved. Stewardship of rights of use and assignment for
large public and institutional usage rests with the Pacific Utilities Design Council.

*Pour le bien-être du peuple.*
