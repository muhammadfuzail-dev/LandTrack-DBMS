# LandTrack-DBMS

Punjab Land Record and Mutation (Intiqal) Tracking Database

Database Systems 3rd Semester Project, PUCIT, University of the Punjab

Teacher Ahmad Hassan.
Group name: LandTrack Team.
DBMS: PostgreSQL

## Group Members

1.Muhammad Fuzail, bcsf25m037 - Project Manager + Data Architect (ERD, schema, normalization)
2. Hayan Ullah, bcsf25m056 - Database Developer + QA/Documentation (DDL, SQL, tests)

Roles rotate in at least one phase.

## Problem Statement

In Punjab, land ownership is maintained through revenue records kept by patwaris and updated through mutation (intiqal) after every sale, inheritance, gift or partition. Plots are repeatedly subdivided among heirs, ownership is held in fractional shares, and mutations pass through several approval stages, so records easily become inconsistent and hard to trace.

It is difficult to answer basic questions such as who owned a plot at a given date, whether the shares of a plot add up correctly, how a plot was subdivided, or where mutations are delayed.

This project designs a relational database that stores plots, owners, shares, subdivisions and mutation workflows, enforces the ownership rules inside the database, and supports analysis of transfers, delays and disputes. It is an academic prototype using realistic synthetic data only.

## Stakeholders

- Patwari, Girdawar, Tehsildar: create, verify and approve mutations; maintain plot and ownership records
- Landowners, heirs, buyers, sellers: hold shares in plots; apply for or are affected by mutations
- Sub-registrars, lawyers, property dealers: register deeds and verify ownership history before transactions
- Policy analysts, researchers: study mutation delays, fragmentation of holdings and disputes

## Why This Topic

- Real problem: land disputes and delayed mutations affect landowners and revenue staff every day.
- Unique: built on a Pakistan-specific revenue-record domain (mauza, khasra, intiqal), not a generic record store.
- Rich structure: geographic hierarchy, self-referencing plot subdivision tree, M:N ownership with fractional shares, weak entity for mutation stages, 1:1 mutation-deed link.
- Real rules and analytics: ownership rules are enforced inside the database; data supports recursive, window-function and delay/trend analysis.

## Sample Questions

1. Which plots changed ownership most often in the last ten years, and in which mauzas are they located?
2. Which tehsils and mauzas have the longest average mutation processing time and the most pending mutations?
3. For a given original plot, what is the complete subdivision tree and who currently owns each sub-plot, with what share?

## Entities (15)

1. District
2. Tehsil
3. Mauza
4. Person
5. Plot
6. LandClass
7. OwnershipShare
8. MutationType
9. Mutation (Intiqal)
10. MutationStage (weak entity)
11. RegistryDeed
12. RevenueOfficer
13. Objection
14. InheritanceClaim
15. OwnershipAudit

Key relationships:

- Person - Plot: M:N via OwnershipShare
- Mutation - MutationStage: 1:N (weak)
- Mutation - RegistryDeed: 1:1
- District - Tehsil - Mauza: hierarchy
- Plot and RevenueOfficer: self-referencing

## Business Rules Enforced by the Database

- R1: Active owners' shares of a plot must total exactly 100%.
- R2: Total area of sub-plots must not exceed the area of the parent plot.
- R3: A plot cannot be its own parent; a share fraction must be between 0 and 1.
- R4: Ownership may change only through an approved mutation, never by a direct update.
- R5: A seller must hold at least the share being transferred.
- R6: A plot with an open objection cannot complete a mutation.
- R7: Mutation stages follow a fixed order; completion date is not before application date.
- R8: A deed number and a khasra number are unique within their mauza.

## AI-Built Application Track

Yes, optional and limited in scope. A small Flask web interface with psycopg and parameterized SQL only (no ORM) will be built after the database is complete, with two database-enforced roles (revenue officer, read-only public/analyst).

The ERD, schema, normalization and all SQL logic are our own work. An AI Usage Log is maintained from the start and every use of AI is recorded.
