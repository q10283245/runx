---
name: agency-health
description: Grade one running agency from its ordered case projection and receipt-id-stub aggregates without issuing any intervention.
runx:
  category: ops
---

# Agency Health

This read-only skill assembles a health bundle for one running agency over a
bounded period. It appends nothing, sends nothing, executes nothing, moves no
money, grants no access, and consumes no effect.

## Inputs and output

Inputs are `data_source_ref`, pinned `store_id`, `agency_ref`, optional `period`
and `case_id`, and optional
`health_baseline{threshold_days_stuck,cap_pressure_pct,refusal_spike_rate}`.

Output is `decision{status,reason}`, where status is `ready`,
`needs_more_evidence`, or `needs_human`; `health_verdict{status,findings[]}`;
and `intervention_findings[]`. Every health finding contains a metric, observed
value, named norm, assessment, and grounding reference. Every intervention
names a target lane, reason, case id, turn reference, and ledger id-stub.

## Read model

Bind `registry:runx/data-store@0.1.2` to the supplied `store_id` and call
`read_projection` using the agency case as the domain key. Fold events strictly
in projection version order. Separately call the ledger read runner (C7) for
cross-run seal and refusal aggregates. Ledger evidence is audit-only and enters
the bundle only as receipt id-stubs; it must never replace the domain-keyed case
projection.

Grade `seal_rate`, `stuck_case_count`, `cap_usage_pct`, and
`escalation_backlog`. A supplied baseline may tighten declared norms but cannot
invent or widen charter authority. If a norm is absent from both the charter
snapshot and baseline, do not grade that metric.

## Refusals and escalation

- Refuse to grade signals not grounded in the ordered projection or a ledger
  receipt id-stub.
- Never invent a cap, threshold, case event, turn state, or aggregate.
- With no readable case events, seal `needs_more_evidence`, no graded findings,
  and no intervention.
- Route critical findings and any cap- or authority-widening remedy to the human
  ops lane as `needs_human`.

## Handoff

Interventions use dispatch-by-naming only. A routine tighten may name
`policy-author`; a refusal spike may name `improve-skill`. Findings carry no
ceiling or effect bound. Work begins only when a downstream driver or operator
starts that separate governed run. No payment rail consumes this output.
