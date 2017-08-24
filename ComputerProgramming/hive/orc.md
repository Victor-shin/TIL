
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

## 참고자료
Choosing an HDFS data storage format- Avro vs. Parquet and more - StampedeCon 2015
http://www.slideshare.net/StampedeCon/choosing-an-hdfs-data-storage-format-avro-vs-parquet-and-more-stampedecon-2015
