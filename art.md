# 项目结构

## 后端

## 前端

```bash
├── assets                          | 资源
├── build                           | webpack编译配置
├── config                          | 全局变量
├── src                             | 源码
│   ├── api                         | 数据请求
│   ├── assets                      | 资源
│   ├── components                  | 组件
│   ├── mixins                      | mixins
│   ├── filters                     | vue filter
│   ├── icons                       | 图标
│   ├── lang                        | 多语言
│   ├── router                      | 路由
│   ├── store                       | 数据
│   ├── styles                      | 样式
│   ├── utils                       | 工具函数库
│   ├── module-dashboard            | 框架程序
│   │   ├── assets
│   │   ├── components
│   │   ├── pages
│   │   ├── router
│   │   └── store
│   ├── module-example              | 示例程序
│   │   ├── assets
│   │   ├── components
│   │   ├── pages
│   │   ├── router
│   │   └── store
│   ├── App.vue                     | app
│   ├── main.js                     | 主引导
│   └──  errorLog.js                | vue全局错误捕捉
├── dist                            | 编译发布目录
├── README.md
├── index.html                      | 页面模板
├── package.json                    | npn包配置
├── static
└── test                            | 测试
    ├── e2e
    └── unit
```

* 创建模块目录

> 每个业务模块独立目录，互不干扰
>
> 我们简化了每次构建的操作，执行 `npm` 命令

```bash
> module=example npm run art:create
```

自动创建模块目录

```bash
│   ├── module-example              // 业务模块目录
│   │   ├── assets                  // 静态资源 img font svg icon
│   │   ├── components              // 组件 vue
│   │   ├── pages                   // 页面 view
│   │   ├── router                  // 路由控制 vue-router
│   │   └── store                   // 数据管理 vuex
```
