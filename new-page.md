# 新增页面

## 编写业务界面

* 创建 `/src/module-example/pages/my.vue`

```html
<template>
  <div class="dashboard-container">
    my业务页面
  </div>
</template>

<script>

export default {
  name: 'example-my',
  components: {},
  data() {
    return {
    }
  },
  computed: {
  },
  created() {
  }
}
</script>
```

> 注意文件名 `驼峰格式` `首字小写`
>
> 页面请放在目录 `/src/module-example/pages/`
>
> 组件请放在目录 `/src/module-example/components/`
>
> 页面路由请修改 `/src/module-example/router/index.js`

## 可选：`i18n` 多语言配置

* 编辑 `/src/lang/zh.js` `/src/lang/zh.js`

```js
export default {
  route: {
    ...
    my: '我的'
  },
  ...
```

> `router` 是菜单导航显示的标题，对应 `meta: {title: 'my'}` 中的 `title` 属性
