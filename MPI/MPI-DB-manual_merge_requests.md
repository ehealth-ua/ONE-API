# Properties of document

| Property | Value |
|----------|-------|
| Document type | SQL Database Info |
| Document title | DRAFT PostgreSQL DB: manual_merge_requests table / Таблиця бази даних PostgreSQL |
| Guideline ID | GUI-0017 |
| Author | @Kateryna Yakovleva |
| Document version | v010 |
| Document status | DRAFT |
| Date of creation | 21.01.2025 |
| Date of update | 30.01.2025 |
| Table name | mpi.manual_merge_requests |
| Purpose | The `manual_merge_requests` table stores requests for manual merging of person records. |
| DB ID | PostgreSQL.mpi |
| Primary key (PK) | id |
| HL7 version | N/A |

## Table fields

| Nesting level | Attribute name | Description EN | Description UA | M/O | Type | HL7 vs eHealth comparison result |
|---------------|----------------|----------------|----------------|-----|------|---------------------------------|
| 1 | id | Unique identifier for the merge request | Унікальний ідентифікатор запиту на злиття | M | uuid | N/A |
| 1 | master_person_id | ID of the master person | ID майстер-особи | M | uuid | N/A |
| 1 | merge_person_id | ID of the person to merge | ID особи для злиття | M | uuid | N/A |
| 1 | status | Status of the merge request | Статус запиту на злиття | M | text | N/A |
| 1 | inserted_at | Timestamp when the record was created | Мітка часу створення запису | M | timestamp | N/A |
| 1 | updated_at | Timestamp when the record was last updated | Мітка часу останнього оновлення запису | M | timestamp | N/A |

## Indexes (optional)

| Name | Index attributes |
|------|------------------|
| manual_merge_requests_master_person_id_idx | master_person_id |

## Foreign indexes (optional)

| Name | Type |
|------|------|
| manual_merge_requests_master_person_id_fkey | Foreign Key (references mpi.persons(id)) |

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
| master_person_id | id | 1:1 | mpi.persons |
| merge_person_id | id | 1:1 | mpi.persons |

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