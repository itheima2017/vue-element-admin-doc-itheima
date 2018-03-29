# 快速上手

#### 第三步：创建并注册路由

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

编辑路由注册 `/src/router/index.js`

```js
// 导入模块路由
import {ExampleRouter} from '@/module-example/router'

/**
 * 合并业务路由
 **/
routerMap = routerMap.concat(ExampleRouter)
```

#### 第四步：进入 `菜单管理` 创建新建的模块页面

#### 第五步：进入 `授权管理` 进行用户授权

#### 第六步：菜单多语言（可选）

编辑 `/src/lang/zh.js` `/src/lang/zh.js`

```js
export default {
  route: {
    ...
    my: '我的'
  },
  ...
```

`router` 是菜单导航显示的标题，对应 `meta: {title: 'my'}` 中的 `title` 属性

#### 完成！

现在重新登录，即可看见新建的侧栏导航和对应的页面了。
