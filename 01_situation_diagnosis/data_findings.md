# Data findings — Kloud Kart

## Summary (Problem Overview)
Kloud Kart's primary failure is not that it lacks a warehouse. It lacks a controlled path from operational records to business decisions. The same production MySQL instance serves customers and reporting; people manually export and independently calculate numbers; customer copies are uncontrolled. This creates three board-level exposures: trading interruption, decisions made from conflicting numbers, and inability to demonstrate responsible handling or deletion of personal data.

The brief provides no row-level dataset, schema, sample CSVs, query definitions, export logs or privacy register. Consequently, no actual duplicate rate, revenue delta, deletion backlog, query duration or data-loss rate can be measured here. The findings below rank known control failures and the likely root causes; they are not fabricated test results.

## Reconciliation

| Stage | Rows | Delta | Reason |
|---|---:|---:|---|
| Operational MySQL source | Not supplied | — | No extract or query access provided |
| Nana's Monday CSV / spreadsheet | Not supplied | Not measurable | Export and calculation rules not supplied |
| Finance spreadsheet | Not supplied | Not measurable | Independent definitions and formulas not supplied |
| Marketing customer list | Approx. 300,000 people | Not measurable | Copy count and suppression/deletion process unknown |

**Decision:** do not claim that either department's revenue is correct until Finance and Operations approve one written definition and the same sample period is recomputed from source records.

## Findings, ranked by risk

### F-01: Reporting competes with customer transactions — Severity: Critical
- **What it is:** Analytical exports run against the same MySQL database and machine that serve the live shop.
- **How I detected it:** Case evidence: orders, inventory and customer accounts share one approximately 40 GB MySQL database on the website's box; two Monday exports slowed the live site.
- **Scale:** About 4,000 orders/day; Monday exports involve a few hundred thousand rows.
- **Effect on the client's number:** Reports may be incomplete if interrupted or may use inconsistent extraction windows; the confirmed direct impact is degraded customer experience, not a measured revenue loss.
- **What I did about it:** Recommend a separately hosted read replica or second server as the reporting source; schedule bounded extracts away from peak periods; keep analytical queries off the primary.
- **Residual risk:** Replication lag, replica resource exhaustion, accidental reporting against primary, and failover/configuration mistakes. Monitor lag and query load; test replica isolation before use.

### F-02: Revenue has no shared definition or accountable owner — Severity: Critical
- **What it is:** Nana and Finance calculate Monday numbers separately, with no agreed rulebook, controlled transformation or sign-off.
- **How I detected it:** Case evidence: Finance's spreadsheet never matches Nana's. Learning-path guidance identifies definitions/ownership as data management and recommends a thin vertical slice around one number and one consumer.
- **Scale:** Every Monday reporting cycle; scope includes hundreds of thousands of exported rows. Exact variance unknown.
- **Effect on the client's number:** The board cannot distinguish a real business movement from different treatment of cancellations, refunds, discounts, shipping, tax, order dates or payment status.
- **What I did about it:** Establish a revenue definition signed by Finance and Operations; version the transformation; publish one certified Monday revenue output with source period, refresh time and exception count.
- **Residual risk:** Source semantics may be incomplete; historic reports may not be comparable until backfilled and agreed.

### F-03: Customer data is copied without lifecycle control — Severity: Critical
- **What it is:** Marketing exports a list of approximately 300,000 people and cannot track how many copies exist.
- **How I detected it:** Explicit case evidence.
- **Scale:** About 300,000 people; number, location, owner and retention of copies unknown.
- **Effect on the client's number:** Audience counts may be stale or duplicated; more importantly, a deletion request may not reach every copy, creating regulatory and trust exposure.
- **What I did about it:** Stop uncontrolled ad-hoc exports; introduce named access, purpose, expiry and export logging; maintain a restricted deletion/suppression workflow and evidence log across approved systems.
- **Residual risk:** Offline copies, email attachments, vendor systems and backups may remain until separately inventoried and addressed. Legal/DPO review is required; do not promise universal erasure from immutable backups without an approved policy.

