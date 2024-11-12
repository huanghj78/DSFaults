# Crate Fault Scenarios

This directory contains common fault scenarios related to [Crate](https://github.com/crate/crate/).

## Inconsistent Row Values in CrateDB During Network Partition with Identical _version Numbers [[Issue #3711]](https://github.com/crate/crate/issues/3711)


### Summary
This issue highlights an inconsistency in CrateDB where concurrent updates during a network partition can lead to different values being returned for the same _version of a row, violating expected behavior of version consistency. This occurs when multiple clients attempt concurrent updates and reads of the same row in a five-node CrateDB cluster partitioned in an overlapping ring topology.

### Symptoms

Primary-key reads returning different value entries for the same _version.

### Root Cause
The root cause lies in CrateDB’s reliance on an underlying Elasticsearch versioning system where _version does not reliably indicate unique row states under network partitions. CrateDB inherits this limitation from Elasticsearch, where _version fails to account for concurrent modifications, leading to version divergence.

### Fault Type
A ~200-second network partition isolates each node from two neighbors in a ring topology, causing CrateDB to enter a split-brain scenario, which results in divergent _version values.

### Workload
Concurrent updates and reads on a single row by five clients (each bound to a different cluster node) during the partition, causing inconsistencies in _version integrity.

### Version
0.54.9