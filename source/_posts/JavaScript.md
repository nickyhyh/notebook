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
isNaN方法用来判断一个值是否为NaN，只对数值有效，如果传入其他值，会被先转成数值。比如，传入字符串的时候，字符串会被先转成NaN，所以最后返回true，这一点要特别引起注意。也就是说，isNaN为true的值，有可能不是NaN，而是一个字符串。同样的原因，对于对象和数组，isNaN也返回true。

# 对象
对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。
## 对象的引用
不同的变量名指向同一个对象，也就是指向同一个内存地址，修改其中一个变量，其他所有变量都会改变。
## 属性的读取
点运算符：语法为：对象.属性，例如obj.prop。数值键名不能使用点运算符，会被当成小数点，所以只能使用方括号运算符。
方括号运算符：语法为对象.['属性']，例如obj['prop']。使用方括号运算符，属性名（或键名）需要放在引号中，否则会被看作变量来处理。
```JavaScript
var foo = 'bar';
var obj = {
  foo: 1,
  bar: 2
};
obj.foo  // 1
obj[foo]  //obj[foo]即obj['bar'],所以结果为 2
```
## 属性的查看
查看一个对象所有属性使用Object.keys方法，语法：Object.keys(obj)
## 属性的删除
对象属性的删除使用delete命令，删除后返回true，语法：delete 对象名.属性名 。
注意：
1.删除一个不存在的属性，delete不报错，而且返回true。 delete命令返回false，那就是该属性存在，但不得删除。
2.delete命令只能删除对象本身的属性，无法删除继承的属性。
## 判断属性是否存在
in运算符：包含就返回true，否则返回false。语法：'属性名' in 对象。in运算符不能识别属性是否是对象自身的，还是继承的。
hasOwnProperty方法，判断是否是对象自身的属性。语法：对象名.hasOwnProperty（'属性名'）。

## 属性的遍历
1.for...in循环：用来遍历一个对象的全部属性。
注意：它只遍历对象所有可遍历的属性，并且不仅遍历自身的属性，还遍历继承的属性。

