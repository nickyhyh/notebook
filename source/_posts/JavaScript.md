---
title: javascript
---
# 入门篇
## 基本语法
1.语句（statement）是为了完成某种任务而进行的操作。
表达式（expression）是为了得到返回值的计算式。
语句与表达式的区别：语句为了进行某种操作，一般情况下不需要返回值；表达式一定会返回一个值。
2.变量：为“值”起名，引用这个名字等同于引用这个值。JavaScript的变量名区分大小写，A与a是两个不同的变量。变量的声明声明与赋值是两个步骤。
```JavaScript
var a; //只申明不赋值，变量的值是undefined
a = 2;
```
JavaScript 引擎的工作方式是先解析代码，获取所有被声明的变量，然后再一行一行地运行。这会导致所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提（hoisting）。
```JavaScript
console.log(a); //不会报错，返回undefined，因为var a导致变量提升，在console.log方法前执行。
var a = 2;
//等价于
var a;
console.log(a);
a = 2;
```
3.标识符
标识符就是各种值的合法名称，常见的标识符就是变量名和函数名。命名规则：
第一个字符，可以是任意字母、$和下划线"_"
第二个字符及以后可以是任意字母、$、下划线和数字。
4.区块
使用{}将多个语句组合在一起。区块对于var命令不够成单独的作用域。
5.循环语句
while循环：只要条件为真，就不断循环执行代码。
for循环：for（初始化表达式；条件；递增表达式）{}，三个部分都可以省略，全部省略就会形成无限循环。
do...while循环：与while循环的区别就是不管条件是否满足，do...while至少会执行一次循环。while语句后面的分号不能省略。
标签label：相当于定位符，用于跳转到程序任意位置。通常与break语句和continue语句配合使用，跳出特定循环。

# 数据类型
JavaScript的数据类型一共有7种。数值、字符串、布尔值这三种类型是原始类型，称作基本数据类型。undefined和null一般看成特殊值。对象是合成类型，一个对象总是多个原始类型值的合成。称作复杂数据类型。对象又可以分成三个子类型，分别是狭义的对象（object）、数组（array）、函数（function）。

判断数据类型的三种方法：typeof运算符、instanceof运算符、Object.prototype.toString方法。

## null与undefined
null是一个表示“空”的对象，转为数值时为0；undefined是一个表示“此处无定义”的原始值，转为数值时为NaN。
null表示空值，调用函数时，某个参数未设置任何值就可以传入null,表示参数为空。
undefined表示“未定义”，返回undefined的场景有
```JavaScript
// 变量声明了，但没有赋值
var i;
i // undefined
// 调用函数时，应该提供的参数没有提供，该参数等于 undefined
function f(x) {
  return x;
}
f() // undefined
// 对象没有赋值的属性
var  o = new Object();
o.p // undefined
// 函数没有返回值时，默认返回 undefined
function f() {}
f() // undefined
```
## Infinity
Infinity的四则运算：
```JavaScript
5 * Infinity // Infinity
5 - Infinity // -Infinity
Infinity / 5 // Infinity
5 / Infinity // 0

0 * Infinity // NaN
0 / Infinity // 0
Infinity / 0 // Infinity

Infinity + Infinity // Infinity
Infinity * Infinity // Infinity

Infinity - Infinity // NaN
Infinity / Infinity // NaN
```
Infinity与null计算时，null会转成0，等同于与0的计算。Infinity与undefined计算，返回的都是NaN。

## isNaN
isNaN方法用来判断一个值是否为NaN，只对数值有效，如果传入其他值，会被先转成数值。比如，传入字符串的时候，字符串会被先转成NaN，所以最后返回true，这一点要特别引起注意。也就是说，isNaN为true的值，有可能不是NaN，而是一个字符串。同样的原因，对于对象和数组，isNaN也返回true

## 字符串与数组
