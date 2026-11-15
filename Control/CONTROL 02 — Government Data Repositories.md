CONTROL 02 — Government Data Repositories

Version: 0.1
Date: 2026-11-15
Status: Draft
Project: Runtime Republic

---

# 1. Purpose

Defines the shared, public repositories of government facts that members' AI assistants read to estimate taxes and rank the four budgets.

---

# 2. Core Principle

Every fact has an official source and a date. Blank is better than a guess.

---

# 3. Rules

1. One repository per government: Gov-US, Gov-<state> (Gov-KS), Gov-<state>-<county or parish> (Gov-KS-Sedgwick-County). Cities are recorded in their county's repository.
2. A repository is created when its first member arrives, not before.
3. Each repository holds five files:

| File | Holds |
|---|---|
| data/tax-rates.csv | Tax rates and fees: id, level, jurisdiction, tax, base, rate, applies_to, recipient, effective_from, source_title, source_url, verified_on, status |
| data/offices.csv | Offices, officeholders, terms and official contacts |
| data/deadlines.csv | Election, registration and candidate-filing deadlines |
| data/debt.csv | Government debt with as-of dates |
| data/recipients.csv | Funds and agencies that receive the money |

4. Data rules (DATA-RULES.md in each repository):
   a. Every row cites an official source with its link.
   b. `verified_on` is the date the source was checked; `status` is V (verified) or E (estimate or unverified).
   c. History is never deleted. A changed rate gets a new row with a new `effective_from`.
   d. Changes come by pull request; a maintainer checks the source before merging.
   e. Public facts only. No personal data, ever.
5. Members' tax records point to a rate by its id (for example, KS-FUEL-GAS) so every estimate is traceable.
6. The data is public and free for any app developer to use (CONTROL 06).

---

# 4. Edge Cases

| Case | Handling |
|---|---|
| A rate an AI needs is missing | The AI estimates it, labels it [E], and suggests a pull request with a source. |
| A fee may be paused (for example, Kansas environmental assurance fee) | Keep status E until an official source confirms it is being collected. |
| Two sources disagree | Use the statute or the agency's official page, and note the other source. |

---

# 5. Relationship to Other Controls

• CONTROL 01 — Organization, Ownership and Identity (`level` values)
• CONTROL 06 — Commercial Separation and App Developers

---

# 6. Revision Policy

Changes require the founder's approval and a version bump with a one-line `Change:` note under the header.

END OF DOCUMENT
