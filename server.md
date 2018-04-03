# 和服务端进行交互

## 前端请求流程

在 黑马Admin 中，一个完整的前端 UI 交互到服务端处理流程是这样的：

1. UI 组件交互操作；
3. 调用统一管理的 api service 请求函数；
4. 使用封装的 request.js 发送请求；
5. 获取服务端返回；
7. 更新 data；

从上面的流程可以看出，为了方便管理维护，统一的请求处理都放在 `src/api` 文件夹中，并且一般按照 model 纬度进行拆分文件，如：

```
api/
  frame.js
  menus.js
  users.js
  permissions.js
  ...
```

其中，`src/utils/request.js` 是基于 [axios](https://github.com/axios/axios) 的封装，便于统一处理 POST，GET 等请求参数，请求头，以及错误提示信息等。具体可以参看 [request.js](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/utils/request.js)。
它封装了全局 `request拦截器`、`respone拦截器`、`统一的错误处理`、`统一做了超时，baseURL设置等`

### 一个请求 用户管理 的例子：

```js
// api/article.js
import {createAPI} from '@/utils/request'

export const list = data => createAPI('/base/users', 'get', data)
export const simple = data => createAPI('/base/users/simple', 'get', data)
export const add = data => createAPI('/base/users', 'post', data)
export const update = data => createAPI('/base/users', 'put', data)
export const remove = data => createAPI('/base/users', 'delete', data)
export const detail = data => createAPI('/base/users/:id', 'get', data)
```

?> `createAPI` 常规方式提交

?> `createFormAPI` 表单方式提交

### 修改 API 基础地址 `BASE_API`

* 编辑文件 `config/dev.cnv.js` 或者 `config/pro.cnv.js`

```js
'use strict'
const merge = require('webpack-merge')
const prodEnv = require('./prod.env')

module.exports = merge(prodEnv, {
  NODE_ENV: '"development"',
  BASE_API: '"api"'
})
```

?> `BASE_API` 就是基地址

### 是否启用代理

* 编辑文件 `config/index.js`

```js
...
module.exports = {
  dev: {
    // Paths
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {
      '/api': {
        target: 'https://www.easy-mock.com/mock/5ab213e33666166110a94928/admin',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    },
    ...
```

> 关闭请设置 `proxyTable: {}`
>
> 代理配置中有重写路径的选项：`pathRewrite` 设置后
>
> `http://yourserver/api/user/12` 变成 `http://apiserver/user/12`
