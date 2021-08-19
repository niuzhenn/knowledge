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


# Eventloop

# 节流, 防抖

# 匿名自执行函数

# js的作用域

# call, apply, bind

