cassandra

- when to use 
    optimized for writes, rather than complex read patterns	
    no manual sharding and rebalancing 
- Quorum
    we set on each query level also    
- ACID 
	- tunable consistency
	- insert delete and update are AID    

- how the record getting stored internally 
	write comiit log, purged after data flushed in SSTables 
	write data in memtable,
	Flushing data from the memtable
	Storing data on disk in SSTables(like Btree or hash index storage data structure )
		 SSTables are maintained per table
		 partition is typically stored across multiple SSTable files
- how read operation
	gets the record from memtable and SSTables and return the record having latest version
	search in SSTable, first tries to get disk offset then record read operation 
		Bloom Filter(per SSTable)
		Key cache: stores the frequently used record
		Partition summary: groups the partition keys and stores
		Partition index:  full index list 
		SSTable
- CAP theorem---> AP
- collection data type
	list
	map
	set 
- number of nodes recommended
	5 node 3 replication factor, recommended
	3 node 2 replication factor, can be done but will put high stress during node failure
- routing 
	based on partition key,mandatory can be disabled on query, if not availble in query then full scan on each partition 
- bottleneck
    secondry index search 	
- replication
	- on different rack and different data center, to avoid disaster    
- memtable
	- in memory structure,one active per table 
	- each node as memtable
	- stores writes in a sorted order until reaching a configurable limit and then it is flushed
- SSTable
	- SSTable data files are immutable 
- deletion of data

- compaction SSTable
	- To improve read performance as well as to utilize disk space, Cassandra periodically does compaction to create & use new consolidated SSTable files instead of multiple old SSTables.
	- SizeTieredCompactionStrategy is designed for write-intensive workloads,similar-sized sstables(four by default),need more space  
	- LeveledCompactionStrategy for read-intensive workloads

- Read repair
	- to maintain consistency
	- once read done, compare the record from other replica ,if not same writes record in other replica
	- on each read call, yes, it's blocking process first checks the 	replica ,then read repair and then serve the client request	
- coordinater node
	- 	
- number of vnodes
	- 8 vnodes, recommended 
	- num_tokens default value 256.
	- can we increase the vnode post setup?
- Batching 
	- good for single partition queries
	- https://docs.datastax.com/en/dse/6.0/cql/cql/cql_using/useBatch.html
	- batching will reduce the network call but have some overhead on internall process
- Cassandra’s hard limit is 2 billion cells per partition
- SSTables max size 100MB	
- lightweight transaction , if block 	
- snitch
- dynamic snitch
- load balancing policies
	- token aware, round robin, latency aware 
    - by default load balancing 
		- token aware and round robin 
- new node added/node went down
	https://stackoverflow.com/questions/28836010/cassandra-data-redistribution-when-new-nodes-join
	https://www.datastax.com/blog/virtual-nodes-cassandra-12

- downtime on redistribution of token
- 
- AWS keyspaces
	- internally,  9 nodes 3 replication factor , multi AZ,https://docs.datastax.com/en/cassandra-oss/3.0/cassandra/dml/dmlTransactionsDiffer.html local_quorum 	
	- on demand mode: pay for only the reads and writes
	- provisioned mode: optimize the price by specifing the reads and writes per second
	-  Batch: unlogged batch commands with up to 30 commands in the batch. Only unconditional INSERT, UPDATE, or DELETE commands are permitted in a batch. Logged batches are not supported.	 
	- Cassandra’s settings for compaction, compression, caching, garbage collection, and bloom filtering are not applicable	
	- CQL query throughput
		- 3000(read)/1000(write) CQL per TCP connection per second
		- provides 9 peer ip address to drivers
		- means 3000*9 CQL per second
		- if want more increase the number of connection per peer ip
	- Supports range delete: upto 1000 rows in single operation 
	- You cannot update any column in the primary key because that would change the primary key for the record.	
	- Storage : automatically managed by aws 
	- ORDER BY : allowed only on clustering key 
	- QUERY page size: maximum size allowed is 1MB, if exceding will get less number of records 

how rebalancing happens when increase or decrease the node?
	Cassandra will automatically adjust the token ranges each node is responsible for resulting in each node in the cluster storing a smaller subset of the data.

one row in how many SSTable? worstcase on each sstable
one col in how many SSTable?

make point of below url
https://docs.datastax.com/en/cassandra-oss/3.0/cassandra/dml/dmlTransactionsDiffer.html

- size limit of partition : 100MB
- what will happen if two  table have same partiotion key : both will get same token
- how the hashing/token generated
- what will happens when we will reach 2 billions of limit :
	- create a table with new partition key and rehash the records 
	- Bucketing https://www.youtube.com/watch?v=pqf25DDAXdk
- 



https://medium.com/analytics-vidhya/15-reasons-of-read-latency-in-cassandra-8d965f18f85c
https://teddyma.gitbooks.io/learncassandra/content/client/read_requests.html

- when new nodes joins the cluster cassandra break the  vnode and assignes the part of token,from each existing node, to new nodes
- provides Atomicity, Isolation,  Durability 
    https://docs.datastax.com/en/cassandra-oss/3.0/cassandra/dml/dmlTransactionsDiffer.html
    
- BEST PRACTICE 
- http://mighty-titan.blogspot.com/2012/06/understanding-cassandras-consistency.html   
