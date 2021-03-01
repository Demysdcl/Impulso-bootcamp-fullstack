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
