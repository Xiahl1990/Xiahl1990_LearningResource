定义：A instanceof B :检测B.prototype是否存在于参数A的原型链上。

``` javascript
function Ben() {
}

var ben = new Ben();

console.log(ben instanceof Ben);//true
```
