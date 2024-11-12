# Etcd Fault Scenarios

This directory contains common fault scenarios related to [etcd](https://github.com/etcd-io/etcd).

## Crash when joining nodes to the cluster [[Issue #716]](https://github.com/etcd-io/etcd/issues/716)

### Summary
When multiple nodes are joined simultaneously, all but one node crashes. Introducing a 5-second delay between joins usually prevents crashes but not always.

### Symptoms

* Reports timeout or connection refused.
* Simultaneous joins cause crashes, but re-running the join may succeed.

### Root Cause

This appears to be a timing bug or race condition, potentially due to aggressive IO timeouts. Nodes give up after a few hundred milliseconds of trying.

### Fault Scenario

Multiple nodes restart simultaneously.


### Workload

None

### Version

v0.4.0


## Incorrect behavior under network partition [[Issue #828]](https://github.com/etcd-io/etcd/issues/828)

### Summary  

This issue discusses unexpected behavior in an etcd cluster during network partitions, leading to potential data conflicts when nodes mistakenly form a quorum.



### Symptoms  

The cluster exhibits inconsistent state, allowing write operations to occur even when a majority of nodes are unavailable, which can lead to conflicting values for the same key after a network partition is resolved.

### Root Cause

The root cause is the automatic adjustment of the cluster size when nodes are removed due to disconnection, which allows the cluster to continue accepting writes with insufficient quorum.

### Fault Scenario

The fault scenario involves a network partition where two subsets of nodes can communicate with each other while being isolated from the other subset, enabling both groups to accept changes.


### Workload

Set operation

### Version

None