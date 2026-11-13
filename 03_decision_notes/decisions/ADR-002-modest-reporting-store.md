# ADR-002: Start with a modest relational reporting store

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Nana Adjei; Data Engineer accountable for implementation

## Context
Current data is structured operational MySQL data. The first deliverable is a trusted Monday revenue figure; the team has one PHP/MySQL developer and no professional Python/warehouse operator.

## Decision
Load only the required, approved data into a separate relational reporting database on the approved second server initially; expand by business outcome, not by platform fashion.

## Alternatives considered
### Alternative A: Buy a cloud warehouse immediately
- **How it would work:** Load all source data into a managed cloud warehouse and build reports there.
- **Why it is attractive:** Managed scaling, familiar vendor ecosystem and less database administration.
- **Why rejected:** No quote or requirements justify recurring platform spend; it does not solve conflicting definitions or privacy controls by itself. Revisit if scale, resilience or team capability makes the economics favourable.

### Alternative B: Build a lakehouse
- **How it would work:** Store raw files and structured tables in a lakehouse architecture.
- **Why it is attractive:** Flexible for varied data and future ML.
- **Why rejected:** No unstructured/multi-format requirement is stated; it adds operating concepts and skills before the first business number is trusted.

## Consequences
- **What this buys:** Low complexity, SQL-based skills transfer and a clear boundary from production.
- **What this costs:** The team owns patching, backups, capacity and recovery unless a managed host is selected.
- **What it costs the client if I am wrong:** A later migration may be needed if volume or concurrency exceeds the modest store.
- **What would make me revisit this:** Measured workload, availability, geographic recovery or concurrency needs exceed the operating capacity of the initial store.

## What this survives
15–20% annual growth can be tested with measured capacity and cost. If it outgrows the store, the clean source-to-reporting boundary and documented definitions make a later managed-warehouse move possible without changing the business meaning of the metrics.
