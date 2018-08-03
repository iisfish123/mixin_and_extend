# mixin_and_extend
ES5如何实现多继承

前提条件：
假设，C继承与Base类，同时C需要从mixins处获得继承，
并且从mixins继承来的方法应该优先级 高于 从Base继承而来的方法，mixin(C, [A, B]);
并且，在C自身原型链上的方法，也应该高于其他。



//知识点补习
hasOwnProperty   判断对象的属性和方法   是否在实例上，是就return true  否就return false

function A(){}
function B(){}
B.prototype.b = function(){}

A.prototype = new B() //继承
A.prototype.a = function(){}

var o = new A()       //实例化对象
o.hasOwnProperty('a')    //false

关键来了:
A.prototype.hasOwnProperty('a')   //true
A.prototype.hasOwnProperty('b')   //false

原因是，b这个属性方法，是从父类继承而来的。
而a属性方法，是在A的原型链上的。

得出结论是：
A.prototype.hasOwnProperty('x')   只要x在A的原型上，那么就返回true