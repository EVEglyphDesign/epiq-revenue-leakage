# Epiq Revenue-Leakage Model

Consolidated model canon and the team spin surface for the Epiq revenue-leakage engagement.

**Author:** EVE Glyph Design · anchored to Tobias Polly, polly consulting e.U. (17 July 2026)
**Status:** Propose-only · public spin surface

## What this is — read first

This repository is a **fork off of EVE** — the EVE-side baseline. Its purpose is to
**clear up the requirements and stand up the initial demo blueprint**, from the EVE
side only. It is the **PMO access surface**: public, carrying the model canon, method,
and onboarding.

**Boundaries that are not negotiable:**

- **No proprietary Epiq Systems information lives here.** The client-confidential side
  is set up and governed by Tobias in a separate, walled-off surface; the team
  contributes to that through him. Nothing client-confidential crosses into this repo.
- **All Epiq data stays inside the Epiq environment.** The demo data lives in
  **Postgres, inside Epiq infrastructure** — none of Epiq's data is handled outside it.
- Once the demo is approved, it becomes a **repository build on Epiq infrastructure**.
  The EVE fork (baseline solution) can be copied back into the Epiq environment and
  work continues there.
- **We are not here to own the capital asset — that is Epiq's.**

## What's here

- **[DOCUMENT-A-corrections.md](./DOCUMENT-A-corrections.md)** — Tobias-derived
  foundation: the standing-narrative corrections + anchor table. Original PDF in
  [`foundation/`](./foundation/).
- **[DOCUMENT-B-architecture-extract.md](./DOCUMENT-B-architecture-extract.md)** —
  Tobias-derived architecture backbone: RFQ 125 mandate, the four-part engine, the
  reuse-vs-configured table, and the Router → Executor → Synthesizer reasoning path.
- **[MODEL-CANON.md](./MODEL-CANON.md)** — the single consolidated record of the
  revenue-leakage model. The base everyone spins from.
- **[index.html](./index.html)** — the onboarding surface. Step-by-step guide to get
  the team connected to this repo with their surface of choice.
- **`billing-twin/`** — (to be added by Matt) draft billing / Fury app data model and
  table structures, for twinning the billing operation through DataSphere.

## Onboarding

Live guide: **https://eveglyphdesign.github.io/epiq-revenue-leakage/**

New team members: open the guide, connect your surface, spin the model, push back.

---

*Pour le bien-être du peuple.*
