# 函数

## 查看 Function 的属性和方法

```

Object.getOwnPropertyNames(Function);

//["length", "name", "arguments", "caller", "prototype"]

Object.getOwnPropertyNames(Function.prototype);

//["length", "name", "arguments", "caller", "constructor", "bind", "toString", "call", "apply"]

```

### bind 方法的作用与实例

bind()的方法在ie,6,7,8中不适用，需要扩展通过扩展Function prototype可以实现此方法，下面为大家介绍下javascript中bind函数的作用。

```
/**
 * @description 函数说明
 * @params 函数参数
 * @return 函数经过bind后，会生成一个本地函数funBind，funBind里会有一个对函数fun的引用，并非函数fun的一个副本，所以第一个alert会输出true；
 * 而函数一旦经过bind，即便指定了调用者window，那么this仍然是bind指定的i，也就是"1"。
 */
function fun()
{
  alert(arguments.callee == tt);
  alert(this);
}
var i = "1";
var funBind = fun.bind(i);
window.funBind();

/**
 * @description 在ie,6,7,8中通过扩展Function prototype实现bind
 * @params 函数参数
 * @return 函数返回
 */
if (!Function.prototype.bind) { 
  Function.prototype.bind = function(obj) {
    var slice = [].slice, 
    args = slice.call(arguments, 1), 
    self = this, 
    nop = function() {    
    }, 
    bound = function() {
      return self.apply(this instanceof nop ? this : (obj || {}),
      args.concat(slice.call(arguments)));
    };

    nop.prototype = self.prototype;

    bound.prototype = new nop();

    return bound;
  };
}
```

### call,apply 方法的作用与实例

作用：call和apply是为了动态改变this而出现的，当一个object没有某个方法，但是其他的有，我们可以借助call或apply用其它对象的方法来操作。

``` javascript
function Animal(){

}
Animal.prototype={
  name:"dog",
  say: function(){
    alert("I am "+this.name);
  }
}
var dog = new Animal();
dog.say();
//假设有一个对象cat = {name:"cat"}也想调用say方法，可以如下：
dog.say.call(cat);
```
