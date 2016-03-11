
## UPDATE
db.job.update({"status" : "analyze"}, {$set:{"status":"cancel"}}, {multi:true})
db.job.update({"status" : "wait", "owner":"victor.shin"}, {$set:{"status":"cancel"}}, {multi:true})
