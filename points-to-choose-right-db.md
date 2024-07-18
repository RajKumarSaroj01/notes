## How to Choose The Right Database for Your Application?


#### Capacity
#### CAP theorem
#### Number of DB connection
#### Read heavy or Write heavy query
#### Time of read and write query
#### Data Consistency Requirements
* Strong Consistency: Ensures that all clients always see the same data. Critical for applications where data accuracy is paramount, such as financial transactions. Example databases: PostgreSQL, MySQL with InnoDB.
* Eventual Consistency: Accepts temporary inconsistencies for better availability and partition tolerance. Suitable for applications like social media feeds. Example databases: Cassandra, Amazon DynamoDB.
#### Query more on primary key or secondary key
#### Horizontal & Vertical Scaling
#### Replication
#### New node spin up time and easyness
#### Sharding 
#### Concurrency Control
* Optimistic vs. Pessimistic Locking: Understand the database's approach to concurrency control. Optimistic locking is suitable for high-concurrency environments with infrequent conflicts, while pessimistic locking can be better for environments with frequent write conflicts.
* MVCC (Multi-Version Concurrency Control): Allows readers to access the previous state of data without blocking writers, improving performance in read-heavy workloads. Example databases: PostgreSQL, Oracle.
#### Row-Oriented vs. Column-Oriented Storage