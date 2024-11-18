# Dqlite Fault Scenarios

This directory contains common fault scenarios related to [Dqlite](https://github.com/canonical/dqlite).

## LXD start up loop trying to connect to dqlite after loss of quorum [[Issue #323]](https://github.com/canonical/dqlite/issues/323)


### Summary

When two members of a 4-member cluster are stopped concurrently. Due to the loss of quorum, the remaining members are unable to hand over their roles properly. When attempting to start one of the stopped members, dqlite fails to start on that member, entering a startup loop and preventing proper recovery.




### Symptoms 
Cluster becomes unavailabe.


### Root Cause
[Issue #234](https://github.com/canonical/raft/issues/234)


### Fault Type

Node crash and restart.

### Workload

None


### Version

None


## LXD dqlite crash removing member of cluster [[Issue #324]](https://github.com/canonical/dqlite/issues/324)
### Summary  

This issue reports a crash in LXD when attempting to remove a member from a dqlite cluster, triggered by an assertion failure in the Raft implementation.

### Symptoms

The cluster becomes unstable, resulting in a crash during the member removal process and errors related to connection resets.


### Root Cause  

The root cause is an assertion failure in the Raft protocol implementation, specifically when handling the removal of a cluster member.

### Fault Type

The issue occurs during the operation of removing a member from the dqlite cluster, which leads to the crash.

### Workload

None


### Version

None

## Violate invariant as a segment cannot open while truncating inconsistent logs [[Reported by MALLORY]](https://arxiv.org/pdf/2305.02601)


### Summary
The cluster undergoes a sequence of environment faults, including a network partition (#{𝑆1, 𝑆2}, #{𝑆3, 𝑆4, 𝑆5}), leader 𝑆1 crashing, and network healing. As a result of these faults, server 𝑆2 ends up with conflicting entries with the leader 𝑆3, which must be removed. However, the conflicting entries are in a snapshot, which makes the removal fail.

### Symptoms

* Server become unavailable

### Root Cause

This bug happens due to a flawed logic design: it doesn't consider the log entry operation just after a snapshot (it will remove all current log).

### Fault Type

Node crashes and network partition


