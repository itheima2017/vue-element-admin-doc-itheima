# 授权

其实权限问题，可以设计的很复杂，我们通过研究考虑以轻量级的方式开始项目为基线。

后台权限分为两个方面 `权限` `权限点`：

* **权限** 用户可以使用的菜单、路由
* **权限点** 用户在单个页面可以使用的功能

## 第一步：配置路由

假设已有模块目录 `/src/module-example`

### 创建 `/src/module-example/router/index.js`

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

### 注册路由 `/src/router/index.js`

```js
// 导入模块路由
import {ExampleRouter} from '@/module-example/router'

/**
 * 合并业务路由
 **/
routerMap = routerMap.concat(ExampleRouter)
```

## 第二步：菜单管理

添加你的新页面 `代码` `标题`

?> 代码是全局唯一的

## 第三步：权限组授权

权限组授权中勾选需要的菜单项
