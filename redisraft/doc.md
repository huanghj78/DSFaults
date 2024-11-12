# Redisraft Fault Scenarios

This directory contains common fault scenarios related to [redisraft](https://github.com/RedisLabs/redisraft).

## Total data loss on failover [[Issue #14]](https://github.com/RedisLabs/redisraft/issues/14)

### Summary

This issue describes a critical bug in Redis and Redisraft, where every failover results in the complete loss of all data in the cluster. This occurs due to various events, including leader elections and node failures.

### Symptoms

The primary symptom is the total loss of all keys in the cluster after failover events, even when commands have been successfully executed by the leader.

### Root Cause

The root cause of the issue is a missing re-entrancy check when applying commands to Redis, which causes commands to be sent again to the Raft log instead of being applied to the state machine.

### Fault Scenario

The fault scenario includes sporadic leader elections, pausing or killing nodes, and network partitions, all leading to data loss during failover.

### Workload

The workload involves multiple set commands being executed on a Redis instance, which triggers leader elections and results in data inconsistency.


### Version

The issue occurs in Redis version f88f866 and Redisraft version 1b3fbf6. It is confirmed to be fixed as of commit d589127.

## Possible lost updates with partitions and membership changes [[Issue #17]](https://github.com/RedisLabs/redisraft/issues/17)

### Summary

This issue reports potential data loss during membership changes in a Redis cluster when a network partition occurs. It details how updates can be lost if a leader node is isolated while other nodes are making changes, leading to inconsistencies.

### Symptoms

Data loss of updates during network partitions and membership changes, resulting in scenarios where nodes believe they have the most recent data when they do not.

### Root Cause

The issue appears to stem from the joint consensus mechanism for membership changes, allowing a leader to declare a change complete without adequately communicating that change to other nodes, which can lead to split-brain scenarios.

### Fault Scenario
Triggered during a network partition where a node is isolated while membership changes are occurring, specifically when nodes are removed or added to the cluster while the leader is unaware of its isolation.

### Workload

Workload involved appending data to keys in the Redis database during the test, specifically using the append command under conditions of partition and membership changes.

### Version

None

## Transient empty values on process restart [[Issue #18]](https://github.com/RedisLabs/redisraft/issues/18)

### Summary

This issue describes a problem in the redis-raft implementation where processes returning empty reads upon crashing and restarting leads to inconsistencies in the data served.

### Symptoms

The primary symptom is the occurrence of empty reads (e.g., returning [] instead of the expected values) from the database after nodes are killed and restarted.

### Root Cause

The root cause is related to the initialization process of Redis after a crash, specifically the timing of requests being served before the Raft protocol's initialization has completed.

### Fault Scenario

The issue is triggered when all nodes in the cluster are killed and then restarted, followed by additional node terminations leading to a majority being down.

### Workload

The workload that triggers this issue includes operations involving appending data to keys.


### Version

The issue was identified in version redis f88f866 and redisraft d589127, with further testing showing similar behavior in subsequent versions.


