---
title: 学习vue
---
v-bind : 属性名 简写 ：属性名
seen为true时，v-if和v-show没有差别，都显示P标签内容。
seen为false时,页面不显示内容，但是html里显示p标签。
v-if : 不显示P标签
v-show : 显示P标签，<p style="display:none">现在你看到我了</p>

``` javascript
var app = new Vue({
            el: '#app',
            data: {
                message: 'Hello Vue!',
                seen: false
            }
        })
```
v-for = "item in todo"
item.属性和item[属性]都可以访问到对象的属性值，区别在于item[属性]支持变量动态属性。

``` javascript
todo: [{ num: 'hello', num2: '456' },
       { num: '123', num2: '789' },
       { key: 'num', }]
```

# 实例生命周期钩子
每个 Vue 实例在被创建时都要经过一系列的初始化过程——如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做生命周期钩子的函数。

created：还未挂载到DOM，不能访问到$el属性，可用于初始化一些数据，但和DOM操作相关的不能在created中执行。
```javascript
<body>
    <div id="app">{{message}}</div>
    <script>
        var app = new Vue({
            data: {
                message: 'Hello Vue!',
            },
            el: '#app',
            created: function() {
                this.message = "speed"
            }
        })
    </script>
</body>
```
mounted：实例已经挂在到DOM，此时可以通过DOM API获取到DOM节点。
```javascript
Vue.component('todo-item', {
            props: ['todo'],
            template: '<li id="li">{{ todo.text }}</li>',
            created: function() {
                console.log(document.querySelector("#li"))
            },
            mounted: function() {
                console.log(document.querySelector("#li"))
            }
        })
        //document.querySelector:在页面上查找id="li"的元素
```
destroyed:Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。
创建了一个组件2秒后销毁组件
```javascript
 <div id="app">
        <todo-item v-if="show" :todo="todoitem"></todo-item>
    </div>
    <script>
        Vue.component('todo-item', {
            props: ['todo'],
            template: '<li>{{ todo.text }}</li>',
            destroyed: function() {
                console.log('组件已销毁')
            }
        })
        var app = new Vue({
            data: {
                todoitem: {
                    text: 'string'
                },
                show: true,
            },
            el: '#app',
            created: function() {
                var that = this
                setTimeout(function() {
                    that.show = false
                }, 2000)
            }
        })
    </script>
```