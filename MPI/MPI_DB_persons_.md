# **MPI\_DB\_persons\_table**

# **Properties of document**

| Document type | SQL Database Info |
| ----- | :---- |
| **Document title** | \[DRAFT\]\_PostgreSQL\_DB\_persons\_table |
| **Guideline ID** | GUI-0017 |
| **Author** |  |
| **Document version** | **010** |
| **Document status** | \[DRAFT\] |
| **Date of creation** |  |
| **Date of update** |  |
| **Table name** | **persons** |
| **Purpose** |  |
| **DB ID** | **PostgreSQL.MPI** |
| **Primary key (PK)** | **{:id, Ecto.UUID, autogenerate: true}** |
| **HL7 version**  | **N/A** |

# **Table fields**

|  | Nesting level | Attribute name | Description EN | Description UA | M/O | Type | HL7 vs eHealth comparison result |
| :---- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 1 | 1 | Id | unique global identifier (binary UUID), automatically generated when a new record is created | унікальний глобальний ідентифікатор (бінарний UUID), автоматично генерується при створенні нового запису | M | binary UUID, autogenerate | N/A |
| 2 | 1 | version |  |  | M | string | N/A |
| 3 | 1 | first\_name |  |  | M | string | N/A |
| 4 | 1 | last\_name |  |  | M | string | N/A |
| 5 | 1 | second\_name |  |  | M | string | N/A |
| 6 | 1 | birth\_date |  |  | M | date | N/A |
| 7 | 1 | birth\_country |  |  | M | string | N/A |
| 8 | 1 | birth\_settlement |  |  | M | string | N/A |
| 9 | 1 | gender |  |  | M | string | N/A |
| 10 | 1 | email |  |  | M | string | N/A |
| 11 | 1 | tax\_id |  |  | M | string | N/A |
| 12 | 1 | unzr |  |  | M | string | N/A |
| 13 | 1 | death\_date |  |  | M | string | N/A |
| 14 | 1 | preferred\_way\_communication |  |  | M | string | N/A |
| 15 | 1 | invalid\_tax\_id |  |  | M | boolean | N/A |
| 16 | 1 | is\_active |  |  | M | boolean | N/A |
| 17 | 1 | secret |  |  | M | string | N/A |
| 18 | 1 | emergency\_contact |  |  | M | map | N/A |
| 19 | 1 | confidant\_person |  |  | M | {:array, :map} | N/A |
| 20 | 1 | patient\_signed |  |  | M | boolean | N/A |
| 21 | 1 | process\_disclosure\_data\_consent |  |  | M | boolean | N/A |
| 22 | 1 | status |  |  | M | string | N/A |
| 23 | 1 | inserted\_by |  |  | M | string | N/A |
| 24 | 1 | updated\_by |  |  | M | string | N/A |
| 25 | 1 | no\_tax\_id |  |  | M | boolean | N/A |
| 26 | 1 | nhs\_request\_number |  |  | M | string | N/A |
| 27 | 1 | nhs\_request\_comment |  |  | M | string | N/A |
| 28 | 1 | verification\_status |  |  | M | String | N/A |

# **Indexes (optional)**

|  | Name | Index attributes |
| :---- | ----- | ----- |
| 1 | persons\_first\_name\_last\_name\_second\_name\_tax\_id\_birth\_date\_key | first\_name, last\_name, second\_name, tax\_id, birth\_date(UNIQUE, WHERE: status='active') |
| 2 | auth\_method\_search\_index | is\_active, birth\_date, status, lower(first\_name), lower(last\_name), lower(second\_name) |
| 3 | persons\_is\_active\_status\_birth\_date\_tax\_id\_idx | is\_active, status, birth\_date, tax\_id |
| 4 | persons\_documents\_idx | documents (using GIN) |
| 5 | persons\_updated\_at\_idx | updated\_at |
| 6 | persons\_unzr\_idx | Unzr |
| 7 | persons\_authentication\_methods\_idx | authentication\_methods (using GIN) |
| 8 | persons\_tax\_id\_index | tax\_id |
| 9 | persons\_birth\_date\_index | birth\_date |
| 10 | persons\_uniq\_index | tax\_id, birth\_date, last\_name, first\_name, second\_name (UNIQUE, WHERE: status='active') |
| 11 | auth\_method\_search\_idx | birth\_date, lower(last\_name), lower(first\_name), lower(second\_name) |
| 12 | persons\_verification\_status\_index | verification\_status |
| 13 | persons\_verification\_reason\_index | verification\_reason |
| 14 | persons\_synchronization\_idx1 | id, birth\_date (с условием: status \= 'active' AND tax\_id IS NULL) |
| 15 | persons\_synchronization\_idx2 | id (с условием: status \= 'active' AND tax\_id IS NOT NULL) |

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

