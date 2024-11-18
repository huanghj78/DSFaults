# Braft Fault Scenarios

This directory contains common fault scenarios related to [Braft](https://github.com/baidu/braft).

## Leak memory of the server when killed before its status becomes running [[Reported by MALLORY]](https://arxiv.org/pdf/2305.02601)

### Summary
When the server is resumed (after a pause), only to become coincidentally isolated from the cluster due to a network partition, resulting in a failed start. Hence, the server crashes without the chance to release the memory allocated because the allocated memory can only be released when the process is in the running status.

### Symptoms

* Leak memory of the server

### Root Cause

This bug happens due to a flawed logic design; specifically, the allocated memory can only be released when the process is in the running status, and the allocated memory cannot be released before running.

### Fault Type

Node pause and network partition


