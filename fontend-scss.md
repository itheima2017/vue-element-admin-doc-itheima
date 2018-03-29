# scss 样式

## 安装依赖包

```bash
npm install sass-loader node-sass --save-dev
```

## 无需配置

* vue脚手架已经为我们在 `webpack` 中写好了
* 文件 `/build/utils.js`

```js
// https://vue-loader.vuejs.org/en/configurations/extract-css.html
return {
  css: generateLoaders(),
  postcss: generateLoaders(),
  less: generateLoaders('less'),
  sass: generateLoaders('sass', {indentedSyntax: true}),
  scss: generateLoaders('sass'),
  stylus: generateLoaders('stylus'),
  styl: generateLoaders('stylus')
}
```

## 使用

```html
<template>
...
</template>

<script>
...
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
@import "src/styles/mixin.scss";
.app-wrapper {
  @include clearfix;
  position: relative;
  height: 100%;
  width: 100%;
}
</style>
```
