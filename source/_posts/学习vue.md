---
title: 学习vue
---
seen为true时，v-if和v-show没有差别，都显示P标签内容。
seen为false时,页面不显示内容，但是html里显示p标签
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