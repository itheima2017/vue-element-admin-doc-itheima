# 新增页面

## 第一步：创建业务模块目录

```bash
>> module=example npm run art:create

自动创建这些目录
│   ├── module-example          | example模块主目录
│   │   ├── assets              | 资源
│   │   ├── components          | 组件
│   │   ├── pages               | 页面
│   │   ├── router              | 路由
│   │   └── store               | 数据
```

> 每个模块所有的素材、页面、组件、路由、数据，都是独立的，方便大型项目管理，应为大项目会有很多子业务项目，它们之间的关系是平行的、低耦合、互不依赖。

## 第二步：编写业务界面

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

## 第三步：多语言配置（可选）

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
