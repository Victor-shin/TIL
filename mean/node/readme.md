# learnyounode
## 파일 서버
### My solution
```js
var http = require('http');
var fs = require('fs');

var server = http.createServer(function (request, response) {
    src = fs.createReadStream(process.argv[3]);
    src.pipe(response);
});

var PORT = Number(process.argv[2]);
server.listen(PORT)
```

### Their solution
```js
     var http = require('http')
     var fs = require('fs')

     var server = http.createServer(function (req, res) {
       res.writeHead(200, { 'content-type': 'text/plain' })

       fs.createReadStream(process.argv[3]).pipe(res)
     })

     server.listen(Number(process.argv[2]))
```

## 시간 서버
### My solution
```js
var net = require('net');
var strftime = require('strftime');
var server = net.createServer(function (socket) {
    // socket handling logic
    socket.write(strftime("%Y-%m-%d %H:%M"));
    socket.write("\n");
    socket.end();
});

var PORT = Number(process.argv[2]);
server.listen(PORT)
```

### Their solution
```js
     var net = require('net')

     function zeroFill(i) {
       return (i < 10 ? '0' : '') + i
     }

     function now () {
       var d = new Date()
       return d.getFullYear() + '-'
         + zeroFill(d.getMonth() + 1) + '-'
         + zeroFill(d.getDate()) + ' '
         + zeroFill(d.getHours()) + ':'
         + zeroFill(d.getMinutes())
     }

     var server = net.createServer(function (socket) {
       socket.end(now() + '\n')
     })

     server.listen(Number(process.argv[2]))
```


## ASYNC 다루기
### My solution
```js
var http = require('http')
var bl = require('bl')

var count = 0;
var result = ['', '', ''];
function getUrlData(url, index) {
    http.get(url, callback);
    function callback(response) {
            response.setEncoding("utf8");

            response.pipe(bl(function (err, data) {
                if (err)
                    return console.error(err);

                var str = data.toString();
                result[index] = str;
                count += 1;

                if(count == 3) {
                    for(var i = 0; i < 3; i++) {
                        console.log(result[i]);
                    }
                }
            }));
    };
}
```

### Their solution
```js
     var http = require('http')
     var bl = require('bl')
     var results = []
     var count = 0

     function printResults () {
       for (var i = 0; i < 3; i++)
         console.log(results[i])
     }

     function httpGet (index) {
       http.get(process.argv[2 + index], function (response) {
         response.pipe(bl(function (err, data) {
           if (err)
             return console.error(err)

           results[index] = data.toString()
           count++

           if (count == 3)
             printResults()
         }))
       })
     }

     for (var i = 0; i < 3; i++)
       httpGet(i)
```

## HTTP 모으기
### My solution
- program.js
```js
var http = require('http')
var bl = require('bl')

http.get(process.argv[2], callback);

function callback(response) {
        response.setEncoding("utf8");

        response.pipe(bl(function (err, data) {
            if (err)
                return console.error(err);

            var str = data.toString();
            console.log(str.length);
            console.log(str);
        }));
};
```

### Their solution
- program
```js
     var http = require('http')
     var bl = require('bl')

     http.get(process.argv[2], function (response) {
       response.pipe(bl(function (err, data) {
         if (err)
           return console.error(err)
         data = data.toString()
         console.log(data.length)
         console.log(data)
       }))
     })
```

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
