## Cassandra
- Non-relational database (NoSQL)
	- Mix between key-value store and column database
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

### CQL
- Cassandra Query Language
- Similar to SQL in terms of syntax
- All statements end with a semicolon

### SSTables
