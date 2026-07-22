# Live UI runbook (manual e2e)

You own authentication. This agent will not accept or reuse passwords.

## A. Sign-in (you)

1. Open https://platform.worldquantbrain.com/
2. Enter credentials yourself.
3. If the password was previously pasted into chat, **rotate it** first.
4. Do not send cookies, tokens, or session dumps back to the agent.

## B. Capability snapshot (5 minutes)

Record into `research/inventory_live.md` (create when signed in):

- User vs consultant
- IQC 2026 status (none / Stage 2 / Stage 3)
- Regions, universes, delays visible
- Dataset categories visible (PV, fundamental, analyst, news, options, SI, insider, relationship, model)
- Whether Python API appears anywhere in your account
- Any daily simulation or submission quota text
- Live Check Submission threshold labels (do not hard-code community cutoffs)

## C. Simulate READY_PV (C01–C04)

For each candidate version:

1. Simulate → settings from `02_manual_sim_queue.md`
2. Paste expression from `research/private/expressions.md`
3. Run
4. Append one row to `03_experiment_ledger.csv` with all metrics returned (never invent numbers)
5. Apply kill criteria from the hypothesis card before variants

## D. Robustness (only PROMOTED baselines)

Neighbor lookback · adjacent neutralization · truncation 0.01/0.02 · smaller liquid universe · year table · test period once · self-corr vs your submitted book.

## E. Field map (C05–C14)

In Data Explorer, for each placeholder capture: field ID, description, type, unit, frequency, lag, coverage, missing meaning, allowed region/delay. Reject unclear timing.

## F. Approval / submit

1. Fill approval report template in `05_approval_template.md`
2. Stop
3. Submit **only** after you send `APPROVE SUBMISSION <candidate_id>` for that exact version
4. One approval → one submit → verify status → ledger receipt

## Hard stops

- Biometrics / CAPTCHA / ambiguous submit response → stop and ask a human
- API absent → stay on this manual path
- Temptation to “just submit the best Sharpe” → ignore without approval tag
