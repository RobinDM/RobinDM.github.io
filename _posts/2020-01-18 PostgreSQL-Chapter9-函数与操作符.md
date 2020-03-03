## 9.26 系统管理函数

#### 9.26.7 数据库对象管理函数

```text
pg_total_relation_size(regclass) = pg_indexes_size(regclass) + pg_table_size(regclass)
pg_table_size(regclass) = pg_relation_size(relation regclass, fork 'main') + 
    pg_relation_size(relation regclass, fork 'fsm') +
    pg_relation_size(relation regclass, fork 'vm') +
    pg_relation_size(relation regclass, fork 'init')
```

注释：

pg_total_relation_size：指定表所用的总磁盘空间，包括所有的索引和TOAST数据 

pg_indexes_size：附加到指定表的索引所占的总磁盘空间

pg_table_size：被指定表使用的磁盘空间，排除索引（但包括 TOAST、空闲空间映射和可见性映射）

pg_relation_size：指定表或索引的指定分叉（`'main'`、`'fsm'`、`'vm'`或`'init'`）使用的磁盘空间