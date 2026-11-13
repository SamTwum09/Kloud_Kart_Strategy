# ADR-003: Use daily batch for analytics and keep stock transactional

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Nana Adjei; Operations owns stock policy

## Context
The wish list asks for real-time dashboards, but the brief states stock counts cannot go stale and everything else may refresh daily. Overselling is the stated stock risk.

## Decision
Use scheduled daily batch refresh for non-stock analytics; keep stock availability authoritative in the live operational transaction flow and do not serve stock decisions from the delayed reporting store.

## Alternatives considered
### Alternative A: Stream every event and dashboard metric
- **How it would work:** Build continuous event processing and near-real-time dashboards for all domains.
- **Why it is attractive:** Impressive investor demonstration and lower reporting delay.
- **Why rejected:** No business requirement for real-time sales/finance dashboards; adds operational complexity and monitoring burden to a two-hire team.

### Alternative B: Refresh inventory from the reporting store every few minutes
- **How it would work:** Treat the analytical copy as the source for stock dashboards and possibly availability.
- **Why it is attractive:** One place for all metrics.
- **Why rejected:** Replication and batch delays make it unsafe as the stock authority and can enable overselling.

## Consequences
- **What this buys:** Simple, predictable reporting and protects the inventory correctness boundary.
- **What this costs:** Non-stock dashboards are not instant; inventory requires application-level correctness and separate testing.
- **What it costs the client if I am wrong:** A missed real-time use case could delay action; if stock architecture is already flawed, this plan does not repair it.
- **What would make me revisit this:** A quantified decision requiring sub-daily non-stock data, or evidence of stock oversells caused by transaction design rather than reporting.

## What this survives
Investor pressure for real-time views does not change the stock authority or justify streaming all metrics. A narrowly scoped event feed can be assessed later against a named decision, measurable latency target and operating cost.
