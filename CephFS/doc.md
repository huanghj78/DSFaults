# CephFS Fault Scenarios

This directory contains common fault scenarios related to [CephFS](https://github.com/ceph/ceph).

## Data inconsistency under concurrent access by two clients [[Reported by MONARCH]](https://ieeexplore.ieee.org/document/10646793)

### Summary
When the server receives a chmod request on inode A from client 1, it creates a projected inode inode A′, applies a per-inode exclusive lock authlock to and modifies permissions on inode A′. Subsequently, both clients send stat requests simultaneously. As client 1 retains the lock, it can access inode A′ with updated metadata. However, client 2 retrieves outdated metadata of inode A after failing to get the authlock instead of waiting for the authlock. Thus, two clients see inconsistent metadata of file A at the same time.

### Symptoms

* Data inconsistency

### Root Cause

This bug happens due to a flawed logic design; specifically, when two clients send stat requests simultaneously, the client fails to get the authlock will directly retrieves outdated metadata instead of waiting for the authlock.

### Fault Type

Concurrenct request


