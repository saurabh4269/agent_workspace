# Manual simulation queue — Batch B2026-07-22

Private expressions live in `research/private/expressions.md` (gitignored) and the local artifact copy. This file is the **operator checklist** without publishing formulas.

## Execution order (do not mass-submit)

1. Sign in yourself at the platform (do not paste password into chat/agents).
2. Simulate **READY_PV** candidates first (C01–C04), one at a time.
3. For each run: copy settings exactly → paste private expression → Simulate → fill ledger row.
4. Only after baseline metrics exist: run the three predeclared variants (one change each).
5. Map fields for **FIELD_MAP_REQUIRED** (C05–C14) in Data Explorer before writing final expressions.
6. Build C15 only from two low-correlation survivors.
7. Robustness gate → approval report → wait for `APPROVE SUBMISSION <id>`.

## Queue

| Priority | Candidate | Status | Pack | Neut | Decay | Trunc | Region/Univ/Delay | Action |
|---:|---|---|---|---|---:|---:|---|---|
| 1 | C01.v0 | READY_PV | P1 | Subindustry | 6 | 0.01 | USA/TOP3000/D1 | Simulate baseline |
| 2 | C02.v0 | READY_PV | P2 | Industry | 10 | 0.01 | USA/TOP3000/D1 | Simulate baseline |
| 3 | C03.v0 | READY_PV | P2 | Industry | 10 | 0.01 | USA/TOP3000/D1 | Simulate baseline |
| 4 | C04.v0 | READY_PV | P3 | Industry | 12 | 0.01 | USA/TOP3000/D1 | Simulate baseline |
| 5 | C01.v1–v3 | PLANNED | P1 | see card | — | 0.01 | fixed neighbors | Only if C01.v0 not killed |
| 6 | C02.v1–v3 | PLANNED | P2 | see card | — | 0.01 | fixed neighbors | Only if C02.v0 not killed |
| 7 | C03.v1–v3 | PLANNED | P2 | see card | — | 0.01 | fixed neighbors | Only if C03.v0 not killed |
| 8 | C04.v1–v3 | PLANNED | P3 | see card | — | 0.01 | fixed neighbors | Only if C04.v0 not killed |
| 9 | C05–C07 | FIELD_MAP | P4 | Industry | 20 | 0.01 | USA/TOP3000/D1 | Map fundamentals first |
| 10 | C08–C09 | FIELD_MAP | P5 | Subindustry | 8 | 0.01 | USA/TOP3000/D1 | Map analyst/earnings |
| 11 | C10 | FIELD_MAP | P6 | Subindustry | 5 | 0.01 | USA/TOP3000/D1 | Map news novelty |
| 12 | C11 | FIELD_MAP | P7 | Market | 8 | 0.01 | USA/TOP3000/D1 | Map options; expect sparse |
| 13 | C12–C13 | FIELD_MAP | P8 | Industry | 15 | 0.01 | USA/TOP3000/D1 | Map SI/insider + lag |
| 14 | C14 | FIELD_MAP | P9 | Sector | 10 | 0.01 | USA/TOP3000/D1 | Map relationship graph |
| 15 | C15 | BLOCKED | P10 | Market | 10 | 0.01 | USA/TOP3000/D1 | Needs two survivors |

## Common settings to click (every READY_PV run)

- Instrument: Equity  
- Language: FASTEXPR  
- Pasteurization: On  
- Unit Handling: Verify  
- NaN Handling: Off  
- Visualization: On  
- Test Period: 1 year (do not retune on it)  
- Max Trade: Off  

## Decision codes for ledger

`SIMULATED` · `FAILED_SYNTAX` · `KILLED` · `PARKED` · `PROMOTED` · `ROBUST_OK` · `APPROVAL_QUEUE` · `SUBMIT_APPROVED` · `SUBMITTED` · `REJECTED_PLATFORM`

No row may be overwritten; append a new version instead.
