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
  
  参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/GetPrototypeOf
  
  2.Object.getOwnPropertyDescriptor
  
  3.Object.getOwnPropertyNames
  
  4.Object.create
  
  定义：Object.create(prototype, descriptors) ：创建一个具有指定原型且可选择性地包含指定属性的对象

  参数:
  
  prototype 必需。  要用作原型的对象。 可以为 null。
  
  descriptors 可选。 包含一个或多个属性描述符的 JavaScript 对象。
  
  ```javascript
  /* 带原型链
   *
  */
  var pt = {
    say : function(){
        console.log('saying!');    
    }
  }
    
  var o = Object.create(pt);
    
  console.log('say' in o); // true
  console.log(o.hasOwnProperty('say')); // false
  
  /* 没有原型链的空对象
   *
  */
  var o1 = Object.create(null);
  console.dir(o1); // object[ No Properties ]
  
  /* 创建没有原型链的但带descriptors的对象
   *
  */
  var o2 = Object.create(null, {
      size: {
          value: "large",
          enumerable: true
      },
      shape: {
          value: "round",
          enumerable: true
      }    
  });
    
  console.log(o2.size);    // large
  console.log(o2.shape);     // round
  console.log(Object.getPrototypeOf(o2));     // null
  
  /* 创建带属性带原型链的对象
   *
  */
  var pt = {
        say : function(){
            console.log('saying!');    
        }
    }

  var o3 = Object.create(pt, {
      size: {
          value: "large",
          enumerable: true
      },
      shape: {
          value: "round",
          enumerable: true
      }    
  });
    
  console.log(o3.size);    // large
  console.log(o3.shape);     // round
  console.log(Object.getPrototypeOf(o3));     // {say:...}
  
  /* 实现继承
   *
  */
  //Shape - superclass
  function Shape() {
    this.x = 0;
    this.y = 0;
  }

  Shape.prototype.move = function(x, y) {
      this.x += x;
      this.y += y;
      console.info("Shape moved.");
  };

  // Rectangle - subclass
  function Rectangle() {
    Shape.call(this); //call super constructor.
  }

  Rectangle.prototype = Object.create(Shape.prototype);

  var rect = new Rectangle();

  console.log(rect instanceof Rectangle); //true.
  console.log(rect instanceof Shape); //true.

  rect.move(); //"Shape moved."
  ```
  
  5.Object.defineProperty
  
  6.Object.defineProperties
  
  7.Object.seal
  
  8.Object.freeze
  
  9.Object.preventExtensions
  
  10.Object.isSealed
  
  11.Object.isFrozen
  
  12.Object.isExtensible
  
  13.Object.keys
