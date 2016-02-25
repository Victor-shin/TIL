
## ORC
https://orc.apache.org/docs/hive-config.html


##### Create ORC table example
```
CREATE TABLE test (
  name STRING,
  color STRING
) STORED AS ORC TBLPROPERTIES ("orc.compress"="NONE");
```
