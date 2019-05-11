# High-availability service {#concept_tph_vbv_tdb .concept}

The high-availability service consists of several modules including the Detection, Repair, and Notification modules. In combination, these modules guarantee the availability of the data link service and process any internal database exception.

In addition, RDS can improve the performance of its high-availability service by migrating instances to a region that supports multi-zone instances and by adopting the appropriate high-availability policies.

## Detection {#section_ngf_xbv_tdb .section}

The Detection module checks whether the master and slave nodes of the DB engine are providing their services normally. The HA node uses heartbeat information, acquired at an interval of 8 to 10 seconds, to determine the health status of the master node. This information, combined with the health status of the slave node and heartbeat information from other HA nodes, allows the Detection module to eliminate any risk of judgements caused by exceptions such as network jitter. As a result, a failover can be completed within 30 seconds.

## Repair {#section_ogf_xbv_tdb .section}

The Repair module maintains the replication relationship between the master and slave nodes of the DB engine. It can also repair any errors that may occur at either node.

For example:

-   Automatic restoration of master/slave replication in case of an unexpected disconnection
-   Automatic repair of table-level damage to either node
-   On-site saving and automatic repair in case of crashes

## Notice {#section_qgf_xbv_tdb .section}

The Notice module informs the SLB or Proxy of status changes to the master and slave nodes to guarantee that you always access the correct node.

For example, the Detection module discovers that the master node has an exception and instructs the Repair module to fix it. If the Repair module fails to resolve the problem, the Notice module will be informed of this information. The Notice module then forwards the failover request to the SLB or Proxy module, which begins to redirect all traffic to the slave node. At the same time, the Repair module creates a new slave node on another physical server and synchronizes this change back to the Detection module. The Detection module starts to recheck the health status of the instance.

