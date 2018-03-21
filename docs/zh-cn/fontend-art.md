# 项目构建

## vue-cli 脚手架

```bash
> npm i -g vue-cli
> vue init webpack vue-element-admin-itheima
> cd vue-element-admin-itheima
> npm i

✔ Installed 58 packages
✔ Linked 0 latest versions
✔ Run 0 scripts
✔ All packages installed (used 27ms, speed 0B/s, json 0(0B), tarball 0B)

> npm satart

DONE  Compiled successfully in 2748ms
I Your application is running here: http://localhost:8080
```

> 打开浏览器 [http://localhost:8080](http://localhost:8080 'target=_brank')

?> mac系统 ，请 `sudo`

## 项目目录文件

```bash
├── assets
├── build
│   ├── build.js
│   ├── check-versions.js
│   ├── logo.png
│   ├── utils.js
│   ├── vue-loader.conf.js
│   ├── webpack.base.conf.js
│   ├── webpack.dev.conf.js
│   └── webpack.prod.conf.js
├── cd
├── config
│   ├── dev.env.js
│   ├── index.js
│   ├── prod.env.js
│   └── test.env.js
├── mkdir
├── src
│   ├── api
│   ├── assets
│   │   └── logo.png
│   ├── components
│   │   └── HelloWorld.vue
│   ├── mixins
│   ├── module-dashboard
│   │   ├── assets
│   │   ├── components
│   │   ├── pages
│   │   ├── router
│   │   └── store
│   ├── module-example
│   │   ├── assets
│   │   ├── components
│   │   ├── pages
│   │   ├── router
│   │   └── store
│   ├── router
│   │   └── index.js
│   ├── store
│   ├── App.vue
│   └── main.js
├── static
├── test
│   ├── e2e
│   │   ├── custom-assertions
│   │   ├── specs
│   │   ├── nightwatch.conf.js
│   │   └── runner.js
│   └── unit
│       ├── specs
│       ├── jest.conf.js
│       └── setup.js
├── README.md
├── index.html
└── package.json
```

## 创建模块目录

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
