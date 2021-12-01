---
title: 学习Element
---
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
# Dialog 对话框
需要设置visible属性，它接收Boolean，当为true时显示 Dialog。Dialog 分为两个部分：body和footer，footer需要具名为footer的slot。title属性用于定义标题，它是可选的，默认值为空。
## 弹出"注册成功"的提示
```html
<el-button type=input" @click="dialogVisible = true">立即创建</el-button>
<el-dialog
  title="提示"
  :visible.sync="dialogVisible"
  width="30%"
  :before-close="handleClose">
  <span>注册成功</span>
  <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
  </span>
</el-dialog>
```

```JavaScript
export default {
  data() {
    return {
      dialogVisible: false
    };
  },
  methods: {
    handleClose(done) {
      this.$confirm('确认关闭？')
        .then(_ => {
          done();
        })
        .catch(_ => {});
    }
  }
};
```
# Table 表格
用于展示多条结构类似的数据，可对数据进行排序、筛选、对比或其他自定义操作
## 创建一个可选择固定列和表头的表格
height属性固定表头，flex属性固定列，stripe属性可以创建带斑马纹的表格。
Table 组件是不具有竖直方向的边框的，如果需要可以使用border属性设置为true即可启用
``` html
<el-table
  :data="tableData"
  height="250"
  style="width: 100%"
  border
  >
  <el-table-column
    prop="name"
    label="名称"
    width="180">
  </el-table-column>
  <el-table-column
    prop="price"
    label="价格">
  </el-table-column>
</el-table>
```

```JavaScript
export default {
  data() {
    return {
      tableData: [{
        name: 'Applejuice',
        price: '20'
      }, {
        name: 'Lemmonjuice',
        price: '25'
      }, {
        name: 'watermelonjuice',
        price: '30'
      }, {
        name: 'Margojuice',
        price: '25'
      },{
        name: 'Applejuice',
        price: '20'
      }, {
        name: 'Lemmonjuice',
        price: '25'
      }, {
        name: 'watermelonjuice',
        price: '30'
      }, {
        name: 'Margojuice',
        price: '25'
      }]
    }
  }
}
```
# Form 表单
inline 属性可以让表单域变为行内的表单域
label-position 属性可以改变表单域标签的位置，可选值为 top、left，当设为 top 时标签会置于表单域的顶部
Form 组件提供了表单验证的功能，只需要通过 rules 属性传入约定的验证规则，并将 Form-Item 的 prop 属性设置为需校验的字段名即可

``` html
<el-form-item label="姓名">
  <el-input v-model="formLabelAlign.user" placeholder=""></el-input>
</el-form-item>
<el-form-item label="活动名称" prop="name">
  <el-input v-model="formLabelAlign.name"></el-input>
</el-form-item>
<el-form-item label="性别">
  <el-select v-model="formLabelAlign.region" placeholder="">
    <el-option label="男" value="man"></el-option>
    <el-option label="女" value="women"></el-option>
  </el-select>
</el-form-item>
```

``` javascript
export default {
  data() {
    return {
      labelPosition: "right",
      formLabelAlign: {
        user: "",
        region: "",
        name: "",
      },
      rules: {
        name: [
          { required: true, message: "请输入活动名称", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
      },
    };
  },
};
```
# Pagination 分页
layout设置需要显示的内容：prev表示上一页，pager表示页码列表，next表示下一页。jumper表示跳页元素，total表示总条目数，size用于设置每页显示的页码数量。pager-count属性可以设置最大页码按钮数。
```html
<div class="block">
  <span class="demonstration">页数较少时的效果</span>
  <el-pagination
    :page-size="20"
    :pager-count="11"
    layout="prev, pager, next" 
    :total="50">
  </el-pagination>
</div>
```
使用size-change和current-change事件来处理页码大小和当前页变动时候触发的事件。page-sizes接受一个整型数组，数组元素为展示的选择每页显示个数的选项。
``` html
<template>
  <div class="block">
    <span class="demonstration">完整功能</span>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      :page-sizes="[100, 200, 300, 400]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="400">
    </el-pagination>
  </div>
</template>
```
```javascript
<script>
  export default {
    methods: {
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`);
      }
    },
    data() {
      return {
        currentPage4: 4
      };
    }
  }
</script>
```