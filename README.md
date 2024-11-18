# DSFaults
Distributed Systems Fault Scenarios

This project collects and analyzes common failure scenarios in distributed systems, especially distributed databases. 

## Analyses

### [Aerospike](./Aerospike/doc.md).

# [Chronos](./chronos/doc.md).

# [Crate](./Crate/doc.md).

### [CephFS](./CephFS/doc.md).

### [Etcd](./etcd/doc.md).

### [Dqlite](./dqlite/doc.md).

### [Redisraft](./redisraft/doc.md).

### [Zookeeper](./zookeeper/doc.md).

### [Redis](./redis/doc.md).

## Overview

| Issue   | Fault Scenario | Fault Type | 
|----------|----------|----------|
| [ZK-2247](./zookeeper/doc.md#zookeeper-service-becomes-unavailable-when-leader-fails-to-write-transaction-log-issue-2247)    | Zookeeper service becomes unavailable when leader fails to write transaction log    |  IO exception   |
| [ZK-4203](./zookeeper/doc.md#leader-swallows-the-zookeeperserverstateerror-from-leaderlearnercnxacceptor-in-some-concurrency-condition-issue-4203)   | Leader swallows the ZooKeeperServer.State.ERROR from Leader.LearnerCnxAcceptor in some concurrency condition   | Restart, IO exception   | 
| [ET-716](./etcd/doc.md#crash-when-joining-nodes-to-the-cluster-issue-716)    | Crash when joining nodes to the cluster  | Multiple nodes restart simultaneously   | 
| [ET-828](./etcd/doc.md#incorrect-behavior-under-network-partition-issue-828)    | Incorrect behavior under network partition  | Network partition   | 
| [DQ-323](./dqlite/doc.md#lxd-start-up-loop-trying-to-connect-to-dqlite-after-loss-of-quorum-issue-323) |LXD start up loop trying to connect to dqlite after loss of quorum|Node crash and restart|
| [DQ-324](./dqlite/doc.md#lxd-dqlite-crash-removing-member-of-cluster-issue-324) |LXD dqlite crash removing member of cluster|Node removal|
|[RR-14](./redisraft/doc.md#total-data-loss-on-failover-issue-14) |Total data loss on failover|Node crash or network partition|
|[RR-17](./redisraft/doc.md#possible-lost-updates-with-partitions-and-membership-changes-issue-17) |Possible lost updates with partitions and membership changes|Network partition|
|[RD-9688](./redis/doc.md#unbounded-memory-usage-by-cluster-bus-link-buffers-in-face-of-asymmetric-network-partition-issue-9688) |Unbounded memory usage by cluster bus link buffers in face of asymmetric network partition|Network loss|
|[RD-13018](./redis/doc.md#preventing-temporary-circular-replication-and-slot-loss-in-redis-cluster-failover-issue-13018) |Preventing Temporary Circular Replication and Slot Loss in Redis Cluster Failover |Network partition|
|[Ae-1](./Aerospike/doc.md#dirty-reads-after-partitions-reported-by-jepsen)|Dirty Reads After Partitions|Network partition and node crash|
|[Ae-2](./Aerospike/doc.md#cluster-unavaliable-after-nodes-crash-and-restart-reported-by-jepsen)|Cluster unavaliable after nodes crash and restart|Node crash and restart|
|[Ae-3](./Aerospike/doc.md#updates-lost-due-to-concurrent-crashes-reported-by-jepsen)|Updates lost due to concurrent crashes|Concurrent node crash|
|[Ch-511](./chronos/doc.md#jobs-dont-run-when-a-network-partition-occurs--issue-511)|Jobs don't run when a network partition occurs|Network parition|
|[Cr-3711](./Crate/doc.md#_version-does-not-uniquely-identify-a-particular-version-of-a-row-issue-3711)|Inconsistent Row Values in CrateDB During Network Partition with Identical _version Numbers|Network partition|

## Paper
* Efficient Exposure of Partial Failure Bugs in Distributed Systems with Inferred Abstract States
* Greybox Fuzzing of Distributed Systems
* Chronos: Finding Timeout Bugs in Practical Distributed Systems by Deep-Priority Fuzzing with Transient Delay
* Coverage Guided Fault Injection for Cloud Systems
* CoFI: Consistency-Guided Fault Injection for Cloud Systems
* Phoenix: Detect and Locate Resilience Issues in Blockchain via Context-Sensitive Chaos
* Efficient Reproduction of Fault-Induced Failures in Distributed Systems with Feedback-Driven Fault Injection

## Report
* [https://jepsen.io/analyses](https://jepsen.io/analyses)
