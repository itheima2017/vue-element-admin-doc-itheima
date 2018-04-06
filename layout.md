# 布局

了解一个后台项目，先要了解它的基础布局。页面整体布局是一个产品最外层的框架结构，往往会包含导航、侧边栏、面包屑以及内容等。

## Layout

> 对应代码目录: `/src/module-dashboard/pages/layout.vue`

大部分页面都是基于这个`layout`的，除了个别页面如 `login` , `404`, `401` 等页面没有使用该`layout`。如果你想在一个项目中有多种不同的`layout`也是很方便的，只要在一级路由那里选择不同的`layout`组件就行。

```js
//no layout
{
  path: '/401',
  component: _import('errorPage/401')
}

//has layout
{
  path: '/documentation',
  //你可以选择不同的layout组件
  component: Layout,

  //这里开始对应的路由都会显示在app-main中 如上图所示
  children: [{
    path: 'index',
    component: _import('documentation/index'),
    name: 'documentation'
  }]
}
```

这里使用了 vue-router [路由嵌套](https://router.vuejs.org/zh-cn/essentials/nested-routes.html), 所以一般情况下，你增加或者修改页面只会影响 `app-main`这个主体区域， 其它如侧边栏或者导航栏都不会发生变化。

当然你也可以一个项目里面使用多个不同的 `layout`，只要在你想作用的路由父级引用它就可以了。

## app-main

> 对应代码目录: `/src/module-dashboard/components/layoutAppMain.vue`

这里在 `app-main` 外部包了一层 `keep-alive` 主要是为了缓存 `<router-view>`的，配合页面的 `layoutTags` 标签导航使用，如不需要可自行 去除 `layoutTags`。

### router-view

different router the same component vue。真实的业务场景中，这种情况很多。比如

![](img/different-router.jpeg)

我创建和编辑的页面使用的是同一个component,默认情况下当这两个页面切换时并不会触发vue的created或者mounted钩子，官方说你可以通过watch $route的变化来做处理，但其实说真的还是蛮麻烦的。后来发现其实可以简单的在 router-view上加上一个唯一的key，来保证路由切换时都会重新渲染触发钩子了。这样简单的多了。

```js
<router-view :key="key"></router-view>

computed: {
  key() {
    // 或者 :key="$route.path" 只要保证key唯一就可以了
    return this.$route.name !== undefined? this.$route.name + +new Date(): this.$route + +new Date()
  }
 }
```

> 可以声明 `editForm` 和 `createForm` 两个不同的 view 但引入同一个component。

```html
//create.vue
<template>
  <article-detail :is-edit='false'></article-detail> //create
</template>
<script>
  import ArticleDetail from './components/ArticleDetail'
</script>

//edit.vue
<template>
   <article-detail :is-edit='true'></article-detail> //edit
</template>
<script>
  import ArticleDetail from './components/ArticleDetail'
</script>
```
