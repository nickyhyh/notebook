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
作为构造函数，它主要用于生成布尔值的包装对象实例。
```JavaScript
if (new Boolean(false)) {
  console.log('true');
} // true  false对应的包装对象实例是一个对象，所有对象对应的布尔值都是true。
if (new Boolean(false).valueOf()) {
  console.log('true');
} // 无输出 valueOf返回实例对应的原始值
```
## Boolean函数的类型转换作用
```JavaScript
Boolean(undefined) // false
Boolean(null) // false
Boolean(0) // false
Boolean('') // false
Boolean(NaN) // false

Boolean(1) // true
Boolean('false') // true
Boolean([]) // true
Boolean({}) // true
Boolean(function () {}) // true
Boolean(/foo/) // true
```
使用双重的否运算符（!）也可以将任意值转为对应的布尔值。
# Number对象
作为构造函数时，它用于生成值为数值的对象。
Number对象的4个实例方法：
1.Number.prototype.toString():用来将一个数值转为字符串形式。接受一个参数，表示输出的进制。如果省略这个参数，默认将数值先转为十进制，再输出字符串；否则，就根据参数指定的进制，将一个数字转化成某个进制的字符串。
2.Number.prototype.toFixed():先将一个数转为指定位数的小数，然后返回这个小数对应的字符串。参数为小数位数，有效范围0-100，超出则抛出RangError错误。
3.Number.prototype.toExponential():将一个数转为科学计数法形式。参数是小数点后有效数字的位数，范围为0到100，超出这个范围，会抛出一个 RangeError 错误。
4.Number.prototype.toPrecision():用于将一个数转为指定位数的有效数字。参数为有效数字的位数，范围是1到100，超出这个范围会抛出 RangeError 错误。
5.Number.prototype.toLocaleString():接受一个地区码作为参数，返回一个字符串，表示当前数字在该地区的当地书写形式。
# String对象
用来生成字符串对象，字符串对象是一个类似数组的对象。
## 实例方法
1.String.prototype.charAt():返回指定位置的字符，参数从0开始编号的位置。如果参数为负数，或大于等于字符串的长度，charAt返回空字符串。
2.Strig.prototype.charCodeAt():返回字符串指定位置的 Unicode 码点（十进制表示），相当于String.fromCharCode()的逆操作。如果参数为负数，或大于等于字符串的长度，charCodeAt返回NaN。
3.String.prototype.concat():用于连接两个字符串，返回一个新字符串，不改变原字符串。
4.String.prototype.slice():用于从原字符串取出子字符串并返回，不改变原字符串。不改变原字符串。它的第一个参数是子字符串的开始位置，第二个参数是子字符串的结束位置（不含该位置）。如果省略第二个参数，则表示子字符串一直到原字符串结束。如果第一个参数大于第二个参数（正数情况下），slice()方法返回一个空字符串。
5.String.prototype.substring():用于从原字符串取出子字符串并返回，不改变原字符串。跟slice方法很相像。如果第一个参数大于第二个参数，substring方法会自动更换两个参数的位置。如果参数是负数，substring方法会自动将负数转为0。
6.String.prototpye.substr():用于从原字符串取出子字符串并返回，不改变原字符串，跟slice和substring方法的作用相同。substr方法的第一个参数是子字符串的开始位置（从0开始计算），第二个参数是子字符串的长度。如果第一个参数是负数，表示倒数计算的字符位置。如果第二个参数是负数，将被自动转为0，因此会返回空字符串。
7.String.prototype.indexOf()和String.prototype.lastIndexOf()
indexOf用于确定一个字符串在另一个字符串中第一次出现的位置，返回结果是匹配开始的位置。如果返回-1，就表示不匹配。indexOf方法还接受第二个参数，表示从该位置开始向后匹配。
lastIndexOf从尾部开始匹配，indexOf则是从头部开始匹配。lastIndexOf的第二个参数表示从该位置起向前匹配。
8.String.prototype.trim():用于去除字符串两端的空格，返回新字符串，不改变原字符串。
9.String.prototype.toLowerCase()：将一个字符串全部转为小写；String.prototype.toUpperCase()：将一个字符串全部转为大写。它们都返回一个新字符串，不改变原字符串。
10.String.prototype.match():用于确定原字符串是否匹配某个子字符串，返回一个数组，成员为匹配的第一个字符串。如果没有找到匹配，则返回null。返回的数组还有index属性和input属性，分别表示匹配字符串开始的位置和原始字符串。
11.String.prototype.search():用法基本等同于match，但是返回值为匹配的第一个位置。如果没有找到匹配，则返回-1。
String.prototype.replace():用于替换匹配的子字符串，一般情况下只替换第一个匹配（除非使用带有g修饰符的正则表达式）。
12.String.prototype.split()：按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组。如果分割规则为空字符串，则返回数组的成员是原字符串的每一个字符。如果省略参数，则返回数组的唯一成员就是原字符串。如果满足分割规则的两个部分紧邻着（即两个分割符中间没有其他字符），则返回数组之中会有一个空字符串。
``` JavaScript
"1.2..3".split('.')   //['1', '2', '', '3']
```
如果满足分割规则的部分处于字符串的开头或结尾（即它的前面或后面没有其他字符），则返回数组的第一个或最后一个成员是一个空字符串。
```JavaScript
'|b|c'.split('|') // ["", "b", "c"]
'a|b|'.split('|') // ["a", "b", ""]
```
split方法还可以接受第二个参数，限定返回数组的最大成员数。
13.String.prototype.localeCompare():用于比较两个字符串，返回一个整数，如果小于0表示第一个字符串小于第二个；等于0表示两者相等；大于0表示第一个字符串大于第二个。该方法的特点：正常情况大写的英文字母小于小写字母，但是localeCompare方法会考虑自然语言的排序情况，将大写字母排在小写字母的后面，表示大写字母更大。
# Math对象
## Math.random()
Math.random()返回0到1之间的一个伪随机数，可能等于0，但是一定小于1。
1.任意范围的随机数生成函数
```JavaScript
function getRandomArbitrary(min, max) {
  return Math.random() * (max - min) + min;
}
getRandomArbitrary(2.5, 7.5)  //5.289410648102216
```
2.任意范围的随机整数生成函数
```JavaScript
function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
getRandomInt(2, 5) // 3
```
3.返回随机字符的例子
```JavaScript
function random_str(length) {
  var ALPHABET = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  ALPHABET += 'abcdefghijklmnopqrstuvwxyz';
  ALPHABET += '0123456789-_';
  var str = '';
  for(var i = 0; i < length; ++i) {
    var rand = Math.floor(Math.random() * ALPHABET.length);
    str += ALPHABET.substring(rand, rand + 1);
  }
  return str;
}
random_str(7) //  'hWrLy9u'
```
# Date对象
## 普通函数用法
作为普通函数直接调用，返回一个当前时间的字符串。无论是否带有参数，返回的都是当前时间。
## 构造函数用法
使用new命令返回一个Date对象的实例，不加参数实例代表的就是当前时间。其他对象求值时默认调用valueOf()方法，Date实例求值时调用的是toString()方法，导致返回的是一个字符串，代表该实例对应的时间。
注意：
1.时间参数为负数，代表1970年元旦之前的时间。
2.只要是能被Date.parse()方法解析的字符串，都可以当做参数。
3.参数为年、月、日等多个整数时，年和月不能省略，其他参数可省略。至少需要两个参数，因为如果只使用“年”一个参数会被解释为毫秒数。
```JavaScript
new Date(2013, 13) 
// Tue Feb 01 2014 00:00:00 GMT+0800 (CST) 15折算为下一年2月,月份0-11
new Date(2013, 0, 0)
// Mon Dec 31 2012 00:00:00 GMT+0800 (CST)  日期为0代表上个月最后一天
```
```JavaScript
//参数还可以使用负数，表示扣去的时间
new Date(2013, -1)
// Sat Dec 01 2012 00:00:00 GMT+0800 (CST)
new Date(2013, 0, -1)
// Sun Dec 30 2012 00:00:00 GMT+0800 (CST)
```
4.日期的运算：两个日期实例对象进行减法运算时，返回的是它们间隔的毫秒数；进行加法运算时，返回的是两个字符串连接而成的新字符串。
## 静态方法
1.Date.now():返回当前时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数。
2.Date.parse():解析日期字符串，返回改时间距离零点的毫秒数。
3.Date.UTC方法接受年、月、日等变量作为参数，返回距离零点的毫秒数。
## 实例方法
除了valueOf和toString方法以外，可分为以下三类：
1.to类：从Date对象返回一个字符串，表示指定的时间。
2.get类：获取Date对象的日期和时间。
3.set类：设置Date对象的日期和时间。
# RegExp对象
正则表达式是一种表达文本模式的方法，按照“给定模式”匹配文本。新建正则表达式的两种方法：
1.字面量：以斜杠开始开始和结束,`var reges = /abc/;`
2.使用构造函数：`var regex = new RegExp('abc');`
## 实例属性
修饰符类，了解设置了什么修饰符。
RegExp.prototype.ignoreCase:返回一个布尔值，表示是否设置了i修饰符。
RegExp.prototype.global：返回一个布尔值，表示是否设置了g修饰符。
RegExp.prototype.multiline：返回一个布尔值，表示是否设置了m修饰符。
RegExp.prototype.flags：返回一个布尔值，包含已经设置的所有修饰符，按字母排序。
以上属性都是只读的。
与修饰符无关的属性有两个：
RegExp.prototype.lastIndex：返回一个整数，表示下一次开始搜索的位置。该属性可读写。
RegExp.prototype.source：返回正则表达式的字符串形式(不包括反斜杠)，该属性只读。
## 实例方法
1.RegExp.prototype.text():返回一个布尔值，表示当前模式是否能匹配参数字符串。如果正则表达式带有g修饰符，则每一次方法都从上一次结束的位置开始向后匹配。
```JavaScript
var r = /x/g;
var s = '_x_x';
r.lastIndex // 0
r.test(s) // true
r.lastIndex // 2
r.test(s) // true
r.lastIndex // 4
r.test(s) // false
```
2.RegExp.prototype.exec():用来返回匹配结果。发现匹配则返回一个数组，成员是匹配成功的子字符串，否则返回null。
如果正则表示式包含圆括号（即含有“组匹配”），则返回的数组会包括多个成员。第一个成员是整个匹配成功的结果，后面的成员就是圆括号对应的匹配成功的组。也就是说，第二个成员对应第一个括号，第三个成员对应第二个括号，以此类推。整个数组的length属性等于组匹配的数量再加1。
```JavaScript
var s = /a(b)/;    
var r = 'abcdabc';    
s.exec(r); //['ab','b']
```
## 字符串实例方法
字符串的实例方法中有4种与正则表达式有关：
1.String.prototype.match():返回一个数组，成员是所有匹配的子字符串。与exec方法比较像，但是如果正则表达式带有g修饰符，则会一次性返回匹配成功的结果。
```JavaScript
var s = 'abba';
var r = /a/g;
s.match(r) // ["a", "a"]
r.exec(s) // ["a"]
```
设置正则表达式的lastIndex属性，对match方法无效，匹配总是从字符串的第一个字符开始。
```JavaScript
var r = /a|b/g;
r.lastIndex = 7;
'xaxb'.match(r) // ['a', 'b']
r.lastIndex // 0
```
2.String.prototype.search():按给定正则表达式进行搜索，返回第一个满足条件的匹配结果在字符串中的位置。如果没有任何匹配，则返回-1。
3.String.prototype.replace():按给定正则表达式进行替换，返回替换后的字符串。它接受两个参数，第一个是正则表达式，表示搜索模式，第二个是替换的内容。正则表达式如果不加g修饰符，就替换第一个匹配成功的值，否则替换所有匹配成功的值。
replace方法：删除字符串收尾两端的空格
```JavaScript
var str = '   hello,jimmy !  ';
str.replace(/^\s+|\s+$/g, '');  //'hello,jimmy !'
```
replace方法的第二个参数可以使用美元符号$，用来指代所替换的内容。
$&：匹配的子字符串。
$`：匹配结果前面的文本。
$'：匹配结果后面的文本。
$n：匹配成功的第n组内容，n是从1开始的自然数。
$$：指代美元符号$。
```JavaScript
'hello nicky'.replace(/(\w+)\s(\w+)/, '$2 $1')
// "nicky hello"  
'abc'.replace('b', '[$`-$&-$\']')
// "a[a-b-c]c"
```
replace方法的第二个参数还可以是一个函数，将每一个匹配内容替换为函数返回值。
```JavaScript
var str = 'the cure white dog jumped over the lazy cat.'
var pattern = /cure|white|lazy/ig;
str.replace(pattern, function(match) {
  return match.toUpperCase();
});
```
4.String.prototype.split():按照给定规则进行字符串分割,返回一个数组，包含分割后的各个成员。该方法接受两个参数，第一个参数是正则表达式，表示分隔规则，第二个参数是返回数组的最大成员数。
```JavaScript
// 非正则分隔
'a,  b,c, d'.split(',')
// [ 'a', '  b', 'c', ' d' ]
// 正则分隔，去除多余的空格
'a,  b,c, d'.split(/, */)
// [ 'a', 'b', 'c', 'd' ]
// 指定返回数组的最大成员
'a,  b,c, d'.split(/, */, 2)
[ 'a', 'b' ]
```
## 匹配规则
1.字面量字符和元字符
如果在正则表达式之中，某个字符只表示它字面的含义就叫做“字面量字符”。不代表字面的意思。它们叫做“元字符”，主要有以下几个：
(1)点字符(.)
点字符（.）匹配除回车（\r）、换行(\n) 、行分隔符（\u2028）和段分隔符（\u2029）以外的所有字符。
/b.t/匹配b和t之间包含任意一个字符的情况,只要这三个字符在同一行。
(2)位置字符
用来提示字符所处位置，主要有两个字符。
^表示字符串开始的位置，$表示字符串结尾的位置。
(3)选择符(|)
竖线符号（|）在正则表达式中表示“或关系”（OR）。
2.转义符
正则表达式中那些有特殊含义的元字符，如果要匹配它们本身，就需要在它们前面要加上反斜杠。比如要匹配+，就要写成\+。
正则表达式中，需要反斜杠转义的，一共有12个字符：^、.、[、$、(、)、|、*、+、?、{和\。需要特别注意的是，如果使用RegExp方法生成正则对象，转义需要使用两个斜杠，因为字符串内部会先转义一次。
3.特殊字符
\cX 表示Ctrl-[X]，其中的X是A-Z之中任一个英文字母，用来匹配控制字符。
[\b] 匹配退格键(U+0008)，不要与\b混淆。
\n 匹配换行键。
\r 匹配回车键。
\t 匹配制表符 tab（U+0009）。
\v 匹配垂直制表符（U+000B）。
\f 匹配换页符（U+000C）。
\0 匹配null字符（U+0000）。
\xhh 匹配一个以两位十六进制数（\x00-\xFF）表示的字符。
\uhhhh 匹配一个以四位十六进制数（\u0000-\uFFFF）表示的 Unicode 字符。
4.字符类
字符类（class）表示有一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内，比如[xyz] 表示x、y、z之中任选一个匹配。
字符类中有特殊含义：
脱字符(^):如果方括号内的第一个字符是[^]，则表示除了字符类之中的字符，其他字符都可以匹配。比如，[^xyz]表示除了x、y、z之外都可以匹配。
如果方括号内没有其他字符，即只有[^]，就表示匹配一切字符，其中包括换行符。相比之下，点号作为元字符（.）是不包括换行符的。脱字符只有在字符类的第一个位置才有特殊含义，否则就是字面含义。
```JavaScript
var s = 'Please yes\nmake my day!';
s.match(/yes.*day/) // null
s.match(/yes[^]*day/) // [ 'yes\nmake my day']
```
连字符(-):对于连续序列的字符，连字符（-）用来提供简写形式，表示字符的连续范围。比如[abc]可以写成[a-c]，[0123456789]可以写成[0-9]，同理[A-Z]表示26个大写字母。只有在方括号之中才具备简写作用。
`[1-31]`不代表1到31，只代表1-3。
5.预定义模式
某些常见模式的简写方式
\d 匹配0-9之间的任一数字，相当于[0-9]。
\D 匹配所有0-9以外的字符，相当于[^0-9]。
\w 匹配任意的字母、数字和下划线，相当于[A-Za-z0-9_]。
\W 除所有字母、数字和下划线以外的字符，相当于[^A-Za-z0-9_]。
\s 匹配空格（包括换行符、制表符、空格符等），相等于[ \t\r\n\v\f]。
\S 匹配非空格的字符，相当于[^ \t\r\n\v\f]。
\b 匹配词的边界。
\B 匹配非词边界，即在词的内部。
```JavaScript
// \s 的例子
/\s\w*/.exec('hello world') // [" world"]

