# Redis Fault Scenarios

This directory contains common fault scenarios related to [redis](https://github.com/redis/redis).

## Unbounded memory usage by cluster bus link buffers in face of asymmetric network partition [[Issue #9688]](https://github.com/redis/redis/issues/9688)

### Summary  

This issue addresses a memory leak in Redis when operating under an asymmetric network partition scenario, where one primary node loses connectivity with another but maintains inbound connections. This leads to unbounded growth of send buffers, ultimately resulting in out-of-memory (OOM) errors.

### Symptoms

* Cluster becomes unavailable
* Out-of-memory (OOM) errors occur for clients
* Significant memory growth observed for cluster bus link buffers

### Root Cause

This appears to be a timing bug or race condition, potentially due to aggressive IO timeouts. Nodes give up after a few hundred milliseconds of trying.

### Fault Scenario

The fault is triggered during a one-way 100% packet loss from one primary node (P1) to another (P2) in a two-shard Redis cluster.


### Workload

The scenario typically involves a steady stream of PubSub messages being sent from P1 to P2.

### Version

None


## Preventing Temporary Circular Replication and Slot Loss in Redis Cluster Failover [[Issue #13018]](https://github.com/redis/redis/issues/13018)

### Summary  

This issue addresses a problem in Redis Cluster where, during a failover, certain nodes can enter an inconsistent state, leading to temporary circular replication and slot loss. The issue occurs when network latency or partitioning prevents nodes from updating each other about the current cluster state, resulting in nodes observing incorrect replication relationships and slot configurations.

### Symptoms

* Certain nodes in the Redis Cluster incorrectly recognize circular replication relationships.
* Slot loss occurs, causing some slots to be temporarily unassigned.
* The cluster state may go to FAIL, with clients unable to locate a primary node for specific slot ranges, potentially leading to local infinite loops in client requests.


### Root Cause 

The root cause lies in the delay or loss of PONG messages that communicate the cluster's updated replication state. This can result in observer nodes seeing an inconsistent intermediate state, which creates circular replication and leads to temporary slot loss. The problem stems from the lack of strong consistency in handling topology changes within the Redis Cluster.

### Fault Scenario

The fault occurs when a network latency or partition prevents a node’s state update message from reaching other nodes. Specifically, if a node fails to receive a PONG message indicating a replication role change, it may misinterpret the cluster state, resulting in an incorrect replication loop and slot loss.


### Workload

Manual failover operations under network partition conditions or high latency.

### Version

None