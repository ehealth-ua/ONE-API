# MPI_DB_audit_log_mpi_table

- [Properties of document](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Table fields](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Indexes (optional)](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Foreign indexes (optional)](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Triggers (optional)](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Procedures (optional)](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Replications (optional)](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Related tables](#Duplicateof[Documentstatus]PostgreSQLDB)

- [Links to documentation that can create or modify a database
  object](#Duplicateof[Documentstatus]PostgreSQLDB)

# Properties of document

  -----------------------------------------------------------------------
     **Document    SQL Database Info
       type**      
  ---------------- ------------------------------------------------------
     **Document    \[DRAFT\]\_PostgreSQL_DB_audit_log_mpi_table
      title**      

  **Guideline ID** GUI-0017

     **Author**    

     **Document    **010**
     version**     

     **Document    \[DRAFT\]
      status**     

     **Date of     
     creation**    

     **Date of     
      update**     

   **Table name**  **audit_log_mpi**

    **Purpose**    

     **DB ID**     **PostgreSQL.MPI**

   **Primary key   **{:id, Ecto.UUID, autogenerate: true}**
       (PK)**      

  **HL7 version**  **N/A**
  -----------------------------------------------------------------------

# Table fields

  ---------------------------------------------------------------------------------------------------
      **Nesting   **Attribute   **Description   **Description   **M/O**   **Type**       **HL7 vs
      level**     name**        EN**            UA**                                     eHealth
                                                                                         comparison
                                                                                         result**
  --- ----------- ------------- --------------- --------------- --------- -------------- ------------
  1   1           Id            unique global   унікальний      M         binary UUID,   N/A
                                identifier      глобальний                autogenerate   
                                (binary UUID),  ідентифікатор                            
                                automatically   (бінарний                                
                                generated when  UUID),                                   
                                a new record is автоматично                              
                                created         генерується при                          
                                                створенні                                
                                                нового запису                            

  2   1           actor_id                                      M         string         N/A

  3   1           resource                                      M         String         N/A

  4   1           resource_id                                   M         String         N/A

  5   1           changeset                                     M         Map            N/A

  6   1           inserted_at                                   M         utc_datetime   N/A
  ---------------------------------------------------------------------------------------------------

# Indexes (optional)

  ------------------------------------------
      **Name**   **Index attributes**
  --- ---------- ---------------------------
  1   N/A        N/A

  2   N/A        N/A
  ------------------------------------------

# Foreign indexes (optional)

  ------------------------------------------
      **Name**   **Type**
  --- ---------- ---------------------------
  1   N/A        N/A

  2   N/A        N/A
  ------------------------------------------

# Triggers (optional)

  ------------------------------------------
      **Name**   **Description**
  --- ---------- ---------------------------
  1   N/A        N/A

  2   N/A        N/A
  ------------------------------------------

# Procedures (optional)

  ------------------------------------------
      **Name**   **Description**
  --- ---------- ---------------------------
  1   N/A        N/A

  2   N/A        N/A
  ------------------------------------------

# Replications (optional)

  ---------------------------------------------
      **Database.Table**   **List of attributes
                           (fields)**
  --- -------------------- --------------------
  1   N/A                  N/A

  2   N/A                  N/A
  ---------------------------------------------

# Related tables

  ------------------------------------------------------------------------------
  **Attribute (field)  **Attribute (field)  **Relationship   **Database.Target
  of the current       of the target        type**           table**
  table**              table**                               
  -------------------- -------------------- ---------------- -------------------
  N/A                  N/A                  N/A              N/A

  N/A                  N/A                  N/A              N/A
  ------------------------------------------------------------------------------

# Links to documentation that can create or modify a database object

  ------------------------------------------------------------------------------------
      **Database   **List of  **System         **http API   **Business processes that
      type**       tables**   component        endpoint**   are associated with the
                              (repository)**                table, components, access
                                                            points**
  --- ------------ ---------- ---------------- ------------ --------------------------
  1   N/A          N/A        N/A              N/A          N/A

  2    N/A         N/A         N/A             N/A           N/A
  ------------------------------------------------------------------------------------

# Database type

PostgreSQL

# List of tables

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

# System component (repository)

mpi
