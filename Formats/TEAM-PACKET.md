# Team Packet Format

Version: 0.1 · Date: 2026-11-18 · Status: Draft · Governed by: CONTROL 07 §3.7

A team packet is one member's weekly report to their team. The member's **Personal Finance project** writes it at Saturday close, the member reads it, and the member pushes it to the team repository by pull request.

## Where it goes

`packets/<YYYY>-W<ww>/<CallSign>.csv` in the team repository, one file per member per week. Example: `packets/2026-W48/Longbow.csv`. Weeks follow the ISO calendar (Monday to Sunday).

## Columns (one header row, one data row)

| Column | Allowed values | Meaning |
|---|---|---|
| `week` | `2026-W48` | ISO week |
| `call_sign` | Letters, digits, `-` | The member's call sign. Never a real name or initials |
| `flags` | Up to two flag IDs, separated by `;` | From the shared flag log (`RuntimeRepublic.github.io/images/flags/FLAG-LOG.csv`). The US flag is shown for every team and is not listed |
| `closed_week` | `yes` or `no` | Did the member close this week? |
| `ce1_status` … `ce5_status` | `E` earned · `W` working · `N` not yet | Close Encounter level status |
| `ce1_impact` … `ce5_impact` | `1` to `5`, blank unless earned | Impact rating (version 1 table in the Close Encounter Challenge) |
| `ce_reviewed_by` | A call sign, or blank | Who checked the evidence for any newly earned level or rating |
| `governments_counted` | Whole number, or blank | Governments that take the member's money |
| `budget_1` … `budget_4` | `Federal`, `State`, `Local`, `Family` | Who gets paid first, first to last. Blank until ranked |

## Never in a packet

Names, initials, addresses, employers, account numbers, dollar amounts, or any single bill or receipt. A packet that has one is not merged (CONTROL 07 §4).

## Example (sample values)

```
week,call_sign,flags,closed_week,ce1_status,ce1_impact,ce2_status,ce2_impact,ce3_status,ce3_impact,ce4_status,ce4_impact,ce5_status,ce5_impact,ce_reviewed_by,governments_counted,budget_1,budget_2,budget_3,budget_4
2026-W48,Longbow,KS;ICT,yes,E,4,E,2,E,3,W,,N,,Prairie,9,Federal,State,Local,Family
```

## Team rollup

After the packets for a week are merged, the team updates one row in `data/group-counts.csv` (totals only; see the team repository's `DATA-RULES.md`). The public dashboard and the `team:` code read that row.
