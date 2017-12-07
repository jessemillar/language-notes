## Cassandra
- Non-relational database (NoSQL)
	- Mix between key-value store and column database
- The DataStax company has Cassandra install bundles for community and enterprise and has some decent documentation
- Made to handle huge amounts of data
- Initially created at Facebook
	- Combination of Google Big Table and Amazon Dynamo
- Built for fast writes
- Ring-based replication
	- Simple Strategy
		- Doesn't take network topology into account
	- Network Topology Strategy
		- Across multiple datacenters
- Every node is the same
- You can read/write anywhere
- Chooses availability and partition tolerance over consistency
	- You can individually tune query consistency levels
- Runs on the JVM
- Any server can be queried (it acts as the coordinator)
	- You can only query by key (denormalize your data)
		- Don't relate columns or tables to other data; no joins
- Data hierarchy:
	1. Keyspace
	1. Table
	1. Partition
	1. Row
- When you run an `INSERT`, if that row already exists, it is updated
- If you want to be able to run a query similar to `SELECT * FROM users WHERE city='Boston'`, `city` must be defined as a primary key or index during table creation
	- `CREATE TABLE users(id uuid, name varchar, city varchar, PRIMARY KEY (id, city));`

### CQL
- Cassandra Query Language
- Similar to SQL in terms of syntax
- All statements end with a semicolon

### Write Process
- https://docs.datastax.com/en/cassandra/3.0/cassandra/dml/dmlHowDataWritten.html
- The general process of writing data is:
	1. Logs data to the commit log
	1. Writes data to the memtable
	1. Flushes data from the memtable
	1. Flushed into SSTables

### SSTables
- Compaction merges multiple SSTable files into a new one
- Immutable
- Don't get deleted, just have rows marked with a "tombstone"

### Definitions
- Sharding
	- A technique of breaking a big database into smaller pieces (called: Shards) and then running each piece on dedicated commodity hardware in a shared nothing architecture
- Primary Key
	- Indicates one or more columns used to retrieve data from a table
	- If more than one column is used (e.g. `PRIMARY KEY(key_part_one, key_part_two)`), the first part of the key (`key_part_one`) is the partition key and the second part of the key (`key_part_two`) is the clustering key
- Compound Keys
	- Includes the partition key (determines where node data is stored) and one or more additional columns that determine clustering
- Partition Key
	- One or more columns responsible for data distribution across your nodes
- Composite Key
	- One or more columns responsible for data sorting within the partition
- Clustering Key
- Flushing
	- Writing data from memtable into SSTables (disk)
