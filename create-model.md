# 新增模块

## 使用 npm 快捷命令创建

```bash
>> itheima moduleAdd example

`example` 是新模块的名字

自动创建这些目录和文件
│   ├── module-example          | example模块主目录
│   │   ├── assets              | 资源
│   │   ├── components          | 组件
│   │   ├── pages               | 页面
│   │   │   └── index.vue       | 示例
│   │   ├── router              | 路由
│   │   │   └── index.js        | 示例
│   │   └── store               | 数据
│   │       └── app.js          | 示例
```

* 每个模块所有的素材、页面、组件、路由、数据，都是独立的，方便大型项目管理，
* 在实际项目中会有很多子业务项目，它们之间的关系是平行的、低耦合、互不依赖。

## 注册模块

* 编辑 `src/main.js`

```js
...
/*
* 注册 - 业务模块
*/
import dashboard from '@/module-dashboard/' // 面板
import example from '@/module-example/'     // 刚新添加的 example
Vue.use(dashboard, store)
Vue.use(example, store)
...
```

> 使用 `Vue.use` 方式注册
>
> 参数 `store` 表示注册状态管理
