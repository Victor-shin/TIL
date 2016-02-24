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
CREATE TABLE A_ORC (
customerID int, name string, age int, address string
) STORED AS ORC tblproperties (“orc.compress" = “SNAPPY”);

INSERT INTO TABLE A_ORC SELECT * FROM A;

CREATE TABLE B_ORC (
customerID int, role string, salary float, department string
) STORED AS ORC tblproperties (“orc.compress" = “SNAPPY”);

INSERT INTO TABLE B_ORC SELECT * FROM B;

SELECT A_ORC.customerID, A_ORC.name,
A_ORC.age, A_ORC.address join
B_ORC.role, B_ORC.department, B_ORC.salary
ON A_ORC.customerID=B_ORC.customerID;
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
SELECT * 
  FROM (SELECT *, RANK() over (partition by sessionID,
                                   order by timestamp desc) as rank
          FROM clicks
       ) ranked_clicks
 WHERE ranked_clicks.rank = 1;
```