// \b 的例子
/\bworld/.test('hello world') // true
/\bworld/.test('hello-world') // true
/\bworld/.test('helloworld') // false

// \B 的例子
/\Bworld/.test('hello-world') // false
/\Bworld/.test('helloworld') // true

var html = "<b>Hello</b>\n<i>world!</i>";

/[\S\s]*/.exec(html)[0]
// "<b>Hello</b>\n<i>world!</i>" [\S\s]指代一切字符。
```
6.重复类
模式的精确匹配次数，使用大括号（{}）表示。{n}表示恰好重复n次，{n,}表示至少重复n次，{n,m}表示重复不少于n次，不多于m次。
```JavaScript
/lo{2}k/.test('look') //true
/lo{2,5}/.test('looook')  // true
```
7.量词符
用来设定某个模式出现的次数。
? 问号表示某个模式出现0次或1次，等同于{0, 1}。
* 星号表示某个模式出现0次或多次，等同于{0,}。
+ 加号表示某个模式出现1次或多次，等同于{1,}。
8.贪婪模式
量词符默认情况下都是最大可能匹配，即匹配到下一个字符不满足匹配规则为止。这被称为贪婪模式。只要一发现匹配就返回结果，不在继续检查成为非贪婪模式。如果想将贪婪模式改为非贪婪模式，可以在量词符后面加一个问号。+?表示只要发现一个a，就不再往下匹配了。
+?：表示某个模式出现1次或多次，匹配时采用非贪婪模式。
*?：表示某个模式出现0次或多次，匹配时采用非贪婪模式。
??：表格某个模式出现0次或1次，匹配时采用非贪婪模式。
```JavaScript
'abb'.match(/ab*/) // ["abb"]
'abb'.match(/ab*?/) // ["a"]
'abb'.match(/ab?/) // ["ab"]
'abb'.match(/ab??/) // ["a"]
```
/ab*/表示如果a后面有多个b，那么匹配尽可能多的b；/ab*?/表示匹配尽可能少的b，也就是0个b。`
9.修饰符
修饰符（modifier）表示模式的附加规则，放在正则模式的最尾部。
g修饰符：表示全局匹配，匹配全部符合条件的结果，主要用于搜索和替换。
i修饰符:默认情况下，正则对象区分字母的大小写，加上i修饰符以后表示忽略大小写（ignoreCase）。
m修饰符：
10.组匹配
正则表达式的括号表示分组匹配，括号中的模式可以用来匹配分组的内容。
```JavaScript
/fred+/.test('fredd') // true  没有括号+只表示重复字母d
/(fred)+/.test('fredfred') // true 有括号+表示匹配fred这个词
var m = 'abcabc'.match(/(.)b(.)/);
m  // ['abc', 'a', 'c']
```
正则表达式/(.)b(.)/一共使用两个括号，第一个括号捕获a，第二个括号捕获c。
注意，使用组匹配时，不宜同时使用g修饰符，否则match方法不会捕获分组的内容。
非捕获组：表示不返回该组匹配的内容，即匹配的结果中不计入这个括号。
```JavaScript
var m = 'abc'.match(/(?:.)b(.)/);
m // ["abc", "c"]
```
# JSON对象
JSON是用于数据交换的文本格式，JSON的优点是书写简单，解释引擎可直接处理。每个JSON对象都只能是一个值。
JSON对值的规定：复合类型的值只能是对象或数组；原始类型值只有字符串、数值(十进制)、布尔值和null；字符串必须使用双引号；对象键名必须放在双引号里面；数组或对象最后一个成员的后面不能加逗号。
JSON对象是JavaScript的原生对象，用来处理JSON格式数据。它有一下两个静态方法:
1.JSON.stringify:用于将一个值转为 JSON 字符串。该字符串符合 JSON 格式。
如果对象的属性是undefined、函数或 XML 对象，该属性会被JSON.stringify()过滤。
如果数组的成员是undefined、函数或 XML 对象，则这些值被转成null。
```JavaScript
var obj = {
  a: undefined,
  b: function () {}
};
JSON.stringify(obj) // "{}"
var arr = [undefined, function () {}];
JSON.stringify(arr) // "[null,null]"
```
JSON.stringify()方法还可以接受一个数组，作为第二个参数，指定参数对象的哪些属性需要转成字符串。
```JavaScript
var obj = {
  'prop1': 'value1',
  'prop2': 'value2',
  'prop3': 'value3'
};
var selectedProperties = ['prop1','prop2'];
JSON.stringify(obj, selectedProperties)
//"{"prop1":"value1","prop2":"value2"}"
```
递归处理中，每一次处理的对象，都是前一次返回的值。
```JavaScript
function f(key, value) {
  console.log("["+ key +"]:" + value);
  if(typeof value === 'object') {
    return {b:2};
  }
  return value * 2 ; 
}
JSON.stringify(obj, f)
//[]:[object Object] 第一次键名为空，键值是整个对象obj
//[b]:2 
//'{"b":4}'
```
如果处理函数返回undefined或没有返回值，则该属性会被忽略。
```JavaScript
function f(key, value) {
  if (typeof(value) === "string") {
    return undefined;
  }
  return value;
}
JSON.stringify({ a: "abc", b: 123 }, f)
// '{"b": 123}'
```
如果参数对象有自定义的toJSON()方法，那么JSON.stringify()会使用这个方法的返回值作为参数，而忽略原对象的其他属性。

2.JSON.parse:用于将JSON字符串转换成对应的值。如果传入的字符串不是有效的 JSON 格式，JSON.parse()方法将报错。
为了处理解析错误，可以将JSON.parse()方法放在try...catch代码块中。
```JavaScript
try {
  JSON.parse("'String'"); //双引号字符串中是单引号字符串，不符合JSON格式
} catch(e) {
  console.log('parsing error');
}
```
JSON.parse()方法可以接受一个处理函数，作为第二个参数，用法与JSON.stringify()方法类似。
# 面向对象编程
## 实例对象与new命令
1.什么是对象？
对象就是单个实物的抽象；对象是一个容器，封装了属性（property）和方法（method）。属性是对象的状态，方法是对象的行为（完成某种任务）。
2.构造函数
面向对象编程的第一步，就是要生成对象。通常需要一个模板，表示某一类实物的共同特征，然后对象根据这个模板生成。JavaScript 语言的对象是基于构造函数（constructor）和原型链（prototype），使用构造函数（constructor）作为对象的模板，描述实例对象的基本结构。构造函数名字的第一个字母通常大写区别于普通函数。
构造函数的特点有两个：
1.函数体内部使用了this关键字，代表了所要生成的对象实例。
2.生成对象的时候，必须使用new命令。
## new命令
new命令就是执行构造函数，返回一个实例对象。如果不加new命令，构造函数会变成普通函数，不会生产实例对象，此时this代表全局对象。可以在构造函数内部使用严格模式`use strict`，避免不适用new命令而调用构造函数，程序会报错。
new命令的原理就是构造函数内部，this指向一个空对象，针对this上的操作都会发生在空对象上，将其“构造”成想要的样子。
构造函数内部有return语句，而且return后面跟着一个对象，new命令会返回return语句指定的对象；否则，就会不管return语句，返回this对象。但是，如果return语句返回的是一个跟this无关的新对象，new命令会返回这个新对象，而不是this对象。
```JavaScript
var Vehicle = function (){
  this.price = 1000;
  return { price: 2000 };
};
(new Vehicle()).price  // 2000
```
函数内部可以使用new.target属性。如果当前函数是new命令调用，new.target指向当前函数，否则为undefined。
## Object.create() 创建实例对象 
以现有的对象作为模板，生成新的实例对象，这时就可以使用Object.create()方法。
## this关键字
this就是属性或方法“当前”所在的对象。在构造函数中表示实例对象。由于对象的属性可以赋给另一个对象，所以属性所在的当前对象是可变的，即this的指向是可变的。

this的使用场合：
1.全局环境；this指的是顶层对象window。
2.构造函数：this指向实例对象。
3.对象的方法；this的指向就是方法运行时所在的对象。若该方法赋值给另一个对象，this的指向就会改变。

如果this所在的方法不在对象的第一层，这时this只是指向当前一层的对象，而不会继承更上面的层。
```JavaScript
var a = {
  p: 'Hello',
  b: {
    m: function() {
      console.log(this.p);
    }
  }
};
a.b.m() // undefined
```
如果这时将嵌套对象内部的方法赋值给一个变量，this依然会指向全局对象。
```JavaScript
var a = {
  b: {
    m: function() {
      console.log(this.p);
    },
    p: 'Hello'
  }
};
var hello = a.b.m;
hello() // undefined
```
注意：
1.避免多层this，如果不能避免，解决方法如下：在第二层改用一个指向外层this的变量。
```JavaScript
var f = {
  a：function() {
    console.log(this);
    var that = this;  //变量that固定指向外层的this
    var b = function() {
      console.log(that); //在内层使用that，this指向就不会发生改变。
    }();
  }
}
f.a() 
//Object
//Object
```
2.避免数组处理方法中的this：数组的map和foreach方法，允许提供一个函数作为参数。这个函数内部不应该使用this。除了使用中间变量固定this，还可以将this作为forEach方法的第二个参数，固定运行环境。
```JavaScript
var o = {
  v: 'hello',
  p: [ 'a1', 'a2' ],
  f: function f() {
    this.p.forEach(function (item) {
      console.log(this.v + ' ' + item);
    }, this);
  }
}
o.f()
// hello a1
// hello a2
```
3.避免回调函数中的this：回调函数中的this往往会改变指向。
## 绑定this的方法
JavaScript 提供了call、apply、bind这三个方法，来切换/固定this的指向。
1.Function.prototype.call() ：可以指定函数内部this指向函数执行时所在的作用域，然后调用该函数。call方法的参数，应该是一个对象。如果参数为空、null和undefined，则默认传入全局对象。如果call方法的参数是一个原始值，那么这个原始值会自动转成对应的包装对象，然后传入call方法。
`func.call(thisvalue,arg1,arg2,...)`call的第一个参数就是this所要指向的那个对象，后面的参数则是函数调用时所需的参数。
2.Function.prototype.apply()：与call方法类似，唯一的区别就是它接收一个数组作为函数执行时的参数。
`func.apply(thisvalue,[arg1,arg2,...])`apply方法的第一个参数也是this所要指向的那个对象，如果设为null或undefined，则等同于指定全局对象。第二个参数则是一个数组，该数组的所有成员依次作为参数，传入原函数。
案例：找出数组最大元素,结合apply和Math.max方法
```JavaScript
var ary = [9,5,7,12,16];
Math.max.apply(null,ary) //16
```
案例：将数据的空元素变为undefined
```JavaScript
Array.apply(null,['a', ,'b']) 
//[ 'a', undefined, 'b' ]
```
空元素与undefined的差别在于，数组的forEach方法会跳过空元素，但是不会跳过undefined。因此，遍历内部元素的时候，会得到不同的结果。

案例：转换类似数组的对象，将对象转成数组。
这个方法起作用的前提是，被处理的对象必须有length属性，以及相对应的数字键。
```JavaScript
Array.prototype.slice.apply({0: 1, length: 1}) // [1]
Array.prototype.slice.apply({0: 1}) // []
Array.prototype.slice.apply({0: 1, length: 2}) // [1, undefined]
Array.prototype.slice.apply({length: 1}) // [undefined]
```
3.Function.prototype.bind():用于将函数体内的this绑定到某个对象，然后返回一个新函数。bind方法的参数就是所要绑定this的对象。
注意：每一次返回一个新函数；结合回调函数使用。
## 对象的继承
原型对象(prototype)：定义所有实例对象共享的属性和方法。
原型链：任何对象都有自己的原型，并且也可以充当其他对象的原型，因此就会形成一个“原型链”。所有对象的原型最终都可以上溯到Object.prototype，即Object构造函数的prototype属性，因此对象都有valueOf和toString方法。Object.prototype对象的原型是null，null没有任何属性和方法。因此原型链的尽头就是null。
prototype对象有一个constructor属性，默认指向prototype对象所在的构造函数。constructor属性的作用是可以得知某个实例对象，到底是哪一个构造函数产生的。constructor属性表示原型对象与构造函数之间的关联关系，如果修改了原型对象，一般会同时修改constructor属性。
instanceof运算符返回一个布尔值，表示对象是否为某个构造函数的实例。
## 构造函数的继承
一个构造函数继承另一个构造函数分为两步：第一步在子类的构造函数中调用父类的构造函数。第二部是让子类的原型指向父类的原型。
```JavaScript
Sub.prototype = Object.create(Super.prototype);
Sub.prototype.constructor = Sub;
Sub.prototype.method = '...';
```
Sub.prototype是子类的原型，要将它赋值为Object.create(Super.prototype)，而不是直接等于Super.prototype。否则后面两行对Sub.prototype的操作，会连父类的原型Super.prototype一起修改掉。
## Object对象的相关方法
1.Object.getPrototypeOf()：返回参数对象的原型。
特殊对象的原型
```JavaScript
// 空对象的原型是 Object.prototype
Object.getPrototypeOf({}) === Object.prototype // true
// Object.prototype 的原型是 null
Object.getPrototypeOf(Object.prototype) === null// true
// 函数的原型是 Function.prototype
function f() {}
Object.getPrototypeOf(f) === Function.prototype // true
```
2.Object.setPrototypeOf():为参数对象设置原型，返回该参数对象。接收两个参数，第一个是现有对象，第二个是原型对象。
使用setPrototypeOf方法模拟new命令
```JavaScript
var F = function () {
  this.foo = 'bar';
};
var f = new F(); //等同于
var f = Object.setPrototypeof({},F.prototype);
F.call(f);
```
3.Object.create()：接收一个对象作为参数，以它为原型返回一个实例对象，该实例完全继承原型对象的属性。Object.create()方法生成的新对象，动态继承了原型。在原型上添加或修改任何方法，会立刻反映在新对象之上。
三种生产新对象的方式：
```JavaScript
var obj1 = Object.create({});
var obj2 = Object.create(Object.prototype);
var obj3 = new Object();
```
4.Object.prototype.isPrototypeOf()：用来判断该对象是否为参数对象的原型。Object.prototype处于原型链的最顶端，所以对各种实例都返回true，对继承自null的对象返回false。
5.Object.prototype.__proto__：proto的前后都是两个下划线，返回该对象的原型，这个属性可读写。
`obj.__proto__ = p;//将p对象设为obj对象的原型`
6.Object.getOwnPropertyNames()：返回一个数组，成员是参数对象本身的所有属性的键名，不包含继承的属性键名。
7.Object.prototype.hasOwnProperty()：返回一个布尔值，判断某个属性定义在对象自身还是原型链上。
8.in运算符和for...in循环：
in运算符返回一个布尔值表示对象是否具有某个属性。不区分属性是对象自身还是继承的属性。通常用于检查一个属性是否存在。
for...in循环获得对象所有可遍历属性，不管是自身的还是继承的。
# DOM
DOM 是 JavaScript 操作网页的接口，全称为“文档对象模型”。它的作用是将网页转为一个 JavaScript 对象，从而可以用脚本进行各种操作（比如增删内容）。
## 节点
DOM 的最小组成单位叫做节点（node）。浏览器提供一个原生节点Node，下面七种节点类型都继承了Node。
1.Document：整个文档树的顶层节点
2.DocumentType：doctype标签（比如<!DOCTYPE html>）
3.Element：网页的各种HTML标签（比如<body>、<a>等）
4.Attr：网页元素的属性（比如class="right"）
5.Text：标签之间或标签包含的文本
6.Comment：注释
7.DocumentFragment：文档的片段
## Node接口
所有 DOM 节点对象都继承了 Node 接口，拥有一些共同的属性和方法。
### 属性：
1.Node.prototype.nodeType ：返回一个整数值，表示节点的类型。
不同节点的nodeType属性值对应常量如下：
文档节点(document)：9，对应常量Node.DOCUMENT_NODE
元素节点(element):1,对应常量Node.ELEMENT_NODE
属性节点(attr):2,对应常量Node.ATTRIBUTE_NODE
文本节点(text):3，对应常量Node.TEXT_NODE
文档片段节点(DocumentFragment):11,对应常量Node.DOCUMENT_FRAGMENT_NODE
文档类型节点(DocumentType):10,对应常量Node.DOCUMENT_TYPE_NODE
注释节点(Comment):8,对应常量Node.COMMENT_NODE
2.Node.prototype.nodeName:返回节点的名称。
不同节点的nodeName属性值如下。
文档节点（document）：#document
元素节点（element）：大写的标签名
属性节点（attr）：属性的名称
文本节点（text）：#text
文档片断节点（DocumentFragment）：#document-fragment
文档类型节点（DocumentType）：文档的类型
注释节点（Comment）：#comment
3.Node.prototype.nodeValue :返回一个字符串，表示当前节点本身的文本值，该属性可读写。
只有文本节点（text）、注释节点（comment）和属性节点（attr）有文本值，因此这三类节点的nodeValue可以返回结果，其他类型的节点一律返回null。
```JavaScript
// HTML 代码如下
// <div id="d1">hello world</div>
var div = document.getElementById('d1');
div.nodeValue // div是元素节点，返回null
div.firstChild.nodeValue // firstchild是文本节点，返回"hello world"
```
4.Node.prototype.textContent :返回当前节点和它的所有后代节点的文本内容。对于文本节点（text）、注释节点（comment）和属性节点（attr），textContent属性的值与nodeValue属性相同。对于其他类型的节点，该属性会将每个子节点（不包括注释节点）的内容连接在一起返回。如果一个节点没有子节点，则返回空字符串。文档节点（document）和文档类型节点（doctype）的textContent属性为null。如果要读取整个文档的内容，可以使用document.documentElement.textContent。
5.Node.prototype.baseURI:返回一个字符串，表示当前网页的绝对路径。浏览器会根据此属性计算网页上的相对路径的URL。如果无法读到网页的 URL，baseURI属性返回null。可以通过hmtl的base标签改变该属性的值。
6.Node.prototype.ownerDocument:返回当前节点所在的顶层文档对象，即document对象。document对象本身的ownerDocument属性，返回null。
7.Node.prototype.nextSibling:返回紧跟在当前节点后面的第一个同级节点。没有同级节点则返回null。注意，该属性还包括文本节点和注释节点（<!-- comment -->）。因此如果当前节点后面有空格，该属性会返回一个文本节点，内容为空格。
nextSibling属性遍历所有子节点：
```JavaScript
var e = document.getElementById('div1').firstChild;
while (e !== null) {
  console.log(e.nodeName);
  e = e.nextSibling;
}
```
8.Node.prototype.previousSibling：返回当前节点前面的、距离最近的一个同级节点。没有同级节点则返回null。注意，该属性还包括文本节点和注释节点。因此如果当前节点前面有空格，该属性会返回一个文本节点，内容为空格。
9.Node.prototype.parentNode：返回当前节点的父节点。对于一个节点来说，它的父节点只可能是三种类型：元素节点（element）、文档节点（document）和文档片段节点（documentfragment）。文档节点（document）和文档片段节点（documentfragment）的父节点都是null。
10.Node.prototype.parentElement：返回当前节点的父元素节点。如果没有父节点或者父节点类型不是元素节点，则返回null。
11.Node.prototype.firstChild：返回当前节点的第一个子节点，没有则返回null。注意，firstChild返回的除了元素节点，还可能是文本节点或注释节点。
```JavaScript
// HTML 代码如下
// <p id="p1">
//   <span>First span</span>
//  </p>
var p1 = document.getElementById('p1');
p1.firstChild.nodeName // "#text"   P元素和span元素直接有空白字符，所以返回的是文本节点
```
Node.prototype.lastChild：返回当前节点的最后一个子节点，没有则返回null。
12.Node.prototype.childNodes：返回一个类似数组的对象(Nodelist集合)，成员包括当前节点的所有子节点。文档节点（document）就有两个子节点：文档类型节点（docType）和 HTML 根元素节点。
```JavaScript
var children = document.childNodes;
for (var i = 0; i < children.length; i++) {
  console.log(children[i].nodeType);
}
// 10  文档节点
// 1   元素节点
```
注意，除了元素节点，childNodes属性的返回值还包括文本节点和注释节点。如果当前节点不包括任何子节点，则返回一个空的NodeList集合。
13.Node.prototype.isConnected：返回一个布尔值，表示当前节点是否在文档中。
### 方法
1.Node.prototype.appendChild()：接受一个节点对象作为参数，将其作为最后一个子节点，插入当前节点。返回值是插入文档的子节点。如果参数节点是 DOM 已经存在的节点，appendChild()方法会将其从原来的位置，移动到新位置。如果appendChild()方法的参数是DocumentFragment节点，那么插入的是DocumentFragment的所有子节点，而不是DocumentFragment节点本身。返回值是一个空的DocumentFragment节点。
2.Node.prototype.hasChildNodes()：返回一个布尔值，表示当前节点是否有子节点。注意：子节点包括所有类型的节点，并不仅仅是元素节点。哪怕节点只包含一个空格，hasChildNodes方法也会返回true。
判断一个节点是否有子节点的三种方法：
node.hasChildNodes()
node.firstChild !== null
node.childNodes && node.childNodes.length > 0
3.Node.prototype.cloneNode()：用于克隆一个节点。它接受一个布尔值作为参数，表示是否同时克隆子节点。它的返回值是一个克隆出来的新节点。
4.Node.prototype.insertBefore()：用于将某个节点插入父节点内部的指定位置。第一个参数是要插入的节点，第二个参数是父节点内部的一个子节点。如果第二个参数为null，新节点将插在当前节点的最后位置，变成最后一个子节点。
新建的P节点成为documen.body的第一个子节点：
```JavaScript
var p = document.createElement('p');
document.body.insertBefore(p, document.body.firstChild);
```
新节点要插在父节点的某个子节点后面，可以用insertBefore方法结合nextSibling属性
`parent.insertBefore(s1,s2.nextSibling);`
5.Node.prototype.removeChild():接受一个子节点作为参数，用于从当前节点移除该子节点。返回值是移除的子节点。
移除当前节点的所有子节点:
```JavaScript
var element = document.getElementById('top');
while (element.firstChild) {
  element.removeChild(element.firstChild);
}
```
6.Node.prototype.replaceChild():用于将一个新的节点，替换当前节点的某一个子节点。返回值是替换走的节点。
`var replacedNode = parentNode.replaceChild(newChild,oldChild)`
7.Node.prototype.contains():返回一个布尔值，表示参数节点是否满足以下三个条件之一。
参数节点为当前节点。
参数节点为当前节点的子节点。
参数节点为当前节点的后代节点。
8.Node.prototype.compareDocumentPosition()
:与contains方法完全一致，返回一个六个比特位的二进制值，表示参数节点与当前节点的关系。
9.Node.prototype.isEqualNode():返回一个布尔值，用于检查两个节点是否相等。所谓相等的节点，指的是两个节点的类型相同、属性相同、子节点相同。
Node.prototype.isSameNode():返回一个布尔值，表示两个节点是否为同一个节点。
10.Node.prototype.normalize():用于清理当前节点内部的所有文本节点（text）。
11.Node.prototype.getRootNode:返回当前节点所在文档的根节点document，与ownerDocument属性的作用相同。
