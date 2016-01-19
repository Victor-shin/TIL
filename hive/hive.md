## Hive Tunning 5 tips
http://ko.hortonworks.com/blog/5-ways-make-hive-queries-run-faster/

### #1 Use Tez
  - tez
```
set hive.execution.engine=tez;
```
  - spark
```
set hive.execution.engine=spark;
```

  - mr (default)
```
set hive.execution.engine=mr;
```

### #2 Use ORCFile
```
SELECT A.customerID, A.name, A.age, A.address join
B.role, B.department, B.salary
ON A.customerID=B.customerID;
```

### #3 Use Vectorization
```
set hive.vectorized.execution.enabled = true;
set hive.vectorized.execution.reduce.enabled = true;
```

### #4 cost based query optimization
```
set hive.cbo.enable=true;
set hive.compute.query.using.stats=true;
set hive.stats.fetch.column.stats=true;
set hive.stats.fetch.partition.stats=true;
```

### #5 Write good SQL
  - Normal case
```
SELECT clicks.* 
  FROM clicks 
       INNER JOIN (SELECT sessionID, MAX(timestamp) AS max_ts 
                     FROM clicks
                    GROUP BY sessionID) latest
       ON clicks.sessionID = latest.sessionID 
          AND clicks.timestamp = latest.max_ts;

```

  - Better case
```
SELECT clicks.* 
  FROM clicks 
       INNER JOIN (SELECT sessionID, MAX(timestamp) AS max_ts 
                     FROM clicks
                    GROUP BY sessionID) latest
       ON clicks.sessionID = latest.sessionID 
          AND clicks.timestamp = latest.max_ts;
```
