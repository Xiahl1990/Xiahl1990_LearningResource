# 调试技能

## console.dir() 和 console.dirxml()

1.介绍：在调试JavaScript程序时，有时需要dump某些对象的详细信息。通过手工编写JavaScript代码可以完成这一工作：针对对象的属性进行循环，
  
将循环到的每一个属性值打印出来；可见，这一过程是比较繁琐的。在具备调试工具的浏览器上，这一工作可以通过console.dir()语句来方便的完成。

2.区别：console.dir()打印js对象,console.dirxml()打印DOM对象

## console.assert()

1.介绍：在JavaScript程序的开发和维护过程中，Assert(断言)是一个很好的用于保证程序正确性的特性。

在具备调试工具的浏览器上，这一特性可以通过调用console.assert()来实现。

2.例子：

function cat(name, age, score){
    this.name = name;
    this.age = age;
    this.score = score;
}
var c = new cat("miao", 2, [6,8,7]);
console.assert(c.score.length==3, "Assertion of score length failed");

在console.assert()语句中，第一个参数为需要进行assert的结果，正常情况下应当为true；第二个参数则为出错时在控制台上打印的错误信息。

3.兼容性：console.assert()在有调试工具的浏览器上支持较好，各大浏览器均支持此功能。不过值得一提的是，Firefox自身并不支持此功能，

在Firefox上必须安装Firebug插件才能使用console.assert()。
