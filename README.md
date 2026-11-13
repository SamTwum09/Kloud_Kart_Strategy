# Kloud Kart: A Practical Data Strategy

A data engineering consulting lab for Kloud Kart, an online shop whose reporting, revenue numbers and customer data are not under control.

**Author:** Samuel Twum | **Client:** Nana Adjei, Head of Operations | Date:13th November 2026

## The problem

Kloud Kart does not mainly lack a data warehouse. It lacks a controlled path from operational records to business decisions:

- Reporting and the live shop share one 40 GB MySQL database (about 4,000 orders a day). Monday exports have slowed the site twice.
- Operations and Finance calculate Monday revenue separately and never match.
- Marketing holds a list of about 300,000 people and cannot say how many copies exist.

## Recommendation

1. Run reporting on the pre-approved second server / read replica, never on the live database.
2. Agree one signed revenue definition and one reconciled calculation.
3. Add customer-data controls: export register, expiry log, deletion evidence.
4. Hire a Data Engineer first, then an Analytics Engineer.
5. Defer a lakehouse, streaming and forecasting.

Stock stays in the live system. Everything else refreshes daily.

## Contents

| File | What it is |
|---|---|
| [`data_findings.md`](data_findings.md) | Ranked findings and what could not be verified |
| [`client_memo.md`](client_memo.md) | Short memo to the client |
| [`recommendation.md`](recommendation.md) | Data strategy and preliminary budget |
| [`roadmap.md`](roadmap.md) | 12-month plan and hiring order |
| [`adr/`](adr/) | Five Architecture Decision Records |
| [`improvement.md`](improvement.md) | Monday Close Control Workbook (improvement beyond the brief) |
| `Board_Presentation.pptx` | Board slides |

## Limitations

No row-level data, schema or privacy records were supplied, so this work does **not** claim:

- Which revenue figure (Finance or Operations) is correct, or the size of the gap
- Any measured website slowdown or deletion backlog
- Exact costs. The budget (US$300-800 per month plus US$2,000-6,000 one-time) is a planning estimate, not a quote
- Legal compliance. The customer-data controls need review by Ghana privacy counsel
