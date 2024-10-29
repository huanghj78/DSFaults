# Dqlite Fault Scenarios

This directory contains common fault scenarios related to [Dqlite](https://github.com/canonical/dqlite).

## LXD start up loop trying to connect to dqlite after loss of quorum [[Issue #323]](https://github.com/canonical/dqlite/issues/323)


**Summary**  

When two members of a 4-member cluster are stopped concurrently. Due to the loss of quorum, the remaining members are unable to hand over their roles properly. When attempting to start one of the stopped members, dqlite fails to start on that member, entering a startup loop and preventing proper recovery.




**Symptoms**  
Cluster becomes unavailabe.


**Root Cause**  
[Issue #234](https://github.com/canonical/raft/issues/234)


**Fault Scenario**

Node crash and restart.

**Workload**

None


**Version**

None


