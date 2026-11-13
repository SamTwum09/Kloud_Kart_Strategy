# ADR-001: Move analytical reads off the live primary

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Nana Adjei (business sponsor), Data Engineer (Samuel Twum)

## Context
The website and reporting share one MySQL instance; Monday exports have twice slowed the live site. A second server or read replica is pre-approved.

## Decision
Use the pre-approved separate server/read replica as the source for analytical extraction, and prohibit routine reporting queries on the production primary.

## Alternatives considered
### Alternative A: Continue exporting from the primary
- **How it would work:** Keep current CSV workflow and tune export queries.
- **Why it is attractive:** Lowest initial infrastructure change.
- **Why rejected:** It preserves the confirmed customer-facing risk and does not fix repeatability or ownership.

### Alternative B: Move all operations to a new managed database immediately
- **How it would work:** Migrate the live application and reporting to a managed database platform.
- **Why it is attractive:** Potentially stronger managed operations and future scale.
- **Why rejected:** Higher migration risk, cost and skills burden than the immediate problem warrants; no evidence that the current 40 GB database requires a full replacement.

## Consequences
- **What this buys:** Customer traffic is separated from routine analytical load; safer reporting experimentation.
- **What this costs:** Second-server operation, replication monitoring, backups and some replication lag.
- **What it costs the client if I am wrong:** Additional infrastructure spend without adequate isolation, or stale/incomplete reports if lag is ignored.
- **What would make me revisit this:** Replica cannot sustain extract load, lag breaches an agreed threshold, or growth/load tests show inadequate capacity.

## What this survives
If Monday exports grow, they run against the replica, not the customer-facing primary. If investor pressure for instant dashboards rises, the boundary still protects the shop; faster delivery requires a separately justified freshness design, not permission to query production.
