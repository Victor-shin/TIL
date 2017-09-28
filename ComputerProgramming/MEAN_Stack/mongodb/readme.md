
## UPDATE
```
db.job.update({"status" : "analyze"}, {$set:{"status":"cancel"}}, {multi:true})
db.job.update({"status" : "wait", "owner":"victor.shin"}, {$set:{"status":"cancel"}}, {multi:true})
```

## SELECT
```
db.job.find({"code":"abc"}, {req_date:1, mod_Date:1})
```

## DELETE
```
db.job.remove({"status":"wait", "owner":"victor.shin"})
```
