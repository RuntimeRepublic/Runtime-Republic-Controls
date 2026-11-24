CONTROL 09 — Bill Registry

Version: 0.1
Date: 2026-11-24
Status: Draft
Project: Runtime Republic
Change: First draft from decisions James Hodges made on 2026-11-24 (with Claude, Opus 5.5). Card RRC-CWC-007.

---

# 1. Purpose

One registry of every bill, amendment and draft that Runtime Republic writes or tracks, so every tab, letter, essay and team packet points to the same bill by the same ID.

---

# 2. Core Principle

Link, never copy. The registry holds one row per bill and a link to its source. The bill's text, stage and version come from the source itself, and drafts keep their own labels ("not law," "not accepted").

---

# 3. Model / Rules

## 3.1 Where it lives
| Item | Location |
|---|---|
| The registry | `Registry/bills.json` in this repository |
| Our drafts | Their own repositories (Constitutional-Engineering, Legislative-Manager, AGCL-Control-Documents) |
| The public view | A page on the website that reads the registry (CONTROL 03) |

## 3.2 IDs
Level plus short name: `US-HR25`, `US-S59`, `KS-A`, `KS-ONE-HOUR`, `AGCL-AMD-002`. Level codes: `US`, two-letter state, `AGCL` for framework amendments. County and city prefixes are set when the first local bill is added (for example `KS-SG-` for Sedgwick County). An ID is never reused or renamed.

## 3.3 Which bills
| Kind | Rule | `tracked_because` |
|---|---|---|
| Ours | Every draft bill, amendment or framework change Runtime Republic writes | `ours` |
| Outside, tied to AGCL | Always listed | `agcl-point` |
| Outside, other | Listed once a member writes a letter about it | `member-tracked` |

## 3.4 Stage ladder (same words everywhere)
Idea → Definition → Understanding → Spec → Draft text → Filed → Committee → Passed → Law.
Outside bills enter at Filed. The stage is taken from the source; if the source and the registry disagree, the source wins and the registry is corrected.

## 3.5 Fields
`id, title, level, jurisdiction, ours, tracked_because, stage, source_status, source, source_commit (ours), summary, taxes, agcl, votes, last_checked`, plus optional `also` and `companion`.

## 3.6 Uses
| Where | How it uses the ID |
|---|---|
| Politics → Bills tab | Lists every bill with stage and last checked date |
| Paycheck and Property tax tabs | Replacement plans name the bill they follow |
| Officials, Contacts, Exploratory | Bills each office would vote on; bills asked about |
| Letters and reply cards | Every letter names a bill ID |
| Essays and lessons | May cite a bill ID |
| Team packet | Count of letters per bill ID only |
| Workshop (CONTROL 08) | Rule-by-rule scores attach to the bill ID |

## 3.7 Weekly refresh
At the Saturday close, each source is checked; any change in stage or version is recorded with its date and flagged to the team.

---

# 4. Edge Cases (must be tested)

| Case | Handling |
|---|---|
| A bill is renumbered in a new session | New row with a new ID; the old row's `companion` or `also` points to it |
| Companion bills (House and Senate) | One row each, linked by `companion` |
| A draft splits into two bills | Keep the original ID for one; add a new ID for the other; note both |
| Source unreachable | Keep the last stage; mark `source_status` "not reachable on <date>"; never guess |
| A member-tracked bill gets no letters for a year | Stays listed; marked inactive, never deleted |

---

# 5. Enforcement

The registry is checked as valid JSON with unique IDs at every change. A tab or letter that names a bill not in the registry is flagged.

---

# 6. Relationship to Other Controls

• CONTROL 03 — the public page that shows the registry.
• CONTROL 08 — workshop ratings attach to bill IDs.
• AGCL 00J — framework amendments (AGCL-AMD-NNN) keep their own adoption process; the registry only lists them.

---

# 7. Revision Policy

Changes require James Hodges's approval and a version bump with a one-line `Change:` note under the header.

END OF DOCUMENT
