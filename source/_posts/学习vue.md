---
title: 学习vue
---
# Vue框架的特点
1.模板渲染：基于 html 的模板语法，学习成本低。

2.响应式的更新机制：数据改变之后，视图会自动刷新。【重要】

3.渐进式框架

4.组件化/模块化

5.轻量：开启 gzip压缩后，可以达到 20kb 大小

# 利用 vue-cli 新建一个空的项目
## 安装 vue-cli（命令行工具
`# 全局安装 vue-cli`
`$ npm install -g @vue/cli`
## 初始化一个 simple 项目
1.` vue create my-app`
如果初学者，直接选default就行。之后会自动生成一个空的初始化项目，包含了项目目录、以及项目依赖的脚本

buid：打包配置的文件夹

config：webpack对应的配置

src：开发项目的源码

App.vue：入口组件。.vue文件都是组件。
main.js：项目入口文件。
static：存放静态资源

.babelrc：解析ES6的配置文件

.editorcofnig：编辑器的配置

.postcssrc.js：html添加前缀的配置

index.html：单页面的入口。通过 webpack打包后，会把 src 源码进行编译，插入到这个 html 里面来。

package.json：项目的基础配置，包含版本号、脚本命令、项目依赖库、开发依赖库、引擎等。

2.2）本地运行项目：
` cd my-app`
 ` npm run serve`
 浏览器输入http://localhost:8080/，就可以让这个空的项目在本地跑起来
 备注：我们在 GitHub上下载的任何Vue有关的项目，第一步都是要首先执行 npm install，安装依赖的 mode_modules，然后再运行。

# html中导入vue
 <!--1、导入Vue的包-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>



# vue语法
v-cloak：保持和元素实例的关联，直到结束编译后自动消失。v-cloak指令和CSS 规则一起用的时候，能够解决差值表达式闪烁的问题（即：可以隐藏未编译的标签直到实例准备完毕。

v-bind : 用于绑定属性。  简写 ：属性名

v-text ：会覆盖元素中原本的内容,可以将一个变量的值渲染到指定的元素中。
## 差值表达式和 v-text 的区别
1： v-text 没有闪烁的问题，因为它是放在属性里的。
2 :插值表达式只会替换自己的这个占位符，并不会把整个元素的内容清空。

v-html :会被解析成html元素
# v-on：事件绑定机制
v-on:click：点击事件
v-on的简写形式：
`<button v-on:click="change">改变name的值</button>`
可以简写成：
`<button @click="change">改变name的值</button>`

# v-on的常见事件修饰符
## .stop 阻止冒泡。本质是调用 event.stopPropagation()
例子：
```JavaScript
<body>
    <div id="app">
        <div class="father" @click="fatherClick">
            <div class="child" @click="childClick">
            </div>
        </div>
    </div>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {},
            methods: {
                fatherClick: function () {
                    console.log('father 被点击了');
                },
                childClick: function () {
                    console.log('child 被点击了');
                }
            }
        })
    </script>
</body>
```
上方代码中，存在冒泡的现象，父标签中包含了一个子标签。当点击子标签时，父标签也会被触发。打印顺序是：
  child 被点击了
  father 被点击了
如果我不想让子标签的点击事件冒泡到父亲，该怎么做呢？办法是：给子标签加一个事件修饰符.stop，阻止冒泡。代码如下：
`<div class="child" @click.stop="childClick">`
阻止冒泡后，当点击子标签时，打印结果是：
 child 被点击了

## .capture：触发事件时，采用捕获的形式，而不是冒泡的形式。
还是采用上面的例子：当按钮点击时，如果想要采取捕获的方式，而不是冒泡的方式，办法是：可以直接在父标签上加事件修饰符.capture。代码如下：
`<div class="father" @click.capture="fatherClick">`
当点击子标签时，打印结果是：
  father 被点击了
  child 被点击了

