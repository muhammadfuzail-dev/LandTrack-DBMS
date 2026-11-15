# LandTrack-DBMS

Punjab Land Registry and Intiqal Management System

Database Systems Semester Project - Phase 1 Proposal

## Group Information

Group Name: LandTrack Team

1. Muhammad Fuzail, bcsf25m037
2. Hayan Ullah, bcsf25m056

Repository: https://github.com/muhammadfuzail-dev/LandTrack-DBMS

## 1. Introduction and Problem Statement

The Punjab Land Registry and Intiqal Management System is a database-driven project designed to manage land ownership records, ownership transfers (Intiqal), plot subdivisions, revenue records, and disputes.

Land ownership involves multiple people, shared ownership percentages, inheritance, sale, gifts, and division of land into smaller plots. Managing these records requires accurate tracking of ownership history and mutation applications. The proposed system provides a centralized academic database model to maintain these records, reduce inconsistencies, and support efficient retrieval of land-related information.

The project uses synthetic data and is developed as an academic prototype, not as an official government land-record service.

## 2. Objectives

- Maintain records of districts, tehsils, Mauzas, people, and land plots.
- Track current and historical ownership, including fractional ownership shares.
- Manage mutation applications for sale, inheritance, gift, and partition.
- Maintain mutation stages, registry deeds, and supporting documents.
- Track plot subdivisions and their parent-child relationships.
- Record objections, inheritance claims, appeals, and court cases.
- Maintain officer assignments, inspections, and verification records.
- Manage land revenue assessments and payment records.
- Enforce data integrity through constraints, triggers, and transactions.

## 3. Main Database Entities (25)

A. Location and Land Management

1. District
2. Tehsil
3. Mauza
4. Plot
5. LandClass

B. People and Ownership

6. Person
7. OwnershipShare
8. OwnershipAudit
9. LandRecord
10. LandRecordEntry

C. Mutation Management

11. Mutation
12. MutationType
13. MutationStage
14. RegistryDeed
15. MutationDocument
16. DocumentVerification

D. Revenue and Officer Management

17. RevenueOfficer
18. OfficerAssignment
19. LandInspection

E. Dispute and Financial Management

20. Objection
21. InheritanceClaim
22. CourtCase
23. Appeal
24. LandTaxAssessment
25. LandTaxPayment

The entities are connected through primary keys, foreign keys, and one-to-one, one-to-many, and many-to-many relationships. Self-referencing relationships are used for plot subdivisions and officer supervision.

## 4. Important Business Rules

1. Active ownership shares of a plot must total 100%.
2. A person cannot transfer more land ownership than they currently hold.
3. Ownership changes must be recorded through an approved mutation.
4. A plot cannot be its own parent.
5. Subdivided plot areas must not exceed the parent plot's area.
6. Plot subdivision relationships must not contain cycles.
7. Mutation stages must follow the defined workflow.
8. An unresolved objection must prevent mutation completion.
9. Required supporting documents must be verified before approval.
10. Officers can process cases only within their assigned authority.
11. Ownership history must be preserved through audit records.
12. Payments must not exceed the outstanding assessment balance.

These rules are implemented using PostgreSQL constraints, triggers, functions, transactions, and permissions.

## 5. Advanced DBMS Features

- Recursive CTEs: retrieve complete plot subdivision hierarchies.
- Window Functions: rank plots by ownership transfers and analyze mutation activity.
- Triggers: validate ownership transfers and maintain audit records.
- Stored Functions: perform controlled ownership-transfer operations.
- Transactions: ensure mutation approval and ownership updates are atomic.
- Views: display current ownership and mutation status.
- Indexes: improve searches by Khasra number, Mauza, and mutation ID.
- Role-Based Access: different permissions for revenue officers and read-only users.
- Materialized Views: reporting on mutation statistics and processing times.

## 6. Sample Database Queries

1. Ownership Transfer Analysis: identify plots with the highest number of ownership changes during the last ten years, grouped by Mauza.
2. Mutation Performance: find tehsils and Mauzas with the highest average mutation processing time and the greatest number of pending applications.
3. Plot Subdivision and Ownership: retrieve the complete subdivision tree of an original plot and display the current owners and their ownership shares for every sub-plot.
4. Pending Document Verification: identify mutation applications with missing or unverified supporting documents.
5. Revenue Analysis: calculate outstanding land revenue assessments and summarize payments by Mauza.

## 7. Application and Technology Stack

- DBMS: PostgreSQL
- Frontend: HTML, CSS, JavaScript
- Backend: Python Flask
- Database Connectivity: psycopg
- Database Operations: parameterized SQL queries, stored functions, triggers, and transactions

The web application provides basic interfaces for managing land records, people, ownership shares, mutation applications, and reports. Database integrity and business logic remain enforced at the PostgreSQL level.

## 8. Expected Outcome

A well-structured relational database system that demonstrates database design, normalization, relationships, constraints, advanced SQL, transaction management, and security.

The project provides a realistic academic model of Punjab land-record and mutation management, showing how a carefully designed database can maintain ownership history, manage complex relationships, and support reliable reporting.

Application Track: Yes - Web Application
Project Scope: Advanced academic prototype using synthetic data
