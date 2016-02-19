
## UPDATE
db.job.update({"status" : "analyze"}, {$set:{"status":"cancel"}}, {multi:true})
