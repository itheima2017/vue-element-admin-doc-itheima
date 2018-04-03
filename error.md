# 错误处理

## 页面

**404**

页面级的错误处理由 `vue-router` 统一处理，所有匹配不到正确路由的页面都会进 `404`页面。

```js
{ path: '*', redirect: '/404' }
```

**401**

在`@/src/router/index.js`做了权限控制，所有没有权限进入该路由的用户都会被重定向到 `401`页面。

## 请求

项目里所有的请求都会走`@/utils/request.js`里面创建的的 axios 实例，它统一做了错误处理，`@/src/utils/request.js`。

你可以在`service.interceptors.response` respone 拦截器之中根据自己的实际业务统一针对不同的状态码或者根据自定义 code 来做错误处理。如：

```js

```

因为所以请求返回的是`promise`，所以你也可以自行`catch` 错误，做相对应的提示。

```js
getInfo()
  .then(res => {})
  .catch(err => {
    xxxx
  })
```

## 代码

本项目也做了代码层面的错误处理，如果你开启了`eslint`在编写代码的时候就回提示错误。

当然还有很多不能被`eslint`检查出来的错误，vue 也提供了全局错误处理钩子[errorHandler](https://vuejs.org/v2/api/#errorHandler)，所以本项目也做了相对应的错误收集。
