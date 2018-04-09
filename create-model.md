# 新增模块

## 模块目录结构

```bash
│   ├── module-dashboard            | 框架程序
│   │   ├── assets
│   │   ├── components
│   │   ├── pages
│   │   ├── router
│   │   └── store
│   ├── module-example              | 示例程序
│   │   ├── assets
│   │   ├── components
│   │   ├── pages
│   │   ├── router
│   │   └── store
```

* 每个模块所有的素材、页面、组件、路由、数据，都是独立的，方便大型项目管理，
* 在实际项目中会有很多子业务项目，它们之间的关系是平行的、低耦合、互不依赖。

## 使用 npm 快捷命令创建

```bash
>> module=example npm run art:create

自动创建这些目录
│   ├── module-example          | example模块主目录
│   │   ├── assets              | 资源
│   │   ├── components          | 组件
│   │   ├── pages               | 页面
│   │   ├── router              | 路由
│   │   └── store               | 数据
```

* `example` 是新模块的名字

## 注册模块

* 编辑 `src/main.js`

```js
...
/*
* 注册 - 业务模块
*/
import dashboard from '@/module-dashboard/' // 面板
Vue.use(dashboard, store)
...
```

> 使用 `Vue.use` 方式注册
>
> 参数 `store` 表示注册状态管理
