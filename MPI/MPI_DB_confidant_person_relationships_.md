# **Properties of document**

| Document type | SQL Database Info |
| ----- | :---- |
| **Document title** | \[DRAFT\]\_PostgreSQL\_DB\_confidant\_person\_relationships\_table |
| **Guideline ID** | GUI-0017 |
| **Author** |  |
| **Document version** | **010** |
| **Document status** | \[DRAFT\] |
| **Date of creation** |  |
| **Date of update** |  |
| **Table name** | **confidant\_person\_relationships** |
| **Purpose** |  |
| **DB ID** | **PostgreSQL.MPI** |
| **Primary key (PK)** | **{:id, Ecto.UUID, autogenerate: true}** |
| **HL7 version**  | **N/A** |

# **Table fields**

|  | Nesting level | Attribute name | Description EN | Description UA | M/O | Type | HL7 vs eHealth comparison result |
| :---- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 1 | 1 | Id | unique global identifier (binary UUID), automatically generated when a new record is created | унікальний глобальний ідентифікатор (бінарний UUID), автоматично генерується при створенні нового запису | M | binary UUID, autogenerate | N/A |
| 2 | 1 | is\_active |  |  | M | Boolean | N/A |
| 3 | 1 | active\_to |  |  | M | Date | N/A |
| 4 | 1 | verification\_status |  |  | M | String | N/A |
| 5 | 1 | verification\_reason |  |  | M | String | N/A |
| 6 | 1 | verification\_comment |  |  | M | String | N/A |
| 7 | 1 | inserted\_by |  |  | M | UUID | N/A |
| 8 | 1 | updated\_by |  |  | M | UUID | N/A |

# **Indexes (optional)**

|  | Name | Index attributes |
| :---- | ----- | ----- |
| 1 | confidant\_person\_relationships\_person\_id\_idx | person\_id |
| 2 | confidant\_person\_relationships\_confidant\_person\_id\_idx | confidant\_person\_id |

# **Foreign indexes (optional)**

|  | Name | Type |
| :---- | ----- | ----- |
| 1 | confidant\_person\_relationships\_person\_id\_fkey | Foreign Key (references mpi.persons(id)) |
| 2 | confidant\_person\_relationships\_confidant\_person\_id\_fkey | Foreign Key (references mpi.persons(confidant\_person\_id)) |

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

