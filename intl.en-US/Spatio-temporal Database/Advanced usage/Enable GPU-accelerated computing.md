# Enable GPU-accelerated computing {#concept_lkt_hkd_5gb .concept}

## Acceleration principles {#section_jsl_3kd_5gb .section}

Due to its special hardware architecture, a GPU has great advantages over a CPU in processing computing-intensive and easy-to-parallel code. In a database, GPU parallel acceleration is performed at the object level. Ganos converts a single field object to a model suitable for parallel computing, and uses the multiple cores of the GPU for parallel computing. The following figure shows the parallel computing process.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/124754/156620870038836_en-US.png)

## Precautions {#section_nfy_1nd_5gb .section}

A single GPU has limited resources. Therefore, we recommend that you disable GPU-accelerated computing in a session for high-concurrency scenarios.

## Procedure {#section_est_kkd_5gb .section}

When detecting a GPU, Ganos automatically enables GPU-accelerated computing. You do not need to set any parameters. GPU-accelerated computing is transparent and imperceptible to you. In addition, Ganos allows you to enable or disable GPU-accelerated computing at the session level.

1.  Check whether a GPU is available in the current environment.
    1.  Execute the create extension ganos\_raster cascade statement to create a Ganos Raster extension.
    2.  Execute the select st\_checkgpu\(\) statement.

        -   If Ganos detects a GPU in the current environment, it returns the GPU information.

            ``` {#codeblock_imv_lmq_5i3}
            rasterdb=# select st_checkgpu();
                                st_checkgpu                                                                                       
            ------------------------------------------------------------------------------------------------------------------------------
             [GPU(0) prop]multiProcessorCount=20; sharedMemPerBlock=49152; totalGlobalMem=-608239616; maxThreadsPerBlock=1024; maxThreadsPerMultiProcessor=2048; cudaThreadGetLimit=1024.
            (1 row)
            ```

        -   If Ganos does not detect a GPU in the current environment, it returns an error message.

            ``` {#codeblock_2ju_uo3_7zd}
            rasterdb=# select st_checkgpu();
                               st_checkgpu                                                                
            ------------------------------------------------------------------------------------------------------------------------------------------ 
            There is not gpu device on current environment, cuda_errorcode=35, errormsg=CUDA driver version is insufficient for CUDA runtime version.
            (1 row)
            ```

        **Note:** GPU-accelerated computing can be enabled only in an environment where a GPU is available.

2.  Enable or disable GPU-accelerated computing at the session level.
    -   In an environment with a GPU, Ganos enables GPU-accelerated computing by default. To disable GPU-accelerated computing to use the original CPU computing mode, perform the following operation in a session:

        Execute the set ganos.raster.use\_cuda=off statement.

        ``` {#codeblock_hp8_b7i_6uw}
        rasterdb=# set ganos.raster.use_cuda=off;
        SET
        rasterdb=# show ganos.raster.use_cuda;
         ganos.raster.use_cuda 
        -----------------------
         off
        (1 row)
        ```

    -   To enable GPU-accelerated computing again, execute the set ganos.raster.use\_cuda=on statement.

``` {#codeblock_gfh_ii6_iyo}
rasterdb=# set ganos.raster.use_cuda=on;
SET
rasterdb=# show ganos.raster.use_cuda;
 ganos.raster.use_cuda 
-----------------------
 on
(1 row)
```

3.  Implement GPU-accelerated computing in a Ganos module.

    **Note:** Currently, you can implement GPU-accelerated computing only in the Ganos Raster module. GPU-accelerated computing will be supported by the Ganos Trajectory and Ganos Geometry modules in the future.


