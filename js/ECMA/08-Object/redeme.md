# 对象

![JavaScript Object Layout](http://images.cnitblog.com/blog2015/727989/201503/091431518391794.jpg)

1.只有函数才有prototype属性(自己加入的prototype不算)

2.__proto__属性在对象创建的时候自动生成，并指向创建该对象的对象的prototype

3.Function对象是由Function创建的，所以Function的__proto__指向本身的prototype

4.Object对象是由Function创建的，所以Object的__proto__指向Function.prototype

4.Function.prototype对象是由Object对象创建的，所以该对象的__proto__指向Object.prototype

5.Object.prototype对象是js的最终对象，所以该对象的__proto__为null

4.可见，函数是一等公民，万物皆对象！
