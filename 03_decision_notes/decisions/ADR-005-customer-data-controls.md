# ADR-005: Control customer exports and deletion evidence before broadening analytics

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Nana Adjei; designated privacy lead/DPO and Ghana counsel must approve legal controls

## Context
Marketing handles a list of about 300,000 people and cannot state how many copies exist. The case imposes a 90-day DPC complaint response deadline. No inventory of processors, copies, retention or legal basis was provided.

## Decision
Pause uncontrolled exports; maintain an approved export register with purpose, owner, recipients, access and expiry, and a restricted deletion case log that records systems checked, actions, exceptions and evidence. Complete a privacy/legal review before treating the workflow as compliant.

## Alternatives considered
### Alternative A: Keep spreadsheet exports and ask teams to delete files when requested
- **How it would work:** Email teams and rely on manual confirmation.
- **Why it is attractive:** Familiar and cheap.
- **Why rejected:** No reliable inventory, audit trail or evidence that all known copies were addressed.

### Alternative B: Buy a full enterprise governance suite now
- **How it would work:** Deploy a broad catalogue, lineage, consent and policy platform.
- **Why it is attractive:** More automation and central visibility.
- **Why rejected:** Scope and cost are not justified before the company knows its data locations and workflows; process ownership is still required.

## Consequences
- **What this buys:** Better accountability, faster investigation and evidence for a complaint response.
- **What this costs:** Staff time to inventory systems and enforce expiry; manual work remains for unintegrated copies.
- **What it costs the client if I am wrong:** The register may omit shadow copies or legal obligations; a log alone is not proof of compliance.
- **What would make me revisit this:** Inventory reveals many processors/locations, repeated deletion failures, or counsel requires stronger technical enforcement.

## What this survives
If marketing exports grow or investor scrutiny increases, the register provides a control baseline and evidence trail. It scales by adding systems and automation; it does not claim that every backup or third-party copy can be erased instantly.
