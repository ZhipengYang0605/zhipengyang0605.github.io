---
title: JavaScript中的undefined和null
date: 2020-09-03 20:59:30
categories:
- JS

tags:
- JS
---

大家都知道，undefined和null都是JavaScript中基本数据类型之一。先来看看两者的定义：
1. undefined：未定义的值，表示一个变量的原始状态，而非人为操作的结果，常出现在以下情况：
- 声明了变量，但没有赋值
```
let a;
console.log(a) // undefined
```
- 访问对象上不存在的属性或者未定义的变量
```
let obj = {
  name: 'zs'
}
console.log(obj.age) // undefined
console.log(typeof age) // undefined
```
- 函数定义了形参，但没有传递实参
```
//函数定义了形参 a
function fn(a) {
    console.log(a); // undefined
}
fn(); //未传递实参
```


2. null 的字面意思是：空值 。这个值的语义是，希望表示一个对象被人为的重置为空对象，而非一个变量最原始的状态 。 在内存里的表示就是，栈中的变量没有指向堆中的内存对象。

应用场景：
- 初始化一个对象
- 解除引用

注意：
null使用typeof时，得到的结果是object
```
var data = null;
console.log(typeof data); // "object"
```

3. 两者的区别/注意点
- 3.1 typeof的结果不同
```
typeof undefined // undefined
typeof null // object
```
- 3.2
```
console.log ( undefined == null );//true   它们的值是一样都是没有值得意思
console.log ( undefined === null );//false    它们的值一样但是数据类型不一样
```
- 3.3 在if判断中都被判定为false

4. 由以上可知，简单的typeof并不能判断出null，那可以使用什么方式来判断呢？
看了这篇Blog你应该会有答案~
戳这里查看

参考资料：
[JS 应用篇(一)：Underfined与Null的区别](https://blog.csdn.net/madman0621/article/details/82932641)

[js中的undefined和null](https://www.cnblogs.com/zhuangwf/p/11124079.html "js中的undefined和null")

