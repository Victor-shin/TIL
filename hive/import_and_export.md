## CSV로 타입으로 EXPORT해보자.
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

## CSV 파일 IMPORT
```
LOAD DATA INPATH '[HDFS 파일 경로]' INTO TABLE [테이블명];
LOAD DATA LOCAL INPATH '[로컬 파일 경로]' INTO TABLE [테이블명];
```
- https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DML
