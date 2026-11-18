CONTROL 07 — Member Onboarding

Version: 0.2
Date: 2026-11-18
Status: Draft
Project: Runtime Republic
Change: v0.2 adds two AI projects per member (§3.6), the team packet (§3.7) and the `team:` status code (§3.8).

---

# 1. Purpose

Defines how a new member joins a team, and the onboarding smoke test that proves the AI → GitHub → AI loop works for every member each time someone joins.

This document is temporary here. It moves to Lean-Civics/Lean-Civics-Control-Documents once that repository is available, and this copy is then retired with a pointer to the new home.

---

# 2. Core Principle

A team runs on one loop: a member's AI reads the team's GitHub repository, and the member writes back to it. Every new member is a test of that loop for the whole team.

---

# 3. Rules

## 3.1 Requirements for every member

1. A free GitHub account, added to the team repository.
2. An AI account that can read a GitHub repository. Claude, free or paid, is recommended.
3. The AI connected to GitHub. Claude: Customize > Connectors > GitHub Integration > Connect.

## 3.2 Onboarding steps

| Step | Who | Action |
|---|---|---|
| 1 | Team lead | Adds `members/<name>.md` to the team repository |
| 2 | Team lead | Opens a GitHub issue titled `ONBOARD: <name>` |
| 3 | New member | Has their AI read the team README, then posts `onboarded` on the issue |
| 4 | Every current member | Types `ack: <name>` to their AI (§3.4) |
| 5 | Every current member | Posts the acknowledgment line on the `ONBOARD: <name>` issue |
| 6 | Team lead | Closes the issue when all members have acknowledged or the time limit ends |

## 3.3 Smoke test: pass or fail

| Result | Condition | Handling |
|---|---|---|
| PASS | Every current member acknowledges within 72 hours | Close the issue |
| PARTIAL | One or more members miss the 72 hours | New member is onboarded; each member who missed it gets a setup check |
| FAIL | The new member cannot complete Step 3 | Fix the new member's setup before any work is assigned |

A missed acknowledgment means a member's loop is broken (no AI, no GitHub, or lost access). It is a setup problem, not a discipline problem.

## 3.4 Cheat code: `ack:`

A fully onboarded member types:

```
ack: <new member name>
```

The AI reads `members/<name>.md` and writes one line:

```
ACK <new member> | <member name> | <date> | read members/<name>.md | loop OK
```

A paid account may post the line itself. A free account gives the line to the member, who pastes it on the issue at github.com. Both count as PASS.

## 3.5 Paid and free Claude accounts

| Capability | Free Claude | Paid Claude (Pro or higher) |
|---|---|---|
| Connect GitHub | Yes | Yes |
| Read files in the team repository | Yes | Yes |
| Read issues, pull requests and commit history | No | Yes, through Claude Code in the cloud |
| Write the acknowledgment line | Yes | Yes |
| Post to GitHub without the member | No (member pastes it) | Yes |
| Commit files and open pull requests | No | Yes |
| Pass the onboarding smoke test | Yes, with one manual paste | Yes |

Paying is never required to be a member. Other AIs may be used if they can read a GitHub repository. ChatGPT's GitHub connector appears to require a paid plan (UNVERIFIED).

Sources: Claude GitHub integration, https://claude.com/docs/connectors/github ; Claude Code in the cloud, https://code.claude.com/docs/en/web-quickstart

## 3.6 Two AI projects per member

Every member keeps two separate AI projects, so the AI that can see their money never talks to the team.

| | Personal Finance project | Team project |
|---|---|---|
| Connected repositories | The member's private `Personal-Finance` and `master-plan` | The team repository, plus the public Gov data and control repositories |
| Can see | Pay stubs, bills, receipts, the budget | Counts, wins and team issues only |
| Codes | `pfmlr`, `Bill:`, `Paystub:`, `Close week:`, `Status:` | `team:`, `ack:`, `@` |
| Output seen by | The member only | The team, and the public through the dashboard |

The Team project is never connected to a private finance repository.

## 3.7 The team packet

At Saturday close, the Personal Finance project writes a team packet in the member's private repository. It holds only: call sign, CE levels earned, impact ratings, number of governments counted, and budget order (who gets paid first). No names, accounts, employers or dollar amounts.

The member reads the packet, then pushes it to the team repository by pull request. That pull request is the only crossing point between private and team data, and the member carries it across.

## 3.8 Cheat code: `team:`

In the Team project, a member types:

```
team:
```

The AI reads `Runtime-Republic-Controls/Registry/teams.csv` and the team's `data/group-counts.csv`, `MEMBERS.md` and open issues, and shows one screen:

1. Team name, level and status from the registry
2. Members, and how many closed the week
3. CE1 to CE5: how many earned each level, and the average impact rating
4. Family's place in the team's budget order
5. Open `ONBOARD:` issues, and members who have not posted their `ack:` line
6. The team's next step

`team: <team name>` shows another team's public counts only (items 1 to 4).

---

# 4. Edge Cases (must be tested)

| Case | Handling |
|---|---|
| A team has only the team lead | The team lead acknowledges; the test still runs |
| Two members join the same week | One issue per new member; each runs on its own |
| A member uses an AI with no GitHub access | Member reads the file on github.com and writes the line by hand; flag for a setup check |
| A member repeatedly misses acknowledgments | Team lead checks the member's setup and asks whether the member is still active |
| The new member has no AI account yet | Onboarding pauses at Step 3 until one is set up |
| A member's AI plan allows only one project | The one project is the Personal Finance project; the member reads team files on github.com until a second project is available |
| The Team project is connected to a private finance repository | Disconnect it before any team work; report to the team lead |
| A team packet holds a name, account, employer or dollar amount | The pull request is not merged; the member fixes the packet |

---

# 5. Enforcement

Team leads run the steps. The `ONBOARD: <name>` issue is the record. A failed smoke test is reported to the team's sponsor.

---

# 6. Relationship to Other Controls

• CONTROL 01 — Organization, Ownership and Identity
• CONTROL 05 — Qualified Organizations
• AGCL 00L — Smoke Test and Citizen Trigger (draft): smoke tests of government; this document applies the same pass/fail idea to members
• Lean-Civics-Control-Documents: future home of this document

---

# 7. Revision Policy

Changes require the founder's approval and a version bump with a one-line `Change:` note under the header.

END OF DOCUMENT
