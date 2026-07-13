# Renewal Runner Standing Agency Case Trail

This is a redacted real operations trail for the recurring two-week effort to
select, implement, verify, and deliver compliant open-source bounties toward USD
200. The case contains no credentials, private counterparties, wallet actions,
or spending authority.

## Mandate and roster

- Case: `case:two-week-200-bounty-ops`
- Agency: `agency:renewal-runner`
- Mandate: advance compliant bounty work toward USD 200 without spending money,
  signing wallet transactions, exposing credentials, or widening authority.
- Researcher: `agency-health`, scopes `public-read` and `bounty-triage`.
- Implementer: `issue-to-pr`, scopes `workspace-write` and `github-draft-pr`.
- Verifier: `receipt-auditor`, scopes `receipt-read` and `public-evidence`.
- Limits: 12 turns, USD 0 spend, one active claim.

## Governed turns

1. Turn 1 dispatched the fixed researcher for a read-only audit. It found the
   global registry outage and separated it from package correctness. Receipt:
   `runx:receipt:sha256:c89825c9d271389028367a8162ee9ebce0ff9739e4a114fe58b57ac2a52dd1b7`.
2. Turn 2 folded the research result and stopped at `awaiting_approval`. The
   agency refused to republish blindly, substitute a private URL, or bypass the
   hosted harness. Receipt:
   `runx:receipt:sha256:d8ea964534a047b438dd0b44ee3430b76757d82089b80b67e83e9f4f070dbe1a`.
3. Turn 3 recorded the human-ops resolution: wait for the public registry,
   retain public-proof requirements, and perform only evidence verification.
   It dispatched the fixed verifier. Receipt:
   `runx:receipt:sha256:f4878a95993c1b5faeb2e70f20c71c1ccd22fc0d0cda1952b9d005d7e7ea9042`.

All three receipts pass `runx verify` for digest, content address, and Ed25519
signature using the public verification key recorded in `verification.json`.

## What governance changed

- The consequence gate prevented an expedient but invalid workaround: a private
  artifact could not replace the required public registry page.
- The fixed roster prevented the agency from inventing a deployment or payment
  actor. After resolution it could dispatch only the verifier within the
  declared receipt-read/public-evidence scope.
- The sealed fold made the outage finding, gate, resolution, and next dispatch
  auditable in order instead of relying on a loose status narrative.
