```
/**
 * Created by Xiahl1990 on 2016/9/27.
 * js接口的模拟实现
 * 接口的作用：
 * 1.给程序的扩展性提供基础，即 “对修改封闭，对扩展开发”。
 * 2.接口可以降低耦合性，换句话说，可以让某个模块或功能能够重复利用，这样只要写这功能一次代码就ok了。其他地方要用到的，全部用接口调用来实现
 */
var Animal = function () {

}
Animal.prototype.say = new Function();

var Cat = function () {
    this.msg = "miao";
    this.say = function () {
        console.log(this.msg);
    }
}
Cat.prototype = Animal.prototype;

var Dog = function () {
    this.msg = "wang";
    this.say = function () {
        console.log(this.msg);
    }
}
Dog.prototype = Animal.prototype;

function cls( ) {
    var animal = new Animal();
    this.say = function (animal) {
        animal.say();
    }
}
!function (w) {
    var _cls = new cls();

    var _dog = new Dog();
    _cls.say(_dog);

    var _cat = new Cat();
    _cls.say(_cat);

}(window)
```
