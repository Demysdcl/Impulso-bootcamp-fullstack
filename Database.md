# Database

## Data

Raw values, raw facts, documented observations,
loose records, which are chosen and stored without suffering or treatment

## Information

Set of data with relationship

## PostgreSQL

## Multiprocess architecture

- postmaster
- childs
- writing in disc process

### Memory

- shared_buffers
- wal_buffers
- clog_buffers
- Lock space

- Storage

### Primary characteristics

- Open Source
- Point in time recovery
- Procedural language with support several programming language
- Views, Functions, Procesure, Triggers
- Complex queries and Common table expressions
- Geometric data support
- Multi-version concurrency control

## Settings

### postgresql.conf

File where all Postgres server settings are defined and stored.

Some parameters can only be changed with a database reset

The view pg_settings, accessed through database, store all current settings

by default the postgresql is into PGDATA folder

```sql
SELECT name, setting FROM pg_settings

SHOW [$param_name]
```

#### LIST_ADDRESSES

TCP/IP addresses of the interfaces that the PostgreSQL server will listen and release to connections

#### PORT

The TCP port that the PotgreSQl server will listen. The default is 5432

#### MAX_CONNECTION

The maximum simultaneous number of connections is server PostgreSQL

#### SUPERUSER_RESERVED_CONNECTIONS

Number of connections (slot) reserved for connections to the database of super users

#### AUTHENTICATION_TIMEOUT

Maximum time in seconds to the client to get a connection to the server

#### PASSWORD_ENCRYPTION

Encryption algorithm for new user passwords created in the database

#### SSL

enable SSL encrypted connection (Only if PostgreSQL was compiled with SSL support)

#### SHARED_BUFFERS

Size of shared memory of PostgreSQL server for cache/buffer of tables, indexes and other relations

#### WORKD_MEM

Memory size for grouping and sorting operations (ORDER BY, DISTINCT, MERGE JOINS)

#### MAINTENANCE_WORK_MEM

Memory size for operations like VACUUM, INDEX, ALTER TABLE

### pg_hba

File responsible for controlling user authentication on the PostgreSQL server.

#### Authentication methods

TRUST (connection without password)
REJECT (reject connections)
MD5 (MD5 cryptography)
PASSWORD (password without cryptography)
GSS (generic security service application program interface)
SSPI (security support provider interface - only to windows)
KRB5 (kerberos V5)
IDENT (uses the client's operating system user via ident server)
PEER (uses the client's operating system user)
LDAP (ldap server)
RADIUS (radius server)
CERT (authencation via client's ssl certification)
PAM (pluggable authentication modules. The user needs to be in the database)

### pg_ident

File responsible for mapping users of the operating system with users of the database. The ident option needs to be enabled in pg_hba.conf file

### Administrative commands in Ubuntu

| command                                 | description                              |
| --------------------------------------- | ---------------------------------------- |
| pg_lsclusters                           | List all the clusters                    |
| pg_createcluster $version $cluster_name | Create a new cluster                     |
| pg_dropcluster $version $cluster        | Remove a cluster                         |
| pg_ctlcluster $version $cluster $action | start, stop, status, restart the cluster |

## Cluster definition

Collection of databases that share the same settings as PostgresSQL and the operating system

## Database definition

Schema set with objects/relationships (tables, functions, views, etc)

## PGAdmin

### Setting

- Free access to the cluster in postgresql.conf
- Free access to the cluster for the database user at pg_hba.conf
- Create/Edit users

## USERS / ROLES / GROUPS

```sql
CREATE ROLE name [[WITH] option [...]]
```

Where option can be:

- SUPERUSER | NOSUPERUSER
- CREATEDB | NOCREATEDB
- INHERIT | NOINHERIT
- LOGIN | NOLOGIN
- REPLICATION | NOREPLICATION
- BYPASSRLS | NOBYPASSRLS
- CONNECTION LIMIT connlimit
- [ ENCRIPTED ] PASSWORD $password | PASSWORD NULL
- VALID UNTIL $timestamp
- IN ROLE $role_name
- IN GROUP $role_name
- ROLE $role_name
- ADMIN $role_name
- USER $role_name
- SYSID $uid

```sql
CREATE ROLE davi LOGIN CONNECTION LIMIT 1 PASSWORD '123' IN ROLE teachers;
-- role davi takes on the permissions of role teachers

CREATE ROLE davi LOGIN CONNECTION LIMIT 1 PASSWORD '123' ROLE teachers;
-- role teachers becomes part of role davi assuming their permissions

CREATE ROLE davi LOGIN CONNECTION LIMIT 1 PASSWORD '123';
GRANT teachers TO daniel;

REVOKE teachers FROM davi;

ALTER ROLE davi CONNECTION LIMIT 10;

DROP ROLE davi;
```

Command \du list the roles

### GRANT

These are the privileges to access database objects

privileges

- Table: column, sequence
- Database: domain, foreign data wrapper, foreign server
- Function: language, large object
- Schema: tablespace, type

```sql
GRANT ALL ON TABLE student TO teachers;

CREATE ROLE davi INHERIT LOGIN PASSWORD '123' IN ROLE teacher;

REVOKE teachers FROM davi;
```

DML - Data Manipulation Language
DDL - Data Definition Language

#### Idempotency (IDEMPOTÊNCIA)

Property that some actions/operations have enabling them to be executed several times without
changing the result after the initial application (propriedade que algumas ações/operações possuem
possibilitando-as de serem executadas diversas vezes sem alterar o resultado apóes a aplicação inicial)

IF EXISTS improves the idempotency

```sql
INSERT INTO
    agency (bank_number, number_name)
VALUES
    (341.1, 'Downtown')
ON CONFLICT
    (bank_number)
DO NOTHING;
```

##### TRUNCATE

Empty the table

```sql
 TRUNCATE table only $name $restartIdentityOrContinueIdentity, $cascadeOrRestrict
```

### Aggregate functions

- AVG
- COUNT
- MAX
- MIN
- SUM

```sql
SELECT
    COUNT(id)
FROM
    client_transactions
HAVING
    COUNT(id) > 150;
```

### JOINS

- JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL JOIN
- CROSS JOIN

## Common table expressions (CTE)

Auxiliary way of organizing "statements", that is, code blocks,
for very large queries, generating temporary tables and creating relationships between them

```sql
WITH
    tbl_tmp_bank
AS (SELECT number, name FROM banck)
SELECT number, name from tbl_tmp_bank;

WITH params as (
    SELECT 213 AS number_bank
), tbl_temp_bank AS (
    SELECT number, name FROM bank
    JOIN params ON params.number_bank = bank.number
)
SELECT number, name
from tbl_tmp_bank;
```
