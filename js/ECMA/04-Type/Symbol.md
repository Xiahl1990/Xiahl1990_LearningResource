# 符号对象 Symbol

## ES6引入探讨

ES5的对象属性名都是字符串，这容易造成属性名的冲突。

比如，你使用了一个他人提供的对象，但又想为这个对象添加新的方法（mixin模式），新方法的名字就有可能与现有方法产生冲突。

如果有一种机制，保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突。这就是ES6引入Symbol的原因。

## 定义

符号是一种特殊的、不可变的数据类型，可以作为对象属性的标识符使用。符号对象是一个符号 原始数据类型的隐式对象包装器。

## 语法

Symbol([description])

参数

  description 可选
  
  可选的，字符串。符号的描述是用于调试的而不是访问符号本身。
  
## 描述

创建一个新的原始 symbol， 你可以使用带有一个可选字符串作为描述的Symbol()：

```
var sym1 = Symbol();
var sym2 = Symbol("foo");
var sym3 = Symbol("foo");
// 上面的代码创建三个新的symbols。 注意，Symbol("foo") 不会强制字符串 “foo” 成为一个符号。它每次都创建一个新的符号：

Symbol("foo") === Symbol("foo"); // false
// 下面使用 new 运算符的语法将会抛出一个 TypeError 错误：

var sym = new Symbol(); // TypeError
// 这会阻止创建一个显式的符号包装器对象而不是一个新的符号值。
// 围绕原始数据类型创建一个显式包装器对象从 ECMAScript 6 开始不再被支持。
// 然而，现有的原始包装器对象，如 new Boolean、 new String以及new Number因为遗留原因仍可被创建。
// 注意，Symbol函数前不能使用new命令，否则会报错。
// 这是因为生成的Symbol是一个原始类型的值，不是对象。也就是说，由于Symbol值不是对象，所以不能添加属性。
// 基本上，它是一种类似于字符串的数据类型。

//如果你非常想创建一个符号包装对象(Symbol wrapper object)，你可以使用 Object() 函数：

var sym = Symbol("foo");
typeof sym;     // "symbol" 
var symObj = Object(sym);
typeof symObj;  // "object"
```
### 全局共享的Symbol

上面的语法使用Symbol() 函数 不会在你的整个代码库中创建一个可用的全局符号。 

要创建跨文件可用的symbols，甚至跨域（每个都有它自己的全局作用域） , 使用这个方法Symbol.for() 和 Symbol.keyFor() 

从全局symbol的注册处设置和取得symbols。

### 在对象中查找Symbol属性

方法Object.getOwnPropertySymbols() 让你在查找一个给定对象的符号属性时返回一个符号类型的数组。

注意，每个初始化的对象都是没有自己的符号属性的，因此这个数组可能为空。除非你已经在对象上设置了符号属性。

## 其他

参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol
