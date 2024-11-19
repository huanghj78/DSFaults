# MySQL-Cluster Fault Scenarios

This directory contains common fault scenarios related to [MySQL-Cluster](https://github.com/mysql/mysql-server).

##  SEGV cased by nullptr after a series of reconnection timeouts in MySQL-Cluster breaks down multiple nodes [[Reported by Chronos]](https://ieeexplore.ieee.org/document/10646793)

### Summary
The MySQL node will enter "check_and_report" function when errors occur without any check inside. If the errors recover just after it enter the "check_and_report" function, it will clean up the diagnostic report pointer(*da) so that the report function using this pointer may cause a SEGV fault.

### Symptoms

* The node will cause a SEGV fault.

### Root Cause

The bug can only be triggered if the network connection is instable so that some nodes lost connection but soon reconnect repeatedly. When errors occur, the system will report the error. If the node recovers just at that moment, it will clean the diagnostic report pointer(*da) and cause a null pointer access fault.

### Fault Type

Delay


