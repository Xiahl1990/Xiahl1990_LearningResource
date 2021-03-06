# 类数组 (引用 https://segmentfault.com/a/1190000000415572)

```
/**
 * 类数组定义:
 * 1.拥有length属性;
 * 2.属性索引为非负整数;
 * 3.不具有数组所具有的方法
 * javascript中常见的类数组有arguments对象和DOM方法的返回结果。 比如 document.getElementsByTagName()。
 **/
 
 var a = {'0':'a', '1':'b', '2':'c', length:3}; // An array-like object
 Array.prototype.join.call(a, '+'); // => 'a+b+c'
 
/**
 * 类数组判断:
 * 《javascript权威指南》上给出了代码用来判断一个对象是否属于“类数组”。如下：
 **/
 
 // Determine if o is an array-like object.
 // Strings and functions have numeric length properties, but are 
 // excluded by the typeof test. In client-side JavaScript, DOM text
 // nodes have a numeric length property, and may need to be excluded 
 // with an additional o.nodeType != 3 test.
  function isArrayLike(o) {
      if (o &&                                // o is not null, undefined, etc.
          typeof o === 'object' &&            // o is an object
          isFinite(o.length) &&               // o.length is a finite number
          o.length >= 0 &&                    // o.length is non-negative
          o.length===Math.floor(o.length) &&  // o.length is an integer
          o.length < 4294967296)              // o.length < 2^32
          return true;                        // Then o is array-like
      else
          return false;                       // Otherwise it is not
  }
  
 /**
 * 类数组表现:
 * 之所以成为“类数组”，就是因为和“数组”类似。不能直接使用数组方法，但你可以像使用数组那样，使用类数组。
 **/
 
  var a = {'0':'a', '1':'b', '2':'c', length:3};  // An array-like object
  Array.prototype.join.call(a, '+'');  // => 'a+b+c'
  Array.prototype.slice.call(a, 0);   // => ['a','b','c']: true array copy
  Array.prototype.map.call(a, function(x) { 
      return x.toUpperCase();
  });                                 // => ['A','B','C']:
  
  /**
   * 类数组对象转化为数组:
   **/
   
   Array.prototype.slice.call(arguments)
   
   // 对于IE9以前的版本(DOM实现基于COM)，我们可以使用makeArray来实现。
   // 伪数组转化成数组
   var makeArray = function(obj) {
      if (!obj || obj.length === 0) {
          return [];
      }
      // 非伪类对象，直接返回最好
      if (!obj.length) {
          return obj;
      }
      // 针对IE8以前 DOM的COM实现
      try {
          return [].slice.call(obj);
      } catch (e) {
          var i = 0,
              j = obj.length,
              res = [];
          for (; i < j; i++) {
              res.push(obj[i]);
          }
          return res;
      }
   };
```
