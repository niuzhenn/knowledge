# 数据类型
Javascript中的数据类型分为：
> 1. 基本数据类型：string，number，boolean，null，undefined，symbol，bigint，基本数据类型存在栈内存中
> 2. 引用数据类型： object，引用数据类型存在堆内存中，变量中存的是堆内存的地址

# 数据类型判断方法
1. instanceof
2. typeof
3. Object.prototype.toString.call()

# 深拷贝和浅拷贝的区别
浅拷贝只复制一层对象的属性,深拷贝递归复制对象的所有层级的属性

# new操作符都干了什么
1. 创建一个新的对象
2. 将构造函数的作用域赋给新对象
3. 执行构造函数中的代码
4. 返回新对象

# prototype和__proto__


# 箭头函数
1. 箭头函数的没有this，只能从作用域链继承this
2. 箭头函数不能作为构造函数
3. 箭头函数不能使用new关键字
4. 箭头函数没有arguments参数
5. 箭头函数没有prototype属性
6. 箭头函数没有generator

# Promise, async await
Promise三种状态： pending, fulfilled, reject

Promise.race
Promise.all

async await
基于generator实现，返回promise

# Eventloop
Javascript是一个单线程语言,因此在遇到io等操作时,需要进行异步处理
在js中存在一个调用栈,所有任务都会被放在调用栈里等待执行,同步任务被放在调用栈内执行,异步任务等任务有结果了以后,将回调函数放在任务队列里,当调用栈被清空后,会从任务队列里读取任务放入到调用站内执行

### 宏任务和微任务
js中的任务分为宏任务和微任务
> 宏任务: setTimeout,setInterval,IO,UI rendering,request Animation Frame
> 微任务: Promise, Object.observe
> 微任务的执行在宏任务之前

因此,eventloop的执行顺序如下:
1. 同步任务被放入调用栈执行
2. 调用栈清空
3. 执行所有微任务
4. 执行一个宏任务

# 节流, 防抖
节流: 第一次触发,立即执行,后续在n长时间内不再执行  
防抖: 第一次触发不执行,后续在n长时间内不再次触发在执行

# 匿名自执行函数
```
(function() {
  // ...somecode
}());

!function() {
  // ...somecode
}();

+function() {
  // ...somecode
}();
```
> 核心: 使函数声明变成函数表达式  
> 作用: 创建一个独立的作用域,防止变量弥散全局,多用于各种js库

# js的作用域
1. 局部作用域
2. 全局作用域

# call, apply, bind
都是更改this指向
1. call: 具有多个参数
2. apply: 具有2个参数,第二个参数是array
3. bind: 只改变this指向,不直接执行函数

# javascript继承的方式
```
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.say = function() {
  console.log(`I am ${this.name}`);
}
```
1. 原型链继承
```
function Man() {}
Man.prototype = new Person('sam');
const man = new Man();
man.say();
```
3. 构造继承
```
function Man() {
  Person.apply(this, arugments)
}
const man = new Man('sam');
sam.sau(); // 报错
```
5. 组合继承
```
function Man() {
  Person.apply(this, arguments);
}

Man.prototype = new Person();

```
7. 原型式继承
8. 寄生继承
9. 寄生组合继承
```
function Man() {
  Person.apply(this, arguments);
}

Man.prototype = Object.create(Person.prototype);
Man.prototype.construtor = Man;
const man = new Man('')

```
11. class继承

# 常用排序方法和性能
