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


###  Updates lost due to concurrent crashes losing updates due to concurrent crashes [[Reported by Jepsen]](https://jepsen.io/analyses/aerospike-3-99-0-3)

### Summary

During network partition tests in Aerospike 3.99.0.3, nonlinearizable operations were observed, leading to unexpected and erroneous read results after the partition was resolved. This issue appears to be related to how Aerospike handles write failures during network disruptions, especially in cases where operations are retried incorrectly.

### Symptoms

* Nonlinearizable histories with reads returning impossible values.

* Reads reflecting values that were never successfully written (e.g., a key unexpectedly reads as "4" after a partition, despite no write of "4" succeeding).

### Root Cause

The issue stems from Aerospike’s retry logic in its clustering algorithm. When network failures cause writes to fail, Aerospike retries the operation. However, this retry mechanism may result in a misleading error code (e.g., :unavailable), causing subsequent reads to reflect values from failed writes rather than the latest consistent state. This incorrect handling of retries leads to unsafe effects, as non-idempotent operations can be repeated and yield unexpected results.

### Fault Type



### Version

3.99.0.3
