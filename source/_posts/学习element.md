# npm安装element
`npm i element-ui -S`

# container布局容器
```javascript
<el-container style="height:100vh">
  <el-header style="height: 60px; background-color: lightyellow">web</el-header>
  <el-container>
    <el-aside style="width: 200px; background-color: pink">aside</el-aside>
    <el-main>Main</el-main>
  </el-container>
</el-container>
```
# NavMenu 导航菜单
导航菜单默认为垂直模式，通过mode属性可以使导航菜单变更为水平模式。在菜单中通过submenu组件可以生成二级菜单。Menu 还提供了background-color、text-color和active-text-color，分别用于设置菜单的背景色、菜单的文字颜色和当前激活菜单的文字颜色。
## Menu Methods
open，close：展开或收起指定的 sub-menu
## Menu Events
open，close：sub-menu 展开或收起的回调
select：菜单激活回调，index: 收起的 sub-menu 的 index， indexPath: 收起的 sub-menu 的 index path
``` JavaScript
<el-menu class="el-menu-vertical-demo"
            @open="handleOpen"
            @close="handleClose"
            @select="select">
export default {
  name: "Home",
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    select(key, keyPath) {
      console.log(key, keyPath);
    },
  }
}
```
## 侧栏
通过el-menu-item-group组件可以实现菜单进行分组，分组名可以通过title属性直接设定，也可以通过具名 slot 来设定。
```JavaScript
<el-submenu index="2">
       <template slot="title">我的工作台</template>
    <el-menu-item index="2-1">选项1</el-menu-item>
    <el-menu-item index="2-2">选项2</el-menu-item>
    <el-menu-item index="2-3">选项3</el-menu-item>
  </el-submenu>
```
