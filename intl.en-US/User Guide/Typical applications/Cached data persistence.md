# Cached data persistence {#concept_xjd_glx_wdb .concept}

ApsaraDB RDS can be used together with ApsaraDB Memcache and Redis to form storage solutions with high throughput and low delay. This document describes the cached data persistence solution based on the combined use of RDS and Memcache.

## Background information {#section_nd4_dmx_wdb .section}

Compared with RDS, Memcache and Redis have the following features:

-   Quick response: The request delay of ApsaraDB Memcache and Redis is usually within several milliseconds.
-   The cache area supports a higher Queries Per Second \(QPS\) than RDS.

## System requirements {#section_b4s_qmx_wdb .section}

-   bmemcached \(with support for SASL extension\) has been installed in the local environment or ECS.

    bmemcached download address: Click [Here](https://github.com/jaysonsantos/python-binary-memcached) to download.

    The bmemcached installation command is as follows:

    ```
    pip install python-binary-memcached
    ```

-   Python is used as an example. Python and pip must be installed in the local environment or ECS.

## Sample code {#section_pt5_rmx_wdb .section}

The following sample code realizes the combined use of ApsaraDB RDS and Memcache:

```
/usr/bin/env python
import bmemcached
Memcache_client = bmemcached.Client((‘ip:port’), ‘user’, ‘passwd’)
#Search for a value in ApsaraDB Memcache
res = os.client.get(‘test’)
if res is not None:
    return res #Return the value found
else:
    #Query RDS if the value is not found
    res = mysql_client.fetchone(sql)
     Memcache_client.put(‘test’, res) #Write cached data to ApsaraDB for Memcache
    return res
```

