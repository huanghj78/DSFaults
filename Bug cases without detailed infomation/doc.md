# Bug cases without detailed information

This directory contains some bug cases in some papers withou detailed information.



| Issue   | Fault Scenario | Fault Type |  Subject  |
|----------|----------|----------|--------|
| [MALLORY #1](https://arxiv.org/pdf/2305.02601)    | Read stale data after a newly written update is visible to others    |     |   Braft  |
| [MALLORY #3](https://arxiv.org/pdf/2305.02601)    | Two leaders are elected at the same term due to split votes    |     |   Dqlite  |
| [MALLORY #4](https://arxiv.org/pdf/2305.02601)    | No leader is elected in a healthy cluster with an even number of nodes    |     |   Dqlite  |
| [MALLORY #5](https://arxiv.org/pdf/2305.02601)    | A node reads dirty data that is modified but not committed by another node    |     |   Dqlite  |
| [MALLORY #6](https://arxiv.org/pdf/2305.02601)    | Lose write updates due to split brain    |     |   Dqlite  |
| [MALLORY #7](https://arxiv.org/pdf/2305.02601)    | A null pointer is dereferenced due to missing the pending configuration    |     |   Dqlite  |
| [MALLORY #8](https://arxiv.org/pdf/2305.02601)    | Leak allocated memory when failing to extend entries    |     |   Dqlite  |
| [MALLORY #9](https://arxiv.org/pdf/2305.02601)    | Buffer overflow happens while restoring a snapshot    |     |   Dqlite  |
| [MALLORY #10](https://arxiv.org/pdf/2305.02601)    | A node has an extra online spare    |     |   Dqlite  |
| [MALLORY #12](https://arxiv.org/pdf/2305.02601)    | Not repeatable read due to missing the local write update    |     |   MongoDB  |
| [MALLORY #13](https://arxiv.org/pdf/2305.02601)    | Not read committed due to missing the newly written update    |     |   MongoDB  |
| [MALLORY #14](https://arxiv.org/pdf/2305.02601)    | Read stale data after new data is written to the same key    |     |   Redis  |
| [MALLORY #15](https://arxiv.org/pdf/2305.02601)    | Buffer overflow due to writing data to a wrong data structure    |     |   Redis  |
| [MALLORY #16](https://arxiv.org/pdf/2305.02601)    | Runtime panic on initializing a cluster due to database version mismatch    |     |   Redis  |
| [MALLORY #17](https://arxiv.org/pdf/2305.02601)    | No leader is elected for a long time in a healthy cluster    |     |   TiKV  |
| [MALLORY #18](https://arxiv.org/pdf/2305.02601)    | Lose write updates due to split brain    |     |   TiKV  |
| [MALLORY #19](https://arxiv.org/pdf/2305.02601)    | Runtime fatal error when one server cannot get context before the deadline    |     |   TiKV  |
| [MALLORY #20](https://arxiv.org/pdf/2305.02601)    | Runtime fatal error in a server when the placement driver is killed    |     |   TiKV  |
| [MALLORY #21](https://arxiv.org/pdf/2305.02601)    | Runtime fatal error when failing to update max timestamp for the region    |     |   TiKV  |
| [MALLORY #22](https://arxiv.org/pdf/2305.02601)    | Monotonic time jumps back at runtime    |     |   TiKV  |
| [Chronos #2](https://ieeexplore.ieee.org/document/10646793)    |  SIGSEGV in NIOServerCnxnFactory when follower nodes create plenty of reconnections after timeouts.    |     |   ZooKeeper  |
| [Chronos #3](https://ieeexplore.ieee.org/document/10646793)    |  Endless EOF Exception in ”loadDataBase” after resource request timeouts, leading to service blocking    |     |   ZooKeeper  |
| [Chronos #4](https://ieeexplore.ieee.org/document/10646793)    |  The leader node breaks down when trying reconnection in SocketNIO after constant timeout exceptions.    |     |   ZooKeeper  |
| [Chronos #5](https://ieeexplore.ieee.org/document/10646793)    |   The following node repeatedly throws EndOfStreamException, stop reading data from the master node.    |     |   ZooKeeper  |
| [Chronos #7](https://ieeexplore.ieee.org/document/10646793)    |   SEGV in sql_executor caused by error pointer manipulating in timeout handling crashes MySQL server node.   |     |   MySQL-Cluster  |
| [Chronos #8](https://ieeexplore.ieee.org/document/10646793)    |   SQL selection process is blocked after handling various communication timeouts in the network.   |     |   MySQL-Cluster  |
| [Chronos #9](https://ieeexplore.ieee.org/document/10646793)    |    Server node crashes down when connection timeout during the data syncing and validation process.   |     |   MySQL-Cluster  |
| [Chronos #10](https://ieeexplore.ieee.org/document/10646793)    |    Heap-buffer-overflow occurs in ”Item read” after recovering from the direct communication timeouts.   |     |   MySQL-Cluster  |
| [Chronos #11](https://ieeexplore.ieee.org/document/10646793)    |    SEVG in SQL planer after triggering a series of timeout mechanisms when accessing the local database.   |     |   MySQL-Cluster  |
| [Chronos #12](https://ieeexplore.ieee.org/document/10646793)    |    Heap-buffer-overflow happens when dealing with various timeout SQL results in the union process.   |     |   MySQL-Cluster  |
| [Chronos #13](https://ieeexplore.ieee.org/document/10646793)    |    Frequent timeouts in the transaction syncing process hangs the server which stops the SQL execution.   |     |   MySQL-Cluster  |
| [Chronos #14](https://ieeexplore.ieee.org/document/10646793)    |     Constant timeout requests from other nodes keep blocking SQL optimizer and stop handling SQL queries.   |     |   MySQL-Cluster  |
| [Chronos #15](https://ieeexplore.ieee.org/document/10646793)    |     SEGV in SQL optimizer when handling timeout SQL queries after multiple reconnections from the network.   |     |   MySQL-Cluster  |
| [Chronos #16](https://ieeexplore.ieee.org/document/10646793)    |    Repeated timeout error in ”item subselect” crash down the MySQL server node and cannot be recovered.   |     |   MySQL-Cluster  |
| [Chronos #17](https://ieeexplore.ieee.org/document/10646793)    |    SEGV occurs after packet timeouts when the master node dispatches commands to other slave nodes.   |     |   MySQL-Cluster  |
| [Chronos #18](https://ieeexplore.ieee.org/document/10646793)    |    SEGV in data syncing process after multiple request timeouts and retry, breaking down the server nodes.   |     |   MySQL-Cluster  |
| [Chronos #19](https://ieeexplore.ieee.org/document/10646793)    |     Memory leak in ”buf block init”, hanging the server after plenty of SQL requests timeouts.   |     |   MySQL-Cluster  |
| [Chronos #20](https://ieeexplore.ieee.org/document/10646793)    |      The AsyncDispather thread is interrupted due to timeout connections and the RM cannot be contacted.   |     |   HDFS  |
| [Chronos #21](https://ieeexplore.ieee.org/document/10646793)    |      The IPC call is interrupted and the RM no long gives any response to the datanode after multiple timeouts.   |     |   HDFS  |
| [Chronos #22](https://ieeexplore.ieee.org/document/10646793)    |      Yarn gets stuck and repeated throw exceptions during the runtime due to timeouts in sending packets to RM.   |     |   HDFS  |
| [Chronos #23](https://ieeexplore.ieee.org/document/10646793)    |       Namenode tries to delete a container that has already been deleted in cleanup process after request timeouts.    |     |   HDFS  |
| [Chronos #24](https://ieeexplore.ieee.org/document/10646793)    |      A deadlock occurs and the MapReduce is rejected to execute when datanode throws a timeout exception.   |     |   HDFS  |
| [Chronos #25](https://ieeexplore.ieee.org/document/10646793)    |        Service hang when Socket is reset and the executing task cannot finish in time after multiple timeouts.    |     |   HDFS  |
| [Chronos #26](https://ieeexplore.ieee.org/document/10646793)    |       Serial of timeout messages cause panic in the ”Full sync process ”, and break down Ethereum nodes.   |     |   Go-Ethereum  |
| [Chronos #27](https://ieeexplore.ieee.org/document/10646793)    |         Repeated timeouts in BlockHeader syncing hang the message queue and stop transaction handling process.    |     |   Go-Ethereum  |