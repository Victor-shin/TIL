
## ORC
https://orc.apache.org/docs/hive-config.html
https://www.mapr.com/blog/what-kind-hive-table-best-your-data
https://streever.atlassian.net/wiki/display/HADOOP/Optimizing+ORC+Files+for+Query+Performance

##### Create ORC table example
```
CREATE TABLE test (
  name STRING,
  color STRING
) STORED AS ORC TBLPROPERTIES ("orc.compress"="NONE");
```
