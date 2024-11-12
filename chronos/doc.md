# Chronos Fault Scenarios

This directory contains common fault scenarios related to [Chronos](https://github.com/mesos/chronos/).

## Jobs don't run when a network partition occurs  [[Issue #511]](https://github.com/mesos/chronos/issues/511)

### Summary
Chronos fails to execute scheduled tasks when a complete network partition divides the Mesos cluster in half. During this partition, tasks enqueued before, during, or after the failure experience significant scheduling delays or are not executed at all. After network healing, Chronos does not resume task scheduling as expected, and some Chronos nodes become permanently unresponsive.

### Symptoms 

* Tasks fail to meet scheduling demands across various stages of partitioning.
* Some Chronos nodes refuse connections for the remainder of the test after partition events.
* Cluster accepts new jobs but fails to process them correctly after network healing.


### Root Cause
The Mesos slaves fail to detect a new master after the network heals. This is potentially due to a timeout in the registry_fetch_timeout setting, causing issues in recovering the registry log among Mesos masters when reconnecting to Zookeeper.


### Fault Type

Complete network partition splits the cluster into isolated halves. 

### Workload

A series of jobs.


### Version

2.3.4-1.0.81.debian77
