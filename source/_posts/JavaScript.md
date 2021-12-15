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
1.void运算符：执行一个表达式不返回任何值，或者返回undefined。主要通途是浏览器的书签工具，以及在超链接中插入代码防止网页跳转。
```html
<a href="javascript: void(document.form.submit())">提交</a>
```
2.逗号运算符：用于对两个表达式求值，并返回后一个表达式的值。用途是在返回一个值以前，进行一些辅助操作。
# 数据类型转换
## 强制转换
强制转换主要指使用Number()、String()和Boolean()三个函数，手动将各种类型的值，分别转换成数字、字符串或者布尔值。
## Number()
1.原始类型值。数值：转换后还是原来的值。字符串可以被解析为数值，则转为数值；不能解析为数值的转换为NaN。空字符串转为0。布尔值true转为1，false转为0。undefined转为NaN。null转为0。
2.对象类型。Number方法的参数是对象时返回NaN，除非是包含单个数值的数组。
参数是对象，Number的转换规则：
第一步，调用对象自身的valueOf方法。如果返回原始类型的值，则直接对该值使用Number函数，不再进行后续步骤。
第二步，如果valueOf方法返回的还是对象，则改为调用对象自身的toString方法。如果toString方法返回原始类型的值，则对该值使用Number函数，不再进行后续步骤。
第三步，如果toString方法返回的是对象，就报错。
## String()
1.原始类型值。数值：转为相应的字符串。字符串：转换后还是原来的值。布尔值：true转为字符串"true"，false转为字符串"false"。undefined：转为字符串"undefined"。
null：转为字符串"null"。
2.对象类型。String方法的参数是对象，返回一个类型字符串；如果是数组，返回该数组的字符串形式。
```JavaScript
String({a: 1}) // "[object Object]"
String([1, 2, 3]) // "1,2,3"
```
String方法的转换规则，与Number方法基本相同，只是互换了valueOf方法和toString方法的执行顺序。如果toString法和valueOf方法，返回的都是对象，就会报错。
```JavaScript
String({a: 1})
// "[object Object]",上面代码先调用对象的toString方法，发现返回的是字符串[object Object]，就不再调用valueOf方法了。
```
## Boolean()
可以将任意类型的值转为布尔值。除了undefined、null、0、NaN、''（空字符串）五个值为false，其他值全为true。
注意，所有对象（包括空对象）的转换结果都是true，甚至连false对应的布尔对象new Boolean(false)也是true。
## 自动转换
以下三种情况JavaScript会自动转换数据类型。
1.不同类型的数据相互运算。
2.对非布尔值类型的数据求布尔值。
3.对非数值类型的值使用一元运算符（即+和-）。

