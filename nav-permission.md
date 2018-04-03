# 新增菜单

假设已有模块目录 `/src/module-example`

## 第一步：创建路由

创建 `/src/module-example/router/index.js`

```js
import Layout from '@/module-dashboard/pages/layout'
const _import = require('@/router/_import_' + process.env.NODE_ENV)

export const DashboardRouter = [
  {
    path: '/example',
    component: Layout,
    redirect: 'noredirect',
    name: 'base',
    meta: {
      title: 'example',
      icon: 'example'
    },
    children: [
      {
        path: 'my',
        component: _import('example/pages/my'),
        name: 'example-my',
        meta: {title: 'my'}
      }
    ]
  }
]
```

## 第二步：注册路由 `/src/router/index.js`

```js
// 导入模块路由
import {ExampleRouter} from '@/module-example/router'

/**
 * 合并业务路由
 **/
routerMap = routerMap.concat(ExampleRouter)
```

## 第三步：菜单管理

添加你的新页面 `代码` `标题`

?> 代码是全局唯一的

## 第四步：权限组授权

权限组授权中勾选需要的菜单项
