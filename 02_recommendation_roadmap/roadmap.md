# Kloud Kart — 12-month roadmap

**North star:** one trusted Monday revenue number, produced away from the live shop, with customer-data handling that can be evidenced. Stock remains correct in the operational system.

| Quarter | What changes | What Nana can verify | Accountable lead |
|---|---|---|---|
| **Q1 — Protect and agree** | Hire Data Engineer first. Provision and isolate the approved replica/second server. Measure current Monday export impact. Agree revenue definition with Finance and Operations. Inventory marketing exports and access. | Monday reporting no longer runs on the live primary; a written revenue rule is signed by Nana and Finance; list of approved customer-data copies, owners and expiry dates exists; baseline slowdown and replication lag are recorded. | Data Engineer; Nana + Finance approve definition |
| **Q2 — Deliver the first trusted number** | Hire Analytics Engineer. Load orders/payments/refunds needed for the first reporting slice into a separate reporting store. Add scheduled daily load, checks, run log, failure alert and reconciliation. | Four consecutive Monday reports use the same definition; each report shows period, refresh time, source row counts and exceptions; Finance and Operations sign off variances or documented exclusions. | Analytics Engineer; Data Engineer operates pipeline |
| **Q3 — Extend carefully and control customer data** | Add agreed daily sales, order and fulfilment measures. Add export request/approval/expiry and deletion evidence workflow across known systems. Test restore and complaint-response tabletop. | Nana can see daily agreed measures; every approved marketing export has owner, purpose and expiry; a sample deletion request is traced end-to-end and evidence assembled within the internal target (30 days), leaving buffer before the case's 90-day deadline. | Analytics Engineer + Data Engineer; DPO/legal oversight |
| **Q4 — Prove scale and decide next investment** | Load-test at 15–20% growth assumption; review costs, data quality, privacy exceptions and stock boundaries. Decide whether any additional freshness or forecasting case has evidence to proceed. | Board receives cost-vs-budget report, pipeline reliability and freshness summary, reconciliation trend, deletion-process test result, and a go/no-go recommendation for year two. | Data Engineer + Analytics Engineer; Nana sponsors |

## Guardrails throughout the year
- Stock availability is read/written through the operational application and database; the reporting store is never used to authorize stock sales.
- Daily refresh is the service level for non-stock analytics. Stock freshness is governed separately by application transaction design.
- Alert on failed loads, late data, unexpected row-count changes and replica lag.
- Do not export identifiable customer data into the reporting store unless a documented purpose and access need require it; aggregate or pseudonymise where practical.
- Quarterly access review, backup-restore test and cost review.

## Hiring order and first 90 days
**1. Data Engineer (start Q1).** Days 1–30: map MySQL tables/flows, baseline query impact, inspect replication support, inventory exports and document access. Days 31–60: provision isolated replica/reporting host, configure secure credentials, backup, monitoring and a read-only extraction path. Days 61–90: deliver first repeatable load in a test environment, run failure/recovery and replica-lag tests, document runbook; no production cutover until acceptance tests pass.

**2. Analytics Engineer (start Q2; recruit in Q1).** Days 1–30: facilitate Finance/Operations workshop, define revenue inclusions/exclusions and KPI owners, profile sample outputs. Days 31–60: implement version-controlled transformations and automated reconciliation tests for the Monday revenue slice. Days 61–90: publish a controlled report, train Nana/Finance, capture sign-off and document known exceptions.

## Cost and capacity position
Planning allowance: US$300–800/month for isolated compute, storage, backups and monitoring; US$2,000–6,000 one-time setup/migration. Validate with quotes and a representative load test. Hiring costs are separate and depend on local compensation. No enterprise warehouse subscription is assumed.
