# 新增菜单

假设已有模块目录 `/src/module-example`

## 第一步：编辑路由

打开刚才自动创建的 `/src/module-example/router/index.js`

```js
import Layout from '@/module-dashboard/pages/layout'
const _import = require('@/router/import_' + process.env.NODE_ENV)

export default [
  {
    path: '/my-admin',
    component: Layout,
    redirect: 'noredirect',
    name: 'my-admin',
    meta: {
      title: 'my-admin',
      icon: 'component'
    },
    children: [
      {
        path: 'index',
        component: _import('my-admin/pages/index'),
        name: 'my-admin-index',
        meta: {title: 'index'}
      }
    ]
  }
]
```

?> 在 `children` 下维护你的模块页面路由

## 第二步：菜单管理

添加你的新页面 `代码` `标题`

?> 代码是全局唯一的

## 第三步：权限组授权

权限组授权中勾选需要的菜单项
