# Aerospike Fault Scenarios

This directory contains common fault scenarios related to [Aerospike](https://aerospike.com/).

## Dirty Reads After Partitions [[Reported by Jepsen]](https://jepsen.io/analyses/aerospike-3-99-0-3)
### Summary

During network partition tests in Aerospike 3.99.0.3, nonlinearizable operations were observed, leading to unexpected and erroneous read results after the partition was resolved. This issue appears to be related to how Aerospike handles write failures during network disruptions, especially in cases where operations are retried incorrectly.

### Symptoms

* Nonlinearizable histories with reads returning impossible values.

* Reads reflecting values that were never successfully written (e.g., a key unexpectedly reads as "4" after a partition, despite no write of "4" succeeding).

### Root Cause

The issue stems from Aerospike’s retry logic in its clustering algorithm. When network failures cause writes to fail, Aerospike retries the operation. However, this retry mechanism may result in a misleading error code (e.g., :unavailable), causing subsequent reads to reflect values from failed writes rather than the latest consistent state. This incorrect handling of retries leads to unsafe effects, as non-idempotent operations can be repeated and yield unexpected results.

### Fault Type

Total network partitions between nodes.
During the partition, some nodes crash while others attempt to continue operations.
After the partition is resolved, certain read operations return values that are inconsistent with the intended linearizable history.
Workload

Operations include reads, writes, and compare-and-set on single registers.
Majority-minority partition testing, where total partitions are introduced during the workload.

### Version

3.99.0.3


## Cluster unavaliable after nodes crash and restart [[Reported by Jepsen]](https://jepsen.io/analyses/aerospike-3-99-0-3)

### Summary

An immediate problem arises when we crash Aerospike nodes with SIGKILL: the concurrent failure of replication-factor nodes takes down some fraction of the keyspace indefinitely. The cluster will not recover, even after nodes are restarted—some shards will remain down indefinitely.

### Symptoms

Cluster unavaliable

### Root Cause

None

### Fault Type

Node crash with SIGKILL

### Workload

None

### Version

3.99.0.3


##  Updates lost due to concurrent crashes [[Reported by Jepsen]](https://jepsen.io/analyses/aerospike-3-99-0-3)

### Summary

Aerospike 3.99.0.3 exhibited data loss, especially in cases where updates were only stored in memory and not yet written to disk. This data loss was exacerbated by concurrent crashes and the revival of dead shards. Aerospike’s asynchronous write policy, intended to boost performance, contributed to this issue by not persisting data to disk immediately, leading to missing records after failures.

### Symptoms

* Lost updates during concurrent node crashes and revive operations.
* Reads showing missing data, especially in tests involving multiple node restarts.
* Observed data loss and recovery ratios indicating missing records that were not stored on disk.


### Root Cause

The root cause of this issue lies in Aerospike’s design to acknowledge writes without first persisting them to disk, relying instead on memory and redundancy across nodes. When concurrent crashes occur, the unflushed in-memory writes are lost if all replicas for a record are down. Additionally, reviving dead shards prematurely can cause Aerospike to recognize stale data from previously failed nodes, leading to further loss of updates.

### Fault Type

Concurrent node crashes.

### Workload

Write-heavy workloads involving set operations.
Tests requiring node restarts, revives, and reclustering operations.

### Version

3.99.0.3
