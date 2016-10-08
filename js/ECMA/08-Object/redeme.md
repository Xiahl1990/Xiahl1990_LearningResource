# 对象

## 全景图

借博客园网友的图片(http://www.cnblogs.com/Lennyyi/p/4323620.html)

![JavaScript Object Layout](http://images.cnitblog.com/blog2015/727989/201503/091431518391794.jpg)

1.只有函数才有prototype属性(自己加入的prototype不算)

2.__proto__属性在对象创建的时候自动生成，并指向创建该对象的对象的prototype

3.Function对象是由Function创建的，所以Function的__proto__指向本身的prototype

4.Object对象是由Function创建的，所以Object的__proto__指向Function.prototype

5.Function.prototype对象是由Object对象创建的，所以该对象的__proto__指向Object.prototype

6.Object.prototype对象是js的最终对象，所以该对象的__proto__为null

7.可见，函数创造一切，一切皆为对象！

## 查看 Object 对象的属性和方法

```
Object.getOwnPropertyNames(Object);

//["length", "name", "arguments", "caller", "prototype", "keys", "create", "defineProperty", "defineProperties", 
// "freeze", "getPrototypeOf", "setPrototypeOf", "getOwnPropertyDescriptor", "getOwnPropertyNames", "is",
// "isExtensible","isFrozen", "isSealed", "preventExtensions", "seal", "getOwnPropertySymbols", "assign", 
// "deliverChangeRecords", "getNotifier", "observe", "unobserve"]

Object.getOwnPropertyNames(Object.prototype);

//["constructor", "toString", "toLocaleString", "valueOf", "hasOwnProperty", "isPrototypeOf", "propertyIsEnumerable", 
// "__defineGetter__", "__lookupGetter__", "__defineSetter__", "__lookupSetter__", "__proto__"]

```
