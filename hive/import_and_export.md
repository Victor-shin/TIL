## CSV로 타입으로 export해보자.
##### 테이블 생성1
```
CREATE TABLE test_csv (
  seq string,
  category string,
  value string
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n'    
STORED AS TEXTFILE
;
```
##### 테이블 생성2
```
CREATE TABLE test_csv ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n'
    AS
SELECT ...(생략)...
...
```
##### export
```
EXPORT TABLE [테이블명] to '[HDFS 디렉토리 경로]';
```

## CSV 파일 import
```
LOAD DATA INPATH '[로컬 화일]' INTO TABLE [테이블명];
```
- http://www.cloudera.com/documentation/enterprise/5-2-x/topics/impala_load_data.html
