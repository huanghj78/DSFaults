# Zookeeper Fault Scenarios

This directory contains common fault scenarios related to [zookeeper](https://github.com/apache/zookeeper).


## Zookeeper service becomes unavailable when leader fails to write transaction log [[Issue #2247]](https://issues.apache.org/jira/browse/ZOOKEEPER-2247)

**Summary**

Zookeeper service becomes unavailable when leader fails to write transaction log. 

**Symptoms**

After this exception Leader server still remains leader. After this non recoverable exception the leader should go down and let other followers become leader.

**Root Cause**

The problem is because quorum is not being shutdown along with other services. We should also call shutdown on org.apache.zookeeper.server.quorum.QuorumPeer.

**Fault Scenario**

The issue is triggered when the leader fails to write transaction log due to an IO exception. 

**Workload**

write


**Version**

3.5.0



## Leader swallows the ZooKeeperServer.State.ERROR from Leader.LearnerCnxAcceptor in some concurrency condition [[Issue #4203]](https://issues.apache.org/jira/browse/ZOOKEEPER-4203)

**Summary**

A concurrency issue causes the ZooKeeper leader to not accept followers after a LearnerCnxAcceptor exception.

**Symptoms**

The cluster becomes unavailable as the leader fails to accept any followers, leading to continuous join attempts by followers without success.

**Root Cause**

The issue arises because the exception handling in the Leader.LearnerCnxAcceptor thread does not effectively manage the error state, preventing the leader from detecting it and transitioning to a proper state.

**Fault Scenario**

When a ZooKeeper cluster of 3 nodes is started within a 2-second window, the ServerSocket#accept invocation throws an exception in the LearnerCnxAcceptorHandler for the second follower attempting to join the quorum. 


**Workload**

None


**Version**

3.6.2