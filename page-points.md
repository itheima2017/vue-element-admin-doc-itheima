# 新增权限点

## 添加权限点

## 授权权限点

## 检查权限点

* 第一步：导入 `hasPermissionPoint` 检查函数

```js
import { hasPermissionPoint } from '@/utils/permission'
```

* 第二步：检查操作

```js
let hasList = hasPermissionPoint('base-users-list')
console.log(hasList)
```

> `hasList` 将会以 `bool` 形式返回是否有权限点

?> 对于呈现类组件可以结合 `v-if` 指令来控制
