# Davide's notes

👋 Welcome to your new my personal notes, powered by Foam!

The repository can be found on [GitHub](https://github.com/bellons91/personal-notes).

## Most important sections

- Azure Certifications
  - [[az-900]]
  - [[az-204]]

## Quick notes

- **Parquet**: data format used by Apache Spark; data is stored in columns, and not in rows. Can be queried using tools like Parquet Explorer in Visual Studio.
- **Password spray**: hacking technique. You try the most common passwords on multiple accounts, trying to find an account that used that password;
- **SIM-jacking**: vulnerability that uses SIMs and SMS content;
- **Hammering**: hacking technique. Hackers send continuous push notifications until the victim, annoyed by these notifications, accepts one and gives permissions to the intruder;
- **Adversary-in-the-middle**: deceive users;
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
- **IPAM (IP Address Management)**: technology and networking practice that involves planning, tracking, and managing IP address space within a network. It centralizes the administration of network addresses, ensuring efficient allocation, preventing conflicts, and often integrating with systems like DHCP and DNS to streamline network operations.
- **DHCP (Dynamic Host Configuration Protocol)**: a network management protocol used to automate the setup of devices on IP networks. It dynamically assigns IP addresses and other critical network configuration parameters (such as subnet mask, default gateway, and DNS servers) to devices, simplifying network administration and ensuring efficient address utilization.
- **AGC (Azure Gateway for Containers)**: specialized use of the Azure Application Gateway designed to serve containerized environments. AGC is tailored to handle container traffic by efficiently routing, load balancing, and securing web requests to your containerized applications. It allows for features like path-based routing, SSL termination, and integration with container orchestration platforms, ensuring that modern, microservices-based apps have a reliable and secure entry point into the network. [docs](https://learn.microsoft.com/en-us/azure/aks/advanced-container-networking-services-overview).
- **Azure Managed Grafana**: istanza di Grafana gestita da Azure (a pagamento)
- Azure functions
  - will have Host Initialization Failures stored on AppInsights (instead of on the shell)
  - OTel support
  - Flex Consumption Plan: allows flexibility, private networking, and has pay-per-use license.
  - Can be deployed using Azure Container Apps
- **Durable Task Scheduler**
  - GA in Nov 2025
  - A different backend environment for running durable functions.
  - It's a configuration - the operational code does not change
  - Distributed traffic
- **M.E.AI**: .NET library to integrate AI specifying the model;
  - Can save prompt templates in `.prompt` files, using placeholders. The Source Generator generates a class for them, and asks you to fill in the placeholders as they were input parameters.
- **Hoptimator**: [open-source platform created by LinkedIn](https://www.linkedin.com/blog/engineering/data-streaming-processing/declarative-data-pipelines-with-hoptimator) to manage multi-hop data pipelines.
- **OWL (Web Ontology Language)**: Structured approach to define semantics and relationships between objects. [Link](https://en.wikipedia.org/wiki/Web_Ontology_Language).
- **RDFS (Resource Description Framework Schema)**: set of classes with certain properties using the RDF extensible knowledge representation data model, providing basic elements for the description of ontologies. [Link](https://en.wikipedia.org/wiki/RDF_Schema)
