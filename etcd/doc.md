# etcd Fault Scenarios

This directory contains common fault scenarios related to etcd.

## Crash when joining nodes to the cluster [[Issue #123]](https://github.com/yourusername/yourrepository/issues/123)

**Summary**  
When multiple nodes are joined simultaneously, all but one node crashes. Introducing a 5-second delay between joins usually prevents crashes but not always.

**Symptoms**  

* Reports timeout or connection refused.
* Simultaneous joins cause crashes, but re-running the join may succeed.

**Root Cause**  

This appears to be a timing bug or race condition, potentially due to aggressive IO timeouts. Nodes give up after a few hundred milliseconds of trying.

**Fault Scenario**

Multiple nodes restart simultaneously.


**Workload**

None

**Version**

v0.4.0


