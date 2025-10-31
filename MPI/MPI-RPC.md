# Properties of RPC method document

| Property | Value |
|----------|-------|
| Document type | RPC Method |
| Document name | DRAFT MPI Person Management |
| Guideline ID | GUI-0023 |
| Author | @Maksym Sokhatsky |
| Document version | v010 |
| Document status | DRAFT |
| Date of creation | 21.01.2025 |
| Date of update | 30.01.2025 |
| API ID | RPC-MPI-001 |
| Microservices (namespace) | mpi |
| Resource | Person, Preperson, MergeCandidate, ManualMergeRequest |
| Scope | create, search, update, merge, verification |

## Purpose
The RPC methods in the MPI service provide functionality for managing person records, including creation, retrieval, update, merge, and verification. These methods ensure data integrity in the Master Patient Index, supporting deduplication and synchronization across the eHealth system.

## Logic
The RPC methods interact with the database repositories (Repo, DeduplicationRepo) and validators to manage person data. Operations include inserting new persons, searching with parameters, updating records, handling merges, and publishing updates. Validation ensures data consistency, such as tax ID with birth date and gender.

## Relationship between RPC Methods and API Methods

| API Method | Call Context | RPC Call Type |
|------------|--------------|---------------|
| POST /persons | Create a new person record | By Specific Condition |
| GET /persons/:id | Retrieve person by ID | By Specific Condition |
| PATCH /persons/:id | Update person details | By Specific Condition |
| POST /merges | Initiate merge of persons | By Specific Condition |
| GET /search/persons | Search persons with parameters | By Specific Condition |

## Input parameters

| Input parameter | Values | Type | Description | Example |
|-----------------|--------|------|-------------|---------|
| person_data | Map with person attributes | Map | Data for creating or updating a person | %{"first_name" => "John", "last_name" => "Doe", "birth_date" => "1990-01-01", "gender" => "MALE", "tax_id" => "1234567890"} |
| id | Person ID | Binary | Unique identifier for the person | "a1b2c3d4-e5f6-47g8-9h0i-j1k2l3m4n5o6" |
| search_params | Map of search criteria | Map | Parameters for searching persons | %{"tax_id" => "1234567890", "birth_date" => "1990-01-01"} |
| merge_data | Map for merge request | Map | Data for merging persons | %{"master_person_id" => "id1", "merge_person_id" => "id2"} |

## Output parameters

| Output parameter | Values | Type | Description | Example |
|------------------|--------|------|-------------|---------|
| person | JSON object with person details | Map | Contains person attributes | %{"id" => "a1b2c3d4", "first_name" => "John", "status" => "active"} |
| search_results | List of person maps | List | Results from search query | [%{"id" => "id1"}, %{"id" => "id2"}] |
| merge_result | Map with merge status | Map | Result of merge operation | %{"status" => "merged", "merged_pairs" => 1} |

## Request structure
```elixir
# Example for create_person/1
Core.Rpc.create_person(%{"first_name" => "John", "tax_id" => "1234567890"})

# Example for get_person_by_id/1
Core.Rpc.get_person_by_id("a1b2c3d4-e5f6-47g8-9h0i-j1k2l3m4n5o6")

# Example for search_persons/1
Core.Rpc.search_persons(%{"tax_id" => "1234567890"})

# Example for update_person/2
Core.Rpc.update_person("id", %{"status" => "inactive"})
```

## Response structure
```elixir
# Example for create_person/1
{:ok, %{"id" => "new_id", "status" => "active"}}

# Example for get_person_by_id/1
{:ok, %{"id" => "a1b2c3d4", "first_name" => "John"}}

# Example for search_persons/1
{:ok, [%{"id" => "id1"}, %{"id" => "id2"}]}

# Example for update_person/2
{:ok, %{"id" => "id", "status" => "inactive"}}
```

## Error Handling
- `:not_found` (404): Returned when a person or record is not found.
- `:unprocessable_entity` (422): Returned for validation failures, e.g., invalid tax ID or data format.
- `:forbidden` (403): Returned for unauthorized operations.
- `:internal_server_error` (500): For database or Kafka publication errors.

