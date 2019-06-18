# ST\_CheckGPU {#reference_lfr_mhn_qfb19 .reference}

This function checks whether a GPU is available in the current environment.

## Syntax {#section_og1_4hn_qfb .section}

```
text ST_CheckGPU();
```

## Parameters {#section_cxv_qhn_qfb .section}

This function checks whether a GPU can be identified in the current runtime environment.

## Examples {#section_lmw_qhn_qfb .section}

```
select st_checkgpu();
                                                                          
----------------------------------------------------------------------------------------
 [GPU prop]multiProcessorCount=20; sharedMemPerBlock=49152; maxThreadsPerBlock=1024
 
(1 row)
```

