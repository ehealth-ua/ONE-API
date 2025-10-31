# Properties of document

| Property | Value |
|----------|-------|
| Document type | SQL Database Info |
| Document title | DRAFT PostgreSQL DB: audit_log_deduplication table / Таблиця бази даних PostgreSQL |
| Guideline ID | GUI-0017 |
| Author | @Maksym Sokhatskyi |
| Document version | v010 |
| Document status | DRAFT |
| Date of creation | 21.01.2025 |
| Date of update | 30.01.2025 |
| Table name | deduplication.audit_log_deduplication |
| Purpose | The `audit_log_deduplication` table stores audit logs for deduplication operations in the MPI system. |
| DB ID | PostgreSQL.mpi |
| Primary key (PK) | id |
| HL7 version | N/A |

## Table fields

| Nesting level | Attribute name | Description EN | Description UA | M/O | Type | HL7 vs eHealth comparison result |
|---------------|----------------|----------------|----------------|-----|------|---------------------------------|
| 1 | id | Unique identifier for the audit log record | Унікальний ідентифікатор запису аудиту | M | uuid | N/A |
| 1 | action | Type of deduplication action performed | Тип дії дедуплікації | M | text | N/A |
| 1 | details | Details of the deduplication event | Деталі події дедуплікації | O | jsonb | N/A |
| 1 | inserted_at | Timestamp when the record was created | Мітка часу створення запису | M | timestamp | N/A |
| 1 | updated_at | Timestamp when the record was last updated | Мітка часу останнього оновлення запису | M | timestamp | N/A |

## Indexes (optional)

| Name | Index attributes |
|------|------------------|
| audit_log_deduplication_action_idx | action |

## Foreign indexes (optional)

| Name | Type |
|------|------|
| N/A | N/A |

## Triggers (optional)

| Name | Description |
|------|-------------|
| N/A | N/A |

## Procedures (optional)

| Name | Description |
|------|-------------|
| N/A | N/A |

## Replications (optional)

| Database.Table | List of attributes (fields) |
|----------------|----------------------------|
| N/A | N/A |

## Related tables

| Attribute (field) of the current table | Attribute (field) of the target table | Relationship type | Database.Target table |
|---------------------------------------|--------------------------------------|-------------------|-----------------------|
| N/A | N/A | N/A | N/A |

## Links to documentation that can create or modify a database object
- [MPI RPC Methods](https://e-health-ua.atlassian.net/wiki/)
- [MPI Person Updates Job](https://e-health-ua.atlassian.net/wiki/)

### Database type
PostgreSQL

### List of tables
- deduplication.audit_log_deduplication
- mpi.manual_merge_candidates
- mpi.manual_merge_requests
- mpi.merge_candidates
- mpi.merged_pairs
- mpi.verified_ts
- mpi.verifying_ids
- mpi.confidant_person_relationship_documents
- mpi.confidant_person_relationships
- mpi.person_addresses
- mpi.audit_log_mpi
- mpi.person_authentication_methods
- mpi.person_documents
- mpi.person_dmetaphone_names
- mpi.person_phones
- mpi.person_settlement_last_names
- mpi.person_updates
- mpi.person_verification_candidates
- mpi.person_verifications
- mpi.persons
- mpi.prepersons

### System component (repository)
mpi

### http API endpoint
- [POST /persons](https://e-health-ua.atlassian.net/wiki/)
- [GET /persons/:id](https://e-health-ua.atlassian.net/wiki/)
- [PATCH /persons/:id](https://e-health-ua.atlassian.net/wiki/)
- [POST /merges](https://e-health-ua.atlassian.net/wiki/)

### Business processes that are associated with the table, components, access points
- [Person Deduplication Process](https://e-health-ua.atlassian.net/wiki/)
- [Person Merge Process](https://e-health-ua.atlassian.net/wiki/)