自动转换为字符串
```JavaScript
'5' + 1 // '51'
'5' + true // "5true"
'5' + false // "5false"
'5' + {} // "5[object Object]" {}转为字符串是"[object Object]"
'5' + [] // "5" []转换字符串是" "(空字符)
'5' + function (){} // "5function (){}"
'5' + undefined // "5undefined"
'5' + null // "5null"
```
自动转换为数值
```JavaScript
'5' - '2' // 3
'5' * '2' // 10
true - 1  // 0
false - 1 // -1
'1' - 1   // 0
'5' * []    // 0
false / '5' // 0
'abc' - 1   // NaN
null + 1 // 1  null转为数值时为0
undefined + 1 // NaN undefined转为数值时为NaN
```
# 错误处理机制
## Error实例对象
Error()构造函数接受一个参数，表示错误提示，可以从实例的message属性读到这个参数。抛出Error实例对象以后，整个程序就中断在发生错误的地方，不再往下执行。
## 原生错误类型
1.SyntaxError 对象：解析代码时发生的语法错误。
2.ReferenceError 对象：引用一个不存在的变量或者将一个值分配给无法分配的对象，如给函数结果赋值。
3.RangeError 对象：一个值超出有效范围。
4.TypeError 对象：变量或参数不是预期类型。
5.URIError 对象：URI相关函数的参数不正确。
6.EvalError 对象：eval函数没有被正确执行。改错误类型已不再使用了。
这几种错误对象以及Error对象都是构造函数。都接受一个参数，代表错误提示信息message。
## throw语句
throw语句的作用是手动中断程序执行，抛出一个错误。throw的参数可以是任何类型的
值。
## try...catch
允许对错误进行处理，选择是否往下执行。catch捕获错误之后程序不会中断，继续往下执行。
```JavaScript
try {
  f()  //函数f执行如果报错就会被catch捕获进行处理
}catch(e) {
  //处理错误
}
```
# 标准库
## Object对象
Object对象的原生方法分两类：Object本身的方法和Object实例方法。本身的方法就是直接定义在Object对象的方法，实例方法就是定义在Object原型对象Object.prototype上的方法，可以被所有实例共享使用。
## Object构造函数
构造函数的用途是生产新对象。Object(value)表示将value转成一个对象，new Object(value)表示生产一个新对象，它的值是value。
## Object的静态方法
“静态方法”指的是Object对象自身的方法。遍历对象的属性方法：
Object.keys方法的参数是一个对象，返回一个数组。数组成员都是对象自身的所有属性名。
Object.getOwnPropertyName方法的参数和返回值同Object.keys方法，包含该对象自身的所有属性名。Object.keys方法只返回可枚举的属性，Object.getOwnPropertyNames方法还返回不可枚举的属性名。
## Object的实例方法
Object实例对象的方法，主要有以下六个。
1.Object.Prototype.valueOf():返回当前对象的"值"。默认返回对象本身。自动类型转换时会默认调用这个方法。
2.Object.Prototype.toString():返回一个对象的字符串形式。默认返回类型字符串。数组、字符串、函数、Date对象分别自定义了toString方法，覆盖了Object.Prototype.toString方法。
```JavaScript
[1, 2, 3].toString() // "1,2,3"

'123'.toString() // "123"

(function () {
  return 123;
}).toString()
// "function () {
//   return 123;
// }"

(new Date()).toString()
// "Tue May 10 2016 09:11:31 GMT+0800 (CST)"
```
任何值通过call()方法可以判断这个值的类型：
`Object.Prototype.toString.call(value)`
类型判断函数：
```JavaScript
var type = function (i){
  var s = Object.Prototype.toString.call(i);
  return s.match(/\[object (.*?)\]/)[1].toLowerCase();
};
type({});  // "object"
type([]); // "array"
type(5); // "number"
type(null); // "null"
type(); // "undefined"
type(/abcd/); // "regex"
type(new Date()); // "date"
```
3.Object.prototype.toLocaleString():与toString相同，返回一个字符串形式。主要作用是留出一个接口，让各种不同的对象实现自己版本的toLocaleString，用来返回针对某些地域的特定的值。Array.prototype.toLocaleString()、Number.prototype.toLocaleString()、Date.prototype.toLocaleString()这三个对象自定义了toLocaleString方法。
4.Object.prototype.hasOwnProperty()：接收一个字符串为参数，返回一个布尔值。表示实例是否具有该属性。
5.Object.prototype.isPrototypeOf()：判断当前对象是否为另一个对象的原型。
6.Object.prototype.propertyIsEnumerable()：判断某个属性是否可枚举。
## Array对象
Array是JavaScript的原生对象，同时也是一个构造函数，可以用它生成新的数组。Array()构造函数的缺点：不同的参数个数会导致不一样的行为。因此，直接使用数组字面量生产新数组更合适。
静态方法：Array.isArray()方法返回一个布尔值，表示是否为数组。
实例方法：
1.valueof()方法返回数组本身。toString()方法返回数组字符串形式。
2.push()方法在数组末尾添加一个或多个元素，返回添加新元素后的数组长度，会改变原数组。
pop()方法删除数组的最后一个元素，并返回该元素，会改变原数组。
push和pop结合使用，就构成了“后进先出”的栈结构（stack）。
3.shift()方法删除数组的第一个元素，并返回该元素，改变原数组。
push()和shift()结合使用，就构成了“先进先出”的队列结构（queue）。
unshift()方法在数组的第一个位置添加元素，并返回添加新元素后的数组长度，改变原数组。
4.join()方法以指定参数作为分隔符，将数组成员连接为一个字符串返回。不提供参数默认逗号分隔。
5.concat()方法用于多个数组的合并，返回一个新数组，原数组不变。数量数组也接受其他类型的值作为参数，添加到数组尾部。如果数组成员包括对象，concat方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是新数组拷贝的是对象的引用。
6.reverse()方法用于颠倒排列数组元素，返回改变后的数组。
7.slice()用于提取目标数组的一部分，返回新数组，原数组不变。它的第一个参数为起始位置（从0开始，会包括在返回的新数组之中），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员。slice()没有参数等于返回原数组的拷贝。slice()方法的一个重要应用，是将类似数组的对象转为真正的数组。
8.splice()用于删除原数组的一部分成员，并可以在删除位置添加新数组成员，返回值是被删除的元素，改变原数组。如果只单纯的插入元素，第二个参数设置为0。如果只提供第一个参数，等同于将原数组在指定位置拆分成两个数组。
9.sort()方法对数组成员进行排序。排序后原数组被改变。
10.map()方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。
map()方法还可以接受第二个参数，用来绑定回调函数内部的this变量。
```JavaScript
 var arr = ['a','b','c'];
 [1,2].map(function (e) {
   return this[e];
 },arr) //['b','c']
 ```