## .prevent 阻止默认事件（默认行为）。本质是调用 event.preventDefault()。
表单的默认行为：点击按钮后表单就会被提交到form标签的action属性中指定的那个页面中去，
```JavaScript
 <form action="http://www.baidu.com">
      <input type="submit" value="表单提交">
    </form>
```
修改为点击按钮后，不提交到服务器，而是执行我们自己想要的事件（在submit方法中另行定义）。如下：
```JavaScript
<body>
  <div id="app">
    <!-- 阻止表单中submit的默认事件 -->
    <form @submit.prevent action="http://www.baidu.com">
      <!-- 执行自定义的click事件 -->
      <input type="submit" @click="mySubmit" value="表单提交">
    </form>
  </div>
</body>
<script>
  new Vue({
    el: '#app',
    data: {
    },
    methods: {
      mySubmit: function() {
        alert('ok');
      }
    }
  });
</script>
```
## .self 只有当事件在该元素本身（比如不是子元素）触发时，才会触发回调。
在事件触发机制中，当点击子标签时，父标签会通过冒泡的形式被触发（父标签本身并没有被点击）。可如果我给父标签的点击事件设置.self修饰符，达到的效果是：子标签的点击事件不会再冒泡到父标签了，只有点击符标签本身，父标签的事件才会被触发。
`<div class="father" @click.self="fatherClick">`
.stop和.self都可以阻止冒泡，二者的区别在于：前者能够阻止整个冒泡行为，而后者只能阻止自己身上的冒泡行为。

v-if : 不显示P标签
v-show : 显示P标签，<p style="display:none">现在你看到我了</p>
seen为true时，v-if和v-show没有差别，都显示P标签内容。
seen为false时,页面不显示内容，但是html里显示p标签。

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
定义一个名为todo-item的组件2秒后销毁组件
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
# 创建hello项目
`vue create hello-world`

# 创建网页
1.views文件夹中创建FirstPage.vue
```javascript
<template>
  <div class="FirstPage">
    <h1>This is an FirstPage</h1>
  </div>
</template>
```
2.router文件夹下index.js中引用FirstPage.vue
```javascript
const routes = [{
         {
        path: '/FirstPage',
        name: 'FirstPage',
        component: () =>
            import ( /* webpackChunkName: "about" */ '../views/FirstPage.vue')
    }]
```
component有两种定义方式
```javascript
import SecondPage from '../views/SecondPage.vue'
{
        path: '/SecondPage',
        name: 'SecondPage',
        component: SecondPage
    },
```
```javascript
{
        path: '/SecondPage',
        name: 'SecondPage',
        component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
 },
```
Home.vue中自定义了HelloWorld元素，引用到HelloWorld.vue
`import HelloWorld from '@/components/HelloWorld.vue'`
HelloWorld.vue中引用HelloWorld元素
```javascript
<template>
  <div class="hello">
   <h1>{{ msg }}</h1>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>
```
router文件是针对App.vue的路由，对应的内容全部都会显示在<router-view></router-view>中，App.vue会自动寻找这一些组件，比如，在目前的index.js中，path显示的是“/”这就意味着当页面打开到App.vue，而没有增加其他的url后缀的时候 （http://localhost:8080/#/），App.vue会自动载入HelloWorld这个组件。

# vue-router中children使用方法
router:index.js
```javascript
const routes = [{
        path: '/',
        name: 'Home',
        component: Home,
        children: [{
            path: '/page1',
            name: 'page1',
            component: function() {
                return import ( /* webpackChunkName: "about" */ '../views/FirstPage.vue')
            }
        }]
    }]
```
Home.vue
``` JavaScript
<template>
  <div class="home">
    <span><router-link to="/page1">导航一</router-link></span>
   <router-view></router-view>
  </div>
</template>
```

# Vue 内置的按键修饰符
## v-on的按键修饰符
Vue 允许为 v-on 在监听键盘事件时添加按键修饰符，例如：
@keyup.enter="addData"表示：按住enter键后，执行addData()方法。全称是v-on:key.enter="addData"
## 自定义全局按键修饰符
（1）使用Vue.directive()自定义全局指令
自定义全局指令 v-focus：让文本框自动获取焦点
参数1：指令的名称。注意，在定义的时候，指令的名称前面，不需要加 v- 前缀；但是：在`调用`的时候，必须在指令名称前加上 v- 前缀
参数2：是一个对象，这个对象身上，有一些指令相关的函数，这些函数可以在特定的阶段，执行相关的操作
```javascript
    Vue.directive('focus',
     {bind: function (el)  //每当指令绑定到元素上的时候，会立即执行这个 bind 函数，【只执行一次】, 在元素刚绑定了指令的时候，还没有插入到 DOM中去，这时候调用 focus 方法没有作用,因为一个元素只有插入DOM之后，才能获取焦点
    },
     {inserted: function (el) {  // inserted 表示元素插入到DOM中的时候，会执行 inserted 函数【触发1次】
            el.focus()
    },
     {updated: function (el) {  // 当VNode更新的时候，会执行 updated， 【可能会触发多次】 },
     })
```
（2）在指定的文本框上加``：