### F-04: Manual spreadsheet logic is untested production logic — Severity: High
- **What it is:** Critical business calculations live in personal spreadsheets, not a versioned, tested shared process.
- **How I detected it:** Nana rebuilds numbers manually; Finance's spreadsheet differs.
- **Scale:** Weekly close process, hundreds of thousands of source rows.
- **Effect on the client's number:** Formula drift, accidental edits, different filters and undocumented adjustments can change totals without trace.
- **What I did about it:** Move calculation rules into version-controlled transformations; retain a controlled spreadsheet only as a review surface, not the calculation engine.
- **Residual risk:** Staff may continue parallel shadow calculations until the certified output earns trust.

### F-05: Stock freshness and reporting freshness are being conflated — Severity: High
- **What it is:** A blanket demand for real-time dashboards ignores that only stock counts have an explicit freshness requirement.
- **How I detected it:** Case constraint: stock counts cannot go stale; everything else can refresh daily.
- **Scale:** Inventory affects overselling; other reporting is daily by requirement.
- **Effect on the client's number:** A slow or delayed stock update can permit overselling. Conversely, streaming all analytics adds cost and operational complexity without a stated business benefit.
- **What I did about it:** Keep inventory availability in the transactional path with synchronous/transactional correctness; do not use a delayed analytical warehouse as the stock authority. Daily batch is acceptable for non-stock analytics.
- **Residual risk:** Existing inventory transaction correctness, race conditions and cross-channel reservation logic are not described and require application-level testing.

### F-06: No observable, repeatable data operations — Severity: High
- **What it is:** A person starts exports; there is no stated schedule, monitoring, run history, recovery procedure or accountable data owner.
- **How I detected it:** Nana manually rebuilds Monday figures; no pipeline or operational controls are described.
- **Scale:** Weekly reporting today; likely to grow 15–20% annually.
- **Effect on the client's number:** Missed or partial runs can go unnoticed; no evidence trail for what was delivered.
- **What I did about it:** Add a simple scheduled batch job, run status, row counts, freshness timestamp, failure alert, retry and documented recovery.
- **Residual risk:** A small team has limited on-call capacity; start with one critical pipeline and a clear owner.

## Looked wrong, is not wrong

| Apparent problem | Why it looks wrong | Why it is actually fine |
|---|---|---|
| Only daily reporting for most metrics | Investors mentioned real-time dashboards | The brief explicitly permits daily refresh for everything except stock; freshness should follow business need, not a demo seen elsewhere. |
| A modest relational reporting store rather than a lakehouse | A lakehouse sounds more modern and future-proof | Current sources are structured MySQL records and the first use case is one trusted revenue number; a lakehouse adds capabilities the team cannot yet operate. |
| No ML in year one | Forecasting is on the wish list | Forecasts trained on unreconciled sales and inventory data would automate uncertainty. First establish trustworthy history and stock signals. |
| Keep stock authority in the live transactional system | A warehouse seems like a single source of truth | Analytical replication is delayed by nature; it must never become the authority for available-to-sell stock. |

## Could not verify
- Actual revenue variance between Nana and Finance, and the definition each uses.
- Table design, indexes, query plans, database CPU/IO, export duration and exact live-site slowdown.
- Whether a replica is supported by current MySQL version/configuration and what replication lag is acceptable.
- Exact hosting, backup, network, storage and staffing costs; no quotes were supplied.
- Where the 300,000-person marketing list is stored, who receives it, retention, consent/legal basis, processors and deletion propagation.
- Whether Kloud Kart has appointed/registered the relevant data protection roles and processes, its privacy notices, breach process, transfer arrangements or records of processing.
- Legal interpretation of the Data Protection Act 2012 and DPC complaint handling in the company's specific circumstances; obtain Ghana-qualified privacy counsel/DPO review.
- The 90-day response deadline is treated as a hard case constraint, not independently validated here as the universal statutory period for every complaint type.
- Actual inventory freshness tolerance and oversell frequency.
- Full text of all 80 pages of the image-based learning-path PDF; OCR only confirmed selected sections.