# 函数
## 函数的声明
声明函数有三种方法：
1.函数声明（Function Declaration）：function命令：function 函数名（）{ 函数体；} 
2.函数表达式（Function Expression）：将一个匿名函数赋值给变量。函数表达式需要在语句结尾加上分号，表示语句结束。而函数的声明在结尾的大括号后面不用加分号。
```JavaScript
var print = function(a) {
  console.log(a);
};
```
3.Function构造函数：接收多个参数传递，只有最后一个参数会被当做函数体，只有一个参数的话，该参数就是函数体。几乎不使用这种声明函数的方式。
## 函数作用域
作用域（scope）指的是变量存在的范围。在 ES5 的规范中，JavaScript 只有两种作用域：一种是全局作用域，变量在整个程序中一直存在，所有地方都可以读取；另一种是函数作用域，变量只在函数内部存在。
对于var命令来说，局部变量只能在函数内部声明，在其他区块中声明，一律都是全局变量。
```JavaScript
if (true) {    //在条件判断区块中声明了x，所以x是全局变量，可在外部读取。
  var x = 5;
}
console.log(x);  // 5
```
函数本身的作用域与变量一样，是声明时所在的作用域，而不是调用时所在的作用域。
```JavaScript
var a = 1;
var x = function () {
  console.log(a);
};
function f() {
  var a = 2;
  x();
}
f() // 1
```
## 传递方式
函数参数如果是原始类型的值（数值、字符串、布尔值），传递方式是传值传递（passes by value）。这意味着，在函数体内修改参数值，不会影响到函数外部。
如果函数参数是复合类型的值（数组、对象、其他函数），传递方式是传址传递（pass by reference）。也就是说，传入函数的原始值的地址，因此在函数内部修改参数，将会影响到原始值。
注意，如果函数内部修改的，不是参数对象的某个属性，而是替换掉整个参数，这时不会影响到原始值。
```JavaScript
var obj = [1, 2, 3];
function f(o) {
  o = [2, 3, 4];
}
f(obj);
obj // [1, 2, 3]
```
## arguments对象
arguments对象可以在函数体内部读取所有参数，严格模式下，arguments对象与函数参数不具有联动关系，修改arguments对象不会影响到实际的函数参数。
arguments对象使用数组的两种方法：slice和填入新数组。
```JavaScript
//将arguments转为真正的数组
var args = Array.prototype.slice.call(arguments);
//或者
var args = [];
for (var i=0;i<arguments.length;i++) {
  args.push(arguments[i]);
}
```
## 闭包
“链式作用域”结构：子对象会一级一级地向上寻找所有父对象的变量。父对象的所有变量，对子对象都是可见的，反之则不成立。
闭包就是可以读取其他函数内部变量的函数。简单说就是定义在一个函数内部的函数。本质就是将函数外部和内部连接起来的桥梁。
```JavaScript
function f1() {
  var n = 999;
  function f2() {
    console.log(n);
  }
  return f2;
}
var result = f1();
result(); // 999
```
闭包的优点：
1.可以读取外部函数里的变量。
2.让这些变量始终保存在内存中。
3.封装对象的私有属性和私有方法。
## eval命令
eval命令接受一个字符串作为参数，并将这个字符串当作语句执行。eval的参数不是字符串，那么会原样返回。
引擎只能分辨eval()这一种形式是直接调用，eval的别名调用，作用域都是全局作用域。
# 数组
数组就是按次序排列的一组值。任何类型的数据，都可以放入数组。数组的本质是特殊的对象。typeof运算符会返回数组的类型是object。
由于数组成员的键名是固定的（默认总是0、1、2...），因此数组不用为每个元素指定键名，而对象的每个成员都必须指定键名。JavaScript 语言规定，对象的键名一律为字符串，所以，数组的键名其实也是字符串。之所以可以用数值读取，是因为非字符串的键名会被转为字符串。对于数值的键名，不能使用点结构（object.key）方式读取。
## length属性
只要是数组，就一定有length属性。该属性是一个动态的值，等于键名中的最大整数加上1。由于数组本质上是一种对象，所以可以为数组添加属性，但是这不影响length属性的值。
```JavaScript
var a = [];
a['p'] = 'abc';
a.length // 0

a[2.1] = 'abc';
a.length // 0
```
## 数组的遍历
for循环和while循环
```JavaScript
var a = [1, 2, 3];

// for循环
for(var i = 0; i < a.length; i++) {
  console.log(a[i]);
}

// while循环
var i = 0;
while (i < a.length) {
  console.log(a[i]);
  i++;
}

var l = a.length;
while (l--) {
  console.log(a[l]);
}
```
## 类似数组的对象
“类似数组的对象”的根本特征，就是具有length属性。只要有length属性，就可以认为这个对象类似于数组。但是有一个问题，这种length属性不是动态值，不会随着成员的变化而变化。
典型的“类似数组的对象”是函数的arguments对象，以及大多数 DOM 元素集，还有字符串。
```JavaScript
// arguments对象
function args() { return arguments }
var arrayLike = args('a', 'b');

arrayLike[0] // 'a'
arrayLike.length // 2
arrayLike instanceof Array // false

// DOM元素集
var elts = document.getElementsByTagName('h3');
elts.length // 3
elts instanceof Array // false

// 字符串
'abc'[1] // 'b'
'abc'.length // 3
'abc' instanceof Array // false
```
除了使用slice方法将“类似数组的对象”变成真正的数组，还可以使用call（）把数组的方法放到对象上。
```JavaScript
//slice arrayLick代表类似数组的对象
var arr = Array.prototype.slice.call(arrayLike)

//call()
function print(value,index) {
  console.log(index + ':' + value);
}
Array.prototype.forEach.call(arrayLick,print);
```
字符串也是类似数组的对象，所以也可以用Array.prototype.forEach.call遍历。
# 运算符
## 非相等运算符
对于非相等的比较，算法是先看两个运算子是否都是字符串，如果是的，就按照字典顺序比较（实际上是比较 Unicode 码点）；否则，将两个运算子都转成数值，再比较数值的大小。
非字符串的比较：
两个运算子都是原始类型值，转成数值再比较。字符串和布尔值都会先转成数值再比较。
这里需要注意与NaN的比较。任何值（包括NaN本身）与NaN使用非相等运算符进行比较，返回的都是false。
两个运算子都是对象，转成原始类型的值再比较。对象转换成原始类型的值，算法是先调用valueOf方法（返回对象本身）；如果返回的还是对象，再接着调用toString方法（返回[object，object]）。
## 严格相等运算符
不同类型的值：类型不同直接返回false。
同一类的原始类型值：值相同返回true，不相同返回false。
注意：NaN与任何值都不相等（包括自身）。另外，正0等于负0。
两个复合类型值（对象、数组、函数）的数据比较时，不是比较它们的值是否相等，而是比较它们是否指向同一个地址。
注意，对于两个对象的比较，严格相等运算符比较的是地址，而大于或小于运算符比较的是值。
undefined和null与自身严格相等。
## 严格不相等运算符(!==)
它的算法就是先求严格相等运算符的结果，然后返回相反值。
```JavaScript
1 !== '1' // true
// 等同于
!(1 === '1')
```
## 相等运算符
相等运算符用来比较相同类型的数据时，与严格相等运算符完全一样。比较不同类型的数据时，相等运算符会先将数据进行类型转换，然后再用严格相等运算符比较。
1.原始类型值：将字符串和布尔值都转为数值再比较。
2.对象与原始类型值比较：对象转换为原始类型值再比较。先调用对象的valueOf()方法，如果得到原始类型的值，就按照上一小节的规则，互相比较；如果得到的还是对象，则再调用toString()方法，得到字符串形式，再进行比较。
undefined和null只有与自身比较，或者互相比较时，才会返回true；与其他类型的值比较时，结果都为false。
## 不相等运算符（！=）
它的算法就是先求相等运算符的结果，然后返回相反值。
# 运算符
