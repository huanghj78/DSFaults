# DSFaults
Distributed Systems Fault Scenarios

This project collects and analyzes common failure scenarios in distributed systems, especially distributed databases. 

## Databases

### etcd
You'll find fault scenarios and analyses related to etcd in [etcd](./etcd/doc.md).

### Dqlite
You'll find fault scenarios and analyses related to Dqlite in [Dqlite](./dqlite/doc.md).

### redisraft
You'll find fault scenarios and analyses related to RedisRaft in [redisraft](./redisraft/doc.md).

### zookeeper
You'll find fault scenarios and analyses related to Zookeeper in [zookeeper](./zookeeper/doc.md).

## Overview

| Issue   | Description | Fault Scenario | 
|----------|----------|----------|
| ZK-2247    | Zookeeper service becomes unavailable when leader fails to write transaction log    |  IO exception   |
| ZK-4203   | Leader swallows the ZooKeeperServer.State.ERROR from Leader.LearnerCnxAcceptor in some concurrency condition   | Restart, IO exception   | 
| ET-716    | Crash when joining nodes to the cluster  | Multiple nodes restart simultaneously   | 
| ET-828    | Incorrect behavior under network partition  | Network partition   | 
| DQ-323|LXD start up loop trying to connect to dqlite after loss of quorum|Node crash and restart|
| DQ-324|LXD dqlite crash removing member of cluster|Node removal|
|RR-14|Total data loss on failover|Node crash or network partition|
|RR-17|Possible lost updates with partitions and membership changes|Network partition|

