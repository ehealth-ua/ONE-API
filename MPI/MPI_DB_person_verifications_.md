# **MPI\_DB\_person\_verifications\_table**

* [Properties of document](#bookmark=id.mp8xyyb75mcy)  
* [Table fields](#bookmark=id.mp8xyyb75mcy)  
* [Indexes (optional)](#bookmark=id.mp8xyyb75mcy)  
* [Foreign indexes (optional)](#bookmark=id.mp8xyyb75mcy)  
* [Triggers (optional)](#bookmark=id.mp8xyyb75mcy)  
* [Procedures (optional)](#bookmark=id.mp8xyyb75mcy)  
* [Replications (optional)](#bookmark=id.mp8xyyb75mcy)  
* [Related tables](#bookmark=id.mp8xyyb75mcy)  
* [Links to documentation that can create or modify a database object](#bookmark=id.mp8xyyb75mcy)

# **Properties of document**

| Document type | SQL Database Info |
| ----- | :---- |
| **Document title** | \[DRAFT\]\_PostgreSQL\_DB\_person\_verifications\_table |
| **Guideline ID** | GUI-0017 |
| **Author** |  |
| **Document version** | **010** |
| **Document status** | \[DRAFT\] |
| **Date of creation** |  |
| **Date of update** |  |
| **Table name** | **person\_verifications** |
| **Purpose** |  |
| **DB ID** | **PostgreSQL.MPI** |
| **Primary key (PK)** | **{:id, Ecto.UUID, autogenerate: true}** |
| **HL7 version**  | **N/A** |

# **Table fields**

|  | Nesting level | Attribute name | Description EN | Description UA | M/O | Type | HL7 vs eHealth comparison result |
| :---- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 1 | 1 | Id | unique global identifier (binary UUID), automatically generated when a new record is created | унікальний глобальний ідентифікатор (бінарний UUID), автоматично генерується при створенні нового запису | M | binary UUID, autogenerate | N/A |
| 2 | 1 | drfo\_data\_id |  |  | M | UUID | N/A |
| 3 | 1 | drfo\_data\_result |  |  | M | integer | N/A |
| 4 | 1 | drfo\_verification\_status |  |  | M | string | N/A |
| 5 | 1 | drfo\_verification\_reason |  |  | M | string | N/A |
| 6 | 1 | drfo\_synced\_at |  |  | M | utc\_datetime | N/A |
| 7 | 1 | drfo\_unverified\_at |  |  | M | utc\_datetime | N/A |
| 8 | 1 | dracs\_death\_act\_id |  |  | M | UUID | N/A |
| 9 | 1 | dracs\_death\_online\_status |  |  | M | string | N/A |
| 10 | 1 | dracs\_death\_verification\_status |  |  | M | string | N/A |
| 11 | 1 | dracs\_death\_verification\_reason |  |  | M | string | N/A |
| 12 | 1 | dracs\_death\_verification\_comment |  |  | M | string | N/A |
| 13 | 1 | dracs\_death\_unverified\_at |  |  | M | utc\_datetime | N/A |
| 14 | 1 | nhs\_verification\_status |  |  | M | string | N/A |
| 15 | 1 | nhs\_verification\_reason |  |  | M | string | N/A |
| 16 | 1 | nhs\_verification\_comment |  |  | M | string | N/A |
| 17 | 1 | nhs\_unverified\_at |  |  | M | utc\_datetime | N/A |
| 18 | 1 | inserted\_by |  |  | M | UUID | N/A |
| 19 | 1 | updated\_by |  |  | M | UUID | N/A |

# **Indexes (optional)**

|  | Name | Index attributes |
| :---- | ----- | ----- |
| 1 | N/A | N/A |
| 2 | N/A | N/A |

# **Foreign indexes (optional)**

|  | Name | Type |
| :---- | ----- | ----- |
| 1 | N/A | N/A |
| 2 | N/A | N/A |

# **Triggers (optional)**

|  | Name | Description |
| :---- | ----- | ----- |
| 1 | N/A | N/A |
| 2 | N/A | N/A |

# **Procedures (optional)**

|  | Name | Description |
| :---- | ----- | ----- |
| 1 | N/A | N/A |
| 2 | N/A | N/A |

# **Replications (optional)**

|  | Database.Table  | List of attributes (fields) |
| :---- | ----- | ----- |
| 1 | N/A | N/A |
| 2 | N/A | N/A |

# **Related tables**

| Attribute (field) of the current table | Attribute (field) of the target table | Relationship type | Database.Target table |
| ----- | ----- | ----- | ----- |
| N/A | N/A | N/A | N/A |
| N/A | N/A | N/A | N/A |

# **Links to documentation that can create or modify a database object**

|  | Database type | List of tables | System component (repository) | http API endpoint | Business processes that are associated with the table, components, access points |
| :---- | ----- | ----- | ----- | ----- | ----- |
| 1 | N/A | N/A | N/A | N/A | N/A |
| 2 |  N/A | N/A  |  N/A | N/A  |  N/A |

# **Database type**

PostgreSQL

# **List of tables**

* deduplication.audit\_log\_deduplication  
* mpi.manual\_merge\_candidates  
* mpi.manual\_merge\_requests  
* mpi.merge\_candidates  
* mpi.merged\_pairs  
* mpi.verified\_ts  
* mpi.verifying\_ids  
* mpi.confidant\_person\_relationship\_documents  
* mpi.confidant\_person\_relationships  
* mpi.person\_addresses  
* mpi.audit\_log\_mpi  
* mpi.person\_authentication\_methods  
* mpi.person\_documents  
* mpi.person\_dmetaphone\_names  
* mpi.person\_phones  
* mpi.person\_settlement\_last\_names  
* mpi.person\_updates  
* mpi.person\_verification\_candidates  
* mpi.person\_verifications  
* mpi.persons  
* mpi.prepersons

# **System component (repository)**

mpi

