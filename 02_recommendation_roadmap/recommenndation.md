## Data Strategy Recommendation

**Prepared for:** Nana Adjei, Head of Operations  
**Purpose:** Recommend a practical and affordable data strategy for Kloud Kart.

---

## 1. Establish a Separate Reporting Environment

Kloud Kart should establish a small, separate reporting environment using the pre-approved second server/read replica.

Currently, customer transactions, orders, inventory, customer accounts, and reporting activities share one MySQL database on the same server as the live website. Monday reporting exports have already slowed the live website twice.

Using a separate reporting environment will reduce competition between reporting workloads and live customer transactions.

**Recommended Approach:**
- Keep customer transactions and stock availability on the live transactional system.
- Use the second server/read replica to separate reporting reads from the live website.
- Copy the required data into a modest reporting database.
- Use the reporting database to calculate one agreed Monday revenue figure.

> **Note:** Ordinary business reports should refresh daily. Stock availability must remain under the live system because an analytical replica may experience replication lag and should not become the authority for available-to-sell stock.

---

## 2. Establish Trusted Monday Revenue Reporting

Finance and Operations should agree on one written revenue definition and use one controlled calculation.

**The reporting process should:**
- Document the agreed revenue definition.
- Apply the same calculation rules consistently.
- Compare results against source records.
- Record and investigate differences using a reconciliation process.
- Obtain approval from the responsible business owners.

This will replace separate, manually maintained calculations with a consistent reporting approach.

The first priority should be a tested and reconciled Monday revenue report, rather than a dashboard displaying figures that have not been validated.

---

## 3. Introduce Customer-Data Accountability Controls

Kloud Kart should introduce documented controls for customer-data exports and copies.

**Proposed Controls:**
- **Export Inventory:** Record customer-data exports and where they are stored.
- **Access/Expiry Log:** Track who can access customer information and when access should end.
- **Deletion-Evidence Workflow:** Record how customer deletion requests are handled.

These controls should be formally adopted by the company, assigned to responsible personnel, and reviewed against applicable **Ghana Data Protection Act** requirements.

---

## 4. Hire the Data Team in Sequence

Kloud Kart should use its two available data hires in the following order:

1. **First Hire — Data Engineer**  
   Establish dependable data movement, protect the live system from reporting workloads, and introduce pipeline validation, logging, and monitoring.
2. **Second Hire — Analytics Engineer**  
   Work with Finance and Operations to agree on business definitions, develop controlled reporting calculations, and publish trusted reports.

Each role should have clear **90-day outcomes** rather than being assessed only by the tools they know.

---

## 5. Defer Unnecessary Technology Investment

Kloud Kart should **not** build a lakehouse, purchase an expensive enterprise data platform, or stream every business metric in real time during year one.

- The immediate business problems are reporting reliability, production database protection, consistent revenue figures, and customer-data accountability.
- A modest relational reporting database is a more proportionate starting point for the company's structured MySQL data and current team capacity.
- Demand forecasting should also be deferred until trustworthy sales and inventory history has been established.

---

## 6. Preliminary Budget

For planning purposes, reserve approximately:
- **US$300–800 per month** for separate compute, storage, backup, and monitoring.
- **US$2,000–6,000 one-time** for initial setup and migration.

> **Disclaimer:** These are preliminary estimates, not supplier quotations. Salaries, taxes, and any paid reporting licence are excluded. Obtain local supplier quotes and load-test the proposed environment before purchasing.

---

## 7. Management Decision Requested

Management should approve the design and validation of a modest separate reporting environment using the pre-approved second server/read replica, prioritize the Data Engineer hire, and direct Finance and Operations to agree on one revenue definition.

- **First Board Commitment:** A tested, reconciled Monday revenue report and a documented customer-data process.
- **Future Reconsideration:** More advanced capabilities—including broad real-time dashboards, a lakehouse, and demand forecasting—should be reconsidered when the underlying data is trustworthy and the business need is demonstrated.