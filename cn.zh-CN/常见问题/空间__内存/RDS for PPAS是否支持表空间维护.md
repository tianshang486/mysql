# RDS for PPAS是否支持表空间维护 {#concept_npf_zzn_hhb .concept}

当前RDS for PPAS不支持表空间的相关操作，主要是因为PPAS底层架构与Oracle不一样。

RDS for PPAS的默认表空间会随着可用空间自动伸缩，因此不需要像Oracle一样进行表空间的维护。

