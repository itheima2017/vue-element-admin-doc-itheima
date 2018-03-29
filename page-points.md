# 页面权限点

## 添加权限点

## 授权权限点

## 检查权限点

直接上 `vue` 代码

```html
<template>
  <div class="dashboard-container">
    test
  </div>
</template>

<script>
import { hasPermissionPoint } from '@/utils/permission'

export default {
  name: 'dashboard',
  components: {},
  data() {
    return {
    }
  },
  computed: {
  },
  created() {
    // 权限点检查
    let hasList = hasPermissionPoint('base-users-list')
    console.log(hasList)
  }
}
</script>
```

* 第一步：导入

```js
import { hasPermissionPoint } from '@/utils/permission'
```

* 第二步：检查

```js
let hasList = hasPermissionPoint('base-users-list')
console.log(hasList)
```

?> 对于呈现类组件可以结合 `v-if` 指令来控制
