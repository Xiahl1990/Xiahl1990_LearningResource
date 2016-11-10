# 函数

## 查看 Function 的属性和方法

```

Object.getOwnPropertyNames(Function);

//["length", "name", "arguments", "caller", "prototype"]

Object.getOwnPropertyNames(Function.prototype);

//["length", "name", "arguments", "caller", "constructor", "bind"(ES5), "toString", "call", "apply"]

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

差异：

1.call:  需要把参数按顺序传递进去；

         参数是明确知道数量时；
         
2.apply: 把参数放在数组里；

         参数不确定的时候，把参数 push 进数组传递进去。（函数内部也可以通过 arguments 这个数组来便利所有的参数）
         

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

// 假设有一个对象cat = {name:"cat"}也想调用say方法，可以如下：
dog.say.call(cat);

// 二者的作用完全一样，只是接受参数的方式存在差异。如：
var func1 = function(arg1, arg2) {};

// 使用方式
func1.call(this, arg1, arg2); 
func1.apply(this, [arg1, arg2]); 
```
