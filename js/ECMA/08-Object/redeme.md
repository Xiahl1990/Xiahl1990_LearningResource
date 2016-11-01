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

//["length", "name", "arguments", "caller", "prototype", "keys"(ES5), "create"(ES5), "defineProperty"(ES5), "defineProperties"(ES5), 
// "freeze"(ES5), "getPrototypeOf"(ES5), "setPrototypeOf", "getOwnPropertyDescriptor"(ES5), "getOwnPropertyNames"(ES5), "is",
// "isExtensible"(ES5),"isFrozen"(ES5), "isSealed"(ES5), "preventExtensions"(ES5), "seal"(ES5), "getOwnPropertySymbols", "assign", 
// "deliverChangeRecords", "getNotifier", "observe", "unobserve"]

Object.getOwnPropertyNames(Object.prototype);

//["constructor", "toString", "toLocaleString", "valueOf", "hasOwnProperty", "isPrototypeOf", "propertyIsEnumerable", 
// "__defineGetter__", "__lookupGetter__", "__defineSetter__", "__lookupSetter__", "__proto__"]

```

ES5:

  1.Object.getPrototypeOf
  
  2.Object.getOwnPropertyDescriptor
  
  3.Object.getOwnPropertyNames
  
  4.Object.create
  
  5.Object.defineProperty
  
  6.Object.defineProperties
  
  7.Object.seal
  
  8.Object.freeze
  
  9.Object.preventExtensions
  
  10.Object.isSealed
  
  11.Object.isFrozen
  
  12.Object.isExtensible
  
  13.Object.keys
