# learnyounode
## HTTP 클라이언트
### My solution
- program.js
```js
var http = require('http')

http.get(process.argv[2], callback);

function callback(response) {
        response.setEncoding("utf8");
        response.on("data", console.log);
}
```

### Their solution
- program.js
```js
     var http = require('http')

     http.get(process.argv[2], function (response) {
       response.setEncoding('utf8')
       response.on('data', console.log)
       response.on('error', console.error)
     }).on('error', console.error)
```

## 모듈 단위로 만들기
### My solution
- program.js
```js
var mymodule = require('./mymodule.js');

function callback(err, data) {
    if(err) return;
    data.forEach(
        function(item) {
            console.log(item);
        }
    );
}

var ret = mymodule(process.argv[2], process.argv[3], callback);
```

- mymodule.js
```js
var fs = require('fs');

module.exports = function (path, ext, callback) {
    fs.readdir(path, mcallback);

    function mcallback (err, list) {
        if (err)
            return callback(err)

        var filtered = list.filter(function (item) {
            return item.endsWith("." + ext);
        });

        callback(null, filtered)
    }
}
```

### Their solution
- program.js
```js
     var filterFn = require('./solution_filter.js')
     var dir = process.argv[2]
     var filterStr = process.argv[3]

     filterFn(dir, filterStr, function (err, list) {
       if (err)
         return console.error('There was an error:', err)

       list.forEach(function (file) {
         console.log(file)
       })
     })
```

- solution_filter.js
```js
     var fs = require('fs')
     var path = require('path')

     module.exports = function (dir, filterStr, callback) {

       fs.readdir(dir, function (err, list) {
         if (err)
           return callback(err)

         list = list.filter(function (file) {
           return path.extname(file) === '.' + filterStr
         })

         callback(null, list)
       })
     }
```
