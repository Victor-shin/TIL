# TIPS
## Parallel asynchronous Ajax requests using jQuery
```javascript
var done = 4; // number of total requests
var sum = 0;

/* Normal loops don't create a new scope */
$([1,2,3,4,5]).each(function() {
  var number = this;
  $.getJSON("/values/" + number, function(data) {
    sum += data.value;
    done -= 1;
    if(done == 0) $("#mynode").html(sum);
  });
});
```
http://stackoverflow.com/questions/1060539/parallel-asynchronous-ajax-requests-using-jquery

## this vs $(this)
this is the element, $(this) is the jQuery object constructed with that element

http://stackoverflow.com/questions/1051782/jquery-this-vs-this
