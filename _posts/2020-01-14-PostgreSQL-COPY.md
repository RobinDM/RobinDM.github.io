[来源]: http://www.postgres.cn/docs/9.4/sql-copy.html

COPY 在表和文件之间拷贝数据

DELIMITER（可选项）：指定分隔每一行记录中的列的字符。文本格式默认为制表符，CSV格式默认为逗号。

- 当文件的分隔符为制表符时，需要在字符串前加E（大小写均可），例如

  ```sql
  DELIMITER E'\t'
  ```

Array（数组）在文本格式中的形式

```json
{1,2,3}
```

JSON在文本格式中的形式

```json
[{"a":1,"b":2},{"a":3,"b":4}]
```