# 单元素/组件的过渡
Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加进入/离开过渡

# 动画进入：
v-enter：动画进入之前的初始状态
v-enter-to：动画进入之后的结束状态
v-enter-active：动画进入的时间段
# 动画离开：
v-leave：动画离开之前的初始状态
v-leave-to：动画离开之后的结束状态
v-leave-active：动画离开的时间段
### v-enter-to和v-leave的状态是一样的。而且一般来说，v-enter和v-leave-to的状态也是一致的。所以，我们可以把这四个状态写成两组。

# Vue组件的定义和注册
组件：就是为了拆分Vue实例的代码量的，能够让我们以不同的组件，来划分不同的功能模块，将来我们需要什么样的功能，就可以去调用对应的组件即可。
## 全局组件的定义和注册
使用Vue.extend方法定义组件，使用 Vue.component方法注册组件
一种写法：
```html
<body>
    <div id="app">
        <!-- 如果要使用组件，直接把组件的名称，以 HTML 标签的形式，引入到页面中，即可 -->
        <account> </account>
    </div>
    <script>
        //第一步：使用 Vue.extend 定义组件
        var myAccount = Vue.extend({
            template: '<div><h2>登录页面</h2> <h3>注册页面</h3></div>' // 通过 template 属性，指定了组件要展示的HTML结构。template 是 Vue 中的关键字，不能改。
        });
        //第二步：使用 Vue.component 注册组件
        // Vue.component('组件的名称', 创建出来的组件模板对象)
        Vue.component('account', myAccount); //第一个参数是组件的名称（标签名），第二个参数是模板对象
        new Vue({
            el: '#app'
        });
    </script>
</body>
```
推荐写法：
``` html
<body>
    <!-- 定义模板 -->
    <template id="myAccount">
        <div>
            <h2>登录页面</h2>
            <h3>注册页面</h3>
        </div>
    </template>
    <div id="app">
        <!-- 使用组件 -->
        <account> </account>
    </div>
    <script>
        //定义、注册组件
        Vue.component('account', {
            template: '#myAccount'    // template 是 Vue 中的关键字，不能改。
        });
        new Vue({
            el: '#app'
        });
    </script>
</body>
```
## components定义私有组件
```JavaScript
 <div id="app">
        <!-- 使用Vue实例内部的私有组件 -->
        <my-login></my-login>
        </div>
<script>
        new Vue({
            el: '#app',
            data: {},
            components: { // 定义、注册Vue实例内部的私有组件
                myLogin: {
                    template: '<h3>这是私有的login组件</h3>'
                }
            }
        });
```
## Vue提供的<component>标签实现多个组件切换
两个组件切换
```HTML
 <div id="app">
        <!-- 【重要】component 是一个占位符, `:is` 属性,可以用来指定要展示的组件名称。这里，我们让 login组件显示出来 -->
        <component :is="'login'"></component>
    </div>
    <script>
        // 组件名称是 字符串
        Vue.component('login', {
            template: '<h3>登录组件</h3>'
        })
        Vue.component('register', {
            template: '<h3>注册组件</h3>'
        })
        // 创建 Vue 实例，得到 ViewModel
        var vm = new Vue({
            el: '#app',
            data: {
                comName: 'login' // 当前 component 中的 :is 绑定的组件的名称
            },
            methods: {}
        });
```
``` HTML
<!-- 点击按钮后，设置变量`comName`为不同的值，代表着后面的component里显示不同的组件 -->
         <a href="" @click.prevent="comName='login'">登录</a>
        <a href="" @click.prevent="comName='register'">注册</a>
        <!-- 此处的`comName`是变量，变量值为组件名称 -->
        <component :is="comName"></component>
```
多个组件切换时，通过mode属性添加过渡的动画
``` HTML
 <div id="app">
        <a href="" @click.prevent="comName='login'">登录</a>
        <a href="" @click.prevent="comName='register'">注册</a>
        <!-- 通过 mode 属性,设置组件切换时候的 过渡动画 -->
        <!-- 【重点】亮点是 mode="out-in" 这句话 -->
        <transition mode="out-in">
            <component :is="comName"></component>
        </transition>
    </div>
```
多个组件切换时，如果要设置动画，可以用<transition>把组件包裹起来。需要注意的是，我给<transition>标签里添加了mode="out-in"这种模式，它表示第一个组件消失之后，第二个组件才会出现。如果没有这个mode属性，第一个组件准备消失的时候，第二个组件马上就准备出现。