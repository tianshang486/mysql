# RDS for PostgreSQL使用中文分词 {#concept_266153 .concept}

## 启用中文分词 {#section_gq7_f0k_cba .section}

可以使用下面的命令，启用中文分词：

``` {#codeblock_4r1_et9_cp1}
CREATE EXTENSION zhparser;
CREATE TEXT SEARCH CONFIGURATION testzhcfg (PARSER = zhparser);
ALTER TEXT SEARCH CONFIGURATION testzhcfg ADD MAPPING FOR n,v,a,i,e,l WITH simple;
--可选的参数设定
alter role all set zhparser.multi_short=on;
--简单测试
SELECT * FROM ts_parse('zhparser', 'hello world! 2010年保障房建设在全国范围内获全面启动，从中央到地方纷纷加大 了 保 障 房 的 建 设 和 投 入 力 度 。2011年，保障房进入了更大规模的建设阶段。住房城乡建设部党组书记、部长姜伟新去年底在全国住房城乡建设工作会议上表示，要继续推进保障性安居工程建设。');
SELECT to_tsvector('testzhcfg','“今年保障房新开工数量虽然有所下调，但实际的年度在建规模以及竣工规模会超以往年份，相对应的对资金的需求也会创历史纪录。”陈国强说。在他看来，与2011年相比，2012年的保障房建设在资金配套上的压力将更为严峻。');
SELECT to_tsquery('testzhcfg', '保障房资金压力');
```

利用分词进行全文索引的方法如下：

``` {#codeblock_vls_ltv_8e6}
--为T1表的name字段创建全文索引
create index idx_t1 on t1 using gin (to_tsvector('zhcfg',upper(name) ));
--使用全文索引
 select * from t1 where to_tsvector('zhcfg',upper(t1.name)) @@ to_tsquery('zhcfg','(防火)') ;
```

## 自定义中文分词词典 {#section_2a5_r7r_1hw .section}

自定义中文分词词典，示例如下：

``` {#codeblock_i8b_uvu_72z}
-- 确实的分词结果
SELECT to_tsquery('testzhcfg', '保障房资金压力');
-- 往自定义分词词典里面插入新的分词
insert into pg_ts_custom_word values ('保障房资');
-- 使新的分词生效
select zhprs_sync_dict_xdb();
-- 退出此连接
\c
-- 重新查询，可以得到新的分词结果
SELECT to_tsquery('testzhcfg', '保障房资金压力');
```

**说明：** 内核小版本20160801和之后的版本才支持自定义中文分词词典，您可以通过命令`show rds_release_date ;`来查询内核版本。

使用自定义分词的注意事项如下：

-   最多支持一百万条自定义分词，超出部分不做处理，用户必须保证分词数量在这个范围之内。自定义分词与缺省的分词词典将共同产生作用。
-   每个词的最大长度为128字节，超出部分将会截取。
-   通过增删改分词之后必须执行`select zhprs_sync_dict_xdb();`并且重新建立连接才会生效。

