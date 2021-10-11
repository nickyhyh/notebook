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