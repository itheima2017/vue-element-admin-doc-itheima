# Mock 数据

Mock 数据是前端开发过程中必不可少的一环，是分离前后端开发的关键链路。通过预先跟服务器端约定好的接口，模拟请求数据甚至逻辑，能够让前端开发独立自主，不会被服务端的开发所阻塞。

## Swagger

我司项目中通常使用 [swagger](https://swagger.io/) 由后端来模拟数据。
**swagger** 是一个 REST APIs 文档生成工具，可以跨平台从代码注释中自动生成，开源，支持大部分语言，社区好，总之非常不错，强烈推荐。

## Easy-mock

我们使用的是 [easy-mock](https://easy-mock.com/login) 来模拟数据。它是一个纯前端可视化，并且能快速生成 模拟数据 的持久化服务。非常的简单易用还能结合 `swagger` ，不管团队还是个人项目都值得一试。

> 地址 `https://www.easy-mock.com/mock/5ab213e33666166110a94928/admin`

## Mockjs

[mockjs](https://github.com/nuysoft/Mock) 生成的，它的原理是:拦截了所有的请求并代理到本地模拟数据，所以 network 中没有发出任何的请求发出。
