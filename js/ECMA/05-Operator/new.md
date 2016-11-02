# new 操作符

## 描述

在加上new操作符，我们就能完成传统面向对象的class + new的方式创建对象，在Javascript中，我们将这类方式成为Pseudoclassical。

## 实例

```
// 我们执行如下代码
var obj = new Base();
```

这样代码的结果是什么，我们在Javascript引擎中看到的对象模型是：

![JavaScript Example for New](http://coolshell.cn/wp-content/uploads/2012/02/joo_3.png)

```
// new操作符具体干了什么呢?其实很简单，就干了三件事情。
var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);

//第一行，我们创建了一个空对象obj
//第二行，我们将这个空对象的__proto__成员指向了Base函数对象prototype成员对象
//第三行，我们将Base函数对象的this指针替换成obj，然后再调用Base函数，于是我们就给obj对象赋值了一个id成员变量，这个成员变量的值是”base”
```
