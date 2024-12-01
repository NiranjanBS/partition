# Partitioning
## What is partition?
* Data partition refers to the process of dividing a dataset into smaller, more manageable pieces or chunks called _**partitions/sharding**_.
* Having multiple copy of data on different nodes _replication_ is not sufficient, for very large datasets or very high query throughput.
* We need to break data in to partitions.
* Partitioning is usually combined with replication so that copies of each partition are stored on multiple nodes.
  * Gives Fault tolerance.
  ### Terminological confusion
  * What we call a _partition_ here is called a _shard_ in MongoDB, Elasticsearch,and SolrCloud;
  * it’s known as a _region_ in HBase, a _tablet_ in Bigtable,
  * a _vnode_ in Cassandra and Riak,
  * and a _vBucket_ in Couchbase.
  * However, _partitioning_ is the most established term, so we’ll stick with that.
## Different approaches to partitioning large dataset.
Say you have a large amount of data, and you want to partition it. How do you decide which records to store on which nodes?
#### Partitioning of key value data.
#### Partitioning by key range.
#### Partitioning by hash of key.

## How database routes request to right partition.
On a high level there are few approaches.
* Client can contact any node in the cluster, if that cluster has the data it serves otherwise it routes the request to next node and return the data.
* Send the request from client to **_routing tier (Colud proxy)_**, which determines when node the request to be forwarded to. Routing tier acts as partition aware load balancer.
* Require that client is aware of the partitioning and the assignment of partitions to nodes. In this case client can connect directly to the appropriate node, without any intemediary.
* ![image](https://github.com/user-attachments/assets/521d1cc1-c3a9-4207-8112-580871ea77f2)

## Partition rebalancing when a node is added or removed from cluster. 
## Role of zookeeper.
* Many distributed data systems rely on a separate coordination service such as Zoo‐Keeper to keep track of this cluster metadata, as illustrated in Figure below.
* Each node registers itself in ZooKeeper, and ZooKeeper maintains the authoritative mapping of partitions to nodes.
* Other actors, such as the routing tier or the partitioning-aware client, can subscribe to this information in ZooKeeper.
* Whenever a partition changes ownership, or a node is added or removed, ZooKeeper notifies the routing tier so that it can keep its routing information up to date.
![image](https://github.com/user-attachments/assets/2ed9b265-f438-45c8-a9b2-5ba5a01e78d7)
## Rebalancing Partitions.
## How indexing of data interact with partition.
## Partitioning and secondary indexing.

