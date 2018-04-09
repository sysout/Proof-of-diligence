### [JavaScript Ep.17: lodash](https://www.youtube.com/watch?v=Ri6ICVUMVa8)
```javascript
var random = _.random(2, 10);
var random = _.random(2, 10, true); // float

var movieTitle = _.map(this.state.movie, "Title"); // extract property

let location = _.get(response, "json.results[0].geometry.location");

_.has(response, "json.results[0].geometry.location");

_.cloneDeep(data);

_.includes(str, "Star Wars");

// find one match
_.find(collection, ...);
// filter finds all matches
_.filter(collection, ...);

_.compact([1, 2, 4, false]);
// => [1, 2, 4]

var items = _.map(["Star Wars I", "Forrest Gump"], (str) =>{
  if (_.includes(str, "Star Wars")){
    return str;
  }
});
items = _.compact(items);
```

### [Lodash Tutorial - How Lodash can enhance your JS code](https://www.youtube.com/watch?v=cqw2i0HIj74)
```javascript
var _ = require('lodash');
// or
import _ from 'lodash'


_.maxBy(objects, "property");

_.clone(obj)



function Foo(){
  this.a = 1;
}
function Bar(){
  this.c = 3;
}
Foo.prototype.b = 2;
Bar.prototype.d = 4;
_.assign({'a': 0}, new Foo, new Bar);
// => {'a': 1, 'c': 3}
_.extend({'a': 0}, new Foo, new Bar); // more deep
// => {'a': 1, 'b': 2, 'c': 3, 'd': 4}



var arr = [0, 1, 2, 3];
arr[100] = 100;
arr['a'] = 'five';
_.forEach(arr, console.log);
// runs the 101 times, because arr has a .length property
// skip none integer values

_.forIn(arr, console.log);
// logs (0, 1, 2, 3, 100, five)
// Order is not guaranteed
// Runs 5 times

function vowels(string) {
  return _.filter(string, function(v){
    return /aeiou/i.test(v);
  })
}

_.mixin({'vowels': vowels});
_.vowels('fred')
// => ['e']

// Declarative Code
// VanillaJS
(_.flatten(_.map([1,2,3], x => [x, x*2]))).slice().sort();
// Lodash
_.chain([1,2,3])
  .map(x => [x, x*2])
  .flatten()
  .sort()
  .value();

```

#### [_.forEach in lodash vs javaScripts native Array.forEach](https://dustinpfister.github.io/2017/11/20/lodash_foreach/)
```javascript
// lodash _.forEach
_.forEach(['a','b','c'],function(el,index,arr){
  console.log(index + ' : ' +el + ' : ' + arr);
  if(el === 'b'){
    // the loop will break
    return false;
  }
});
// 0 : a : a,b,c
// 1 : b : a,b,c
```
