# 定义

如果指定的属性存在于指定的对象中，则 in 运算符会返回 true。

# 语法

prop in objectName 

# 参数

prop：一个字符串类型或者symbol类型的属性名，或者数组索引。

objectName：需要检测的对象。

# 实例

```
// 数组
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
0 in trees        // 返回true
3 in trees        // 返回true
6 in trees        // 返回false
"bay" in trees    // 返回false (必须使用索引号,而不是数组元素的值)
"length" in trees // 返回true (length是一个数组属性)

// 内置对象
"PI" in Math          // 返回true

// 自定义对象
var mycar = {make: "Honda", model: "Accord", year: 1998};
"make" in mycar  // 返回true
"model" in mycar // 返回true

// in右操作数必须是一个对象值。比如，可以是一个String包装对象，但不能是一个字符串原始值。

var color1 = new String("green");
"length" in color1 // 返回true
var color2 = "coral";
"length" in color2 // 报错(color2不是对象)

// 使用delete运算符和将属性赋值为undefined

// 如果你使用 delete 运算符删除了一个属性，则 in 运算符对所删除属性返回 false。

var mycar = {make: "Honda", model: "Accord", year: 1998};
delete mycar.make;
"make" in mycar;  // 返回false

var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
delete trees[3];
3 in trees; // 返回false

// 如果你只是将一个属性的值赋值为 undefined，而没有用 delete 删除它，则 in 运算仍然会返回true。

var mycar = {make: "Honda", model: "Accord", year: 1998};
mycar.make = undefined;
"make" in mycar;  // 返回true
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
trees[3] = undefined;
3 in trees; // 返回true

// 继承属性

// 如果一个属性是从原型链上继承来的，in 运算符也会返回 true。

"toString" in {}; // 返回true
```
