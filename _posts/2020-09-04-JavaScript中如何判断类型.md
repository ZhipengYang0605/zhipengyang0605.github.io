---
title: JavaScript中如何判断类型
description: 总结了JS中常用的五种判断类型的方法， 顺带记录了ES6中几种判断类型的方法！
date: 2020-09-04 20:59:30
categories:
- JS

tags:
- JS
---

## JavaScript判断变量类型

### 1. typeof
- `typeof (整数/小数/自然对数Math.LN2/正无穷大数Infinity)  ===> number`

  `typeof NaN ===> number`
- `typeof (function(){}) ===> function`

  `typeof Math.sin ===> function`
- `typeof undefined ===> undefined`
- `typeof 'xxxx' ===> string`
  
  `typeof '' ===> string`
- `typeof true/false ===> boolean`
- `typeof Symbol() ===> symbol`
  
  `typeof Symbol.iterator ===> symbol`
- `typeof {}/new Date()/[]/null/new RegExp() ===> object`

typeof的方法当遇到对象时, 得到的结果都是object, 并不能准确的判断, 因此此法并不完美.

### 2. Object.prototype.toString
原理:Object原型上的toString()方法可以判断出类型, 格式一般为`[object Function]/[object Number]...`. 这里需要借助call来改变this的指向. 例如:
```
var arr = [1, 2, 3] // 定义一个数组对象
console.log(Object.prototype.toString.call(arr)) // 改变arr的this指向, 调用Object原型链上的toString()方法, 输出[object Array]
```
那么, 为什么不可以直接使用Array/Function...内置的toString()方法来判断类型呢? 这是因为这些对象内置都有toString()方法, 只不过被重写了, 调用toString()方法输出的结果各不一样.

因此这种方式用来判断换类型比较完美, 且兼容性比较好.

### 3. $.type()
jQuery内置的方法, eg:
```
$.type(3) ===> number
$.type(function(){}) ===> function
$.type(null) ===> null
....
```
优点:
- 简洁
- 兼容性好
- 能够准确判断类型

缺点:
- 需要引入整个jQuery包, 增加了项目体积

### 4. instanceof
> instanceof 用来比较一个对象是否为某一个构造函数的实例。注意，instanceof运算符只能用于对象，不适用原始类型的值。

格式为:  实例 instanceof 构造函数, 返回值为true/false

注意: 基本数据类型, 如string/null/undefined/boolean均会返回false, 但function可以用来判断, 如:
```
function(){} instanceof Object // true, function在js中也是一种对象
function(){} instanceof Function // true
```
**用此法来判断对象比较实用, 但是遇到基本类型时显得有点鸡肋, 可视情况选择这种方法来判断了类型**

### 5. constructor
>constructor属性是对象才拥有的，它是从一个对象指向一个函数，含义就是指向该对象的构造函数，每个对象都有构造函数. 

返回值为true/false, 例如:
```
new Number(3).constructor === Number  // true
new Function().constructor === Function  // true
''.constructor === String // true
new Boolean().constructor === Boolean // true
new Date().constructor === Date // true
...
```
有一点需要注意, 有时继承的时候constructor会被重写, 这里不做过多表述.

### 6. JS新语法判断类型
isArray() // 返回值会false/true

isNaN() // 判断是否为NaN





参考资料:

1. [js基础（一）：判断类型](https://segmentfault.com/a/1190000018740340)
2. [由Object.prototype.toString.call( )引发关于toString( )方法的思考](https://juejin.im/post/6844903604990509063)
3. [深入理解Object.prototype.toString.call()](https://www.jianshu.com/p/e4237ebb1cf0)
4. [typeof和instanceof原理](https://juejin.im/post/6844904081803182087)
5. [帮你彻底搞懂JS中的prototype、__proto__与constructor（图解）](https://juejin.im/post/6844903816874164232)