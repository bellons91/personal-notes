# Davide's notes

👋 Welcome to your new my personal notes, powered by Foam!

The repository can be found on [GitHub](https://github.com/bellons91/personal-notes).

## Most important sections

- Azure Certifications
  - [[az-900]]
  - [[az-204]]

## Quick notes

- **Parquet**: data format used by Apache Spark;
- **Password spray**: hacking technique. You try the most common passwords on multiple accounts, trying to find an account that used that password;
- **SIM-jacking**: vulnerability that uses SIMs and SMS content;
- **Hammering**: hacking technique. Hackers send continuous push notifications until the victim, annoyed by these notifications, accepts one and gives permissions to the intruder;
- **Adversary-in-the-middle**: deceive users;
- **DAPR**: used for Sidecar architecture. The main application communicates with the sidecar via GRPC or HTTP;
- **Fitness Functions**: functions that check the -ilities of the architecture. You use metrics and monitors;
- **ArchUnitNET**: library for testing the code architecture. You can validate the modules dependencies;
- **JIT** (Just-in-time compilation): compiles the code on the fly; it compiles the code that you are going to execute;
- **OSR** (On-stack replacement): used to optimize methods with long runs. If during the first executions it finds something to optimize, it replaces the low-level code on the stack;
- **Dynamic PGO**: the Jitter understands the code usage and optimizes the compilation;
- **SNAT (source network address translation)**: SNAT maps the IP address of the backend to the public IP address of your load balancer. SNAT prevents outside sources from having a direct address to the backend instances;
- **B-tree**: data structure used for indexing in SQL databases;
- **Rowstore index**: index based on the value of the row. Userful for searches for specific values or ranges;
- **Columnstore index**: index based on the values for a specific column. It's a `distinct` on the values on the column, and is useful for searching for multiple rows with the same value in that column. You can even use an index on every column; it is optimized for reads; it is useful for creating reports;
- **Heap (SQL)**: column without indexes;
- **Graph on SQL server**: you can create graphs using `CREATE TABLE AS EDGE` and `CREATE TABLE AS NODE`;
- **Clustered-index** on a date makes the database equivalent to a time-series database;
- **RLS (Row-level security)**: based on the user executing the query, the query can view a subset of the rows. It happens using a **Tabular function** that, given the user, returns the subset of the rows. This subset is then optimized by the DB engine. A good usage is multi-tenant applications, where you don't want data leak to other companies. Also known as **Policy-Based Security**.
- **Data masking**: the database masks sensible data automatically, so that developers (and log tools) cannot access the data. To see the actual value you have to execute an `UNMASK` operation;
- **Ledger**: to entrust that data has not been changed from a specific date, all the updates on the main db are also stored on a separate read-only database. In this way, by checking the final outcome, you can demonstrate that data has not been tampered;
- **Data API builder**: dotnet tool that generates CRUD APIS (Rest or GraphQL) for a table on the Azure Database. It also handles pagination, authentication, filtering...
- **Hyperscale**: SQL engine used to perform queries on distributed databases. Data is also stored in-memory for faster access.
