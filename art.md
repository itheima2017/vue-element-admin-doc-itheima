# 项目结构

## 后端
```bash
├── README.md
├── db                                                              | 初始化数据库文件目录
│   ├── _init.sql
│   └── init.sql                                                    | 初始化数据库文件
├── pom.xml                                                         | Maven配置文件
├── src
│   └── main
│       ├── java
│       │   └── itcast
│       │       └── research
│       │           ├── VueElementAdminApiApplication.java          | Springboot启动类
│       │           ├── config                                      | 项目相关配置
│       │           │   └── startup                                 | 自定义启动类
│       │           ├── controller                                  | Api控制器层
│       │           │   ├── other                                   | 控制器-其他
│       │           │   ├── permission                              | 控制器-权限相关
│       │           │   └── user                                    | 控制器-用户相关
│       │           ├── entity                                      | 实体
│       │           │   ├── other                                   | 实体-其他
│       │           │   ├── permission                              | 实体-权限相关
│       │           │   └── user                                    | 实体-用户相关
│       │           ├── exception                                   | 异常处理
│       │           ├── handler                                     | 切面及身份验证处理器
│       │           ├── repository                                  | JPA数据操作接口
│       │           │   ├── other                                   | 数据操作接口-其他
│       │           │   ├── permission                              | 数据操作接口-权限相关
│       │           │   └── user                                    | 数据操作接口-用户相关
│       │           ├── service                                     | 服务层
│       │           │   ├── other                                   | 服务-其他
│       │           │   ├── permission                              | 服务-权限相关
│       │           │   └── user                                    | 服务-用户相关
│       │           └── util                                        | 工具包
│       └── resources                                               | 资源文件
│           ├── _application.yml
│           └── application.yml                                     | Springboot配置文件
```

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
