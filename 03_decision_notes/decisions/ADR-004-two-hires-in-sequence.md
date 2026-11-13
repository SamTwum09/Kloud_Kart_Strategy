# ADR-004: Hire a Data Engineer first and an Analytics Engineer second

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Nana Adjei / board

## Context
Only two data hires are funded. One developer knows PHP/MySQL; nobody has professionally operated a warehouse or written Python. The immediate risk is unsafe extraction; the first business outcome is trusted revenue.

## Decision
Hire a Data Engineer first to isolate and operate data movement; recruit an Analytics Engineer in parallel but onboard second to establish definitions, tests and reporting.

## Alternatives considered
### Alternative A: Hire a Data Scientist
- **How it would work:** Start with forecasting and predictive models.
- **Why it is attractive:** Directly responds to the ML wish list and may impress investors.
- **Why rejected:** No trusted training history, defined forecast use case or data platform; predictions would inherit current inconsistencies.

### Alternative B: Hire two generalist analysts/BI developers
- **How it would work:** Build dashboards and spreadsheet replacements first.
- **Why it is attractive:** Stakeholders see visible reports quickly.
- **Why rejected:** Does not provide the specialist ownership needed to move workload safely off the production database and operate reliable loads.

## Consequences
- **What this buys:** Clear technical ownership followed by business metric ownership, within the two-hire limit.
- **What this costs:** Revenue certification may arrive later than a dashboard-only approach; the PHP developer remains a key application partner.
- **What it costs the client if I am wrong:** Hiring order could leave business users waiting; a weak hire could create a single-person dependency.
- **What would make me revisit this:** Existing staff demonstrate production data-pipeline competence or an urgent, independently funded privacy/security gap requires a different role.

## What this survives
If growth accelerates, the engineer establishes the safe data boundary and repeatable operations; if board pressure shifts to forecasting, the analytics engineer can first validate history and definitions. The plan does not silently add a third hire.