如果数组有空位，map()方法的回调函数在这个位置不会执行，会跳过数组的空位。
```JavaScript 
var f = function (i) { return 'a' };
[1, undefined, 2].map(f) // ['a','a','a'] 
[1, null, 2].map(f) // ['a','a','a'] 
[1, , 2].map(f) // ['a', ,'a'] 
```
11.forEach()方法与map()方法类似，但是forEach()方法没有返回值，只用来操作数据。遍历数组需要得到返回值就使用map()方法。否则使用forEach()方法。
12.filter()方法用于过滤数组成员，满足条件的成员组成一个新数组返回。它的参数是一个函数，所有数组成员依次执行该函数，返回结果为true的成员组成一个新数组返回。该方法不会改变原数组。
13.some()和every():这两个方法类似“断言”，返回布尔值，表示判断数组成员是否符合某种条件。它们接收函数作为参数，数组成员依次执行该函数。some方法是只要一个成员的返回值是true，则整个some方法的返回值就是true，否则返回false。every方法是所有成员的返回值都是true，整个every方法才返回true，否则返回false。
对于空数组，some方法返回false，every方法返回true，回调函数都不会执行。
```JavaScript
function isEven(x) { return x % 2 === 0 }
[].some(isEven) // false
[].every(isEven) // true
```
14.reduce()和reduceRight()：依次处理数组的每个成员，最终累积为一个值。reduce()方法和reduceRight()方法的第一个参数都是一个函数。该函数接受以下四个参数：
累积变量:第一次执行时，默认为数组的第一个成员；以后每次执行时，都是上一轮的返回值。
当前变量:第一次执行时，默认为数组的第二个成员；以后每次执行时，都是下一个成员。
当前位置:一个整数，表示第二个参数（当前变量）的位置，默认为1。
原数组
四个参数中，前两个必须，后两个可选。
15.indexOf()方法：返回给定元素在数组中第一次出现的位置。如果没有出现返回-1。接收第二个参数，表示搜索开始的位置。
IastIndexOf()方法：返回给定元素在数组中最后一次出现的位置。如果没有出现返回-1。
这两个方法不能用来搜索NaN的位置，即它们无法确定数组成员是否包含NaN。
## 包装对象
所谓“包装对象”，指的是与数值、字符串、布尔值分别相对应的Number、String、Boolean三个原生对象。这三个原生对象可以把原始类型的值变成（包装成）对象。这三个对象作为构造函数使用（带有new）时，可以将原始类型的值转为对象；作为普通函数使用时（不带有new），可以将任意类型的值，转为原始类型的值。
# Boolean对象