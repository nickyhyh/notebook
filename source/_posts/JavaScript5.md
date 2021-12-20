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
JSON.parse()方法可以接受一个处理函数，作为第二个参数，用法与JSON.stringify()方法类似。
