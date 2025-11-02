# PostgreSQL
PostgreSQL is classified as an Object-Relational Database Management System (ORDBMS). This designation signifies that it combines the features of a traditional relational database with elements of object-oriented programming

PostgreSQL operates on a client-server architecture. This means that a separate client application interacts with a central server process to manage and access data.

## Read and writes are not really equal
The challenge here in looking at Postgres like this is that reads and writes are not really equal.

Postgres reads data in whole 8kb units, called blocks on disk or pages once they’re part of the shared memory. The cost of reading is much lower than writing. Since the most frequently used data generally resides in the shared buffers or the OS cache, many queries never need additional physical IO and can return results just from memory.
Postgres writes by comparison are a little more complicated. When changing an individual tuple, Postgres needs to write data to WAL defining what happens. If this is the first write after a checkpoint, this could include a copy of the full data page. This also can involve writing additional data for any index changes, toast table changes, or toast table indexes. This is the direct write cost of a single database change, which is done before the commit is accepted. There is also the IO cost for writing out all dirty page buffers, but this is generally done in the background by the background writer. In addition to these write IO costs, the data pages need to be in memory in order to make changes, so every write operation also has potential read overhead as well.

## Benefits of PostgreSQL

- Open source and free to use
- Advanced features: ACID compliance, JSON support, full-text search
- Highly extensible: custom types, functions, and extensions
- Strong community and documentation
- Scales for large datasets and high concurrency

## How PostgreSQL Applies ACID
PostgreSQL is famously and strictly ACID-compliant. This is a core feature and a primary reason it's trusted for critical data.

It uses a Write-Ahead Logging (WAL) system for Durability. Changes are first written to a log file on disk before they are applied to the database tables. If the server crashes, it replays this log upon restart to ensure no committed data is lost.

It uses a sophisticated system called Multiversion Concurrency Control (MVCC) to handle Isolation. Instead of locking tables, it shows each transaction a "snapshot" of the data as it existed when the transaction began. This allows reads and writes to happen at the same time without blocking each other.

## “Just Use Postgres (for everything)” https://github.com/Olshansk/postgres_for_everything

- Elasticsearch -- suported with tsvector/tsquery
- MongoDB -- jsonb
- Redis -- CREATE UNLOGGED TABLE
- Vector Databases -- pgvector, pgai
- Snowflake -- pg_mooncake, pg_duckdb
- Pub/Sub -- pgpubsub
- Cron Jobs -- pgcron, pg_timetable
- Browser DB -- PGLite
- Analytics -- pg_analytics, pg_duckdb
- Audit Logs -- temporal_tables, supa_audit, pgaudit, Bemi
- Graph Data -- Apache Age: Graph Database for PostgreSQL to provide graph data processing and analytics capability to all relational databases.
- API -- postgrest, graphql-engine
- Caching -- pogocache, readysettech/readyset
- Performance -- pgassistant: PostgreSQL assistant for developers designed to help understand and optimize PostgreSQL database performance
- Queue --  pgmq

## Should You Use Postgres?
Most of the time - yes. You should always default to Postgres until the constraints prove you wrong.

Bohan Zhang, a member of OpenAI’s infrastructure team and co-founder of OtterTune (a Postgres tuning service), can be quoted as saying23:

“At OpenAI, we utilize an unsharded architecture with one writer and multiple readers, demonstrating that PostgreSQL can scale gracefully under massive read loads.”

“The main message of my talk was that if you are not too write heavy, you can scale Postgres to a very high read throughput with read replicas using only a single master! That is exactly the message that needs to be spelled out as that covers the vast majority of apps.”

“Postgres is probably the default choice for developers right now. You can use Postgres for a very long time. If you are building a startup with read-heavy workloads, just start with Postgres. If you hit a scalability issue, increase the instance size. You can scale it to a very large scale. If in the future the database becomes a bottleneck, congratulations. You have built a successful startup. It’s a good problem to have.”

(slightly edited for clarity and grammar)
