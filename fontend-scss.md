# scss 样式

## 安装依赖包

```bash
npm install sass-loader node-sass --save-dev
```

## 无需配置 webpack

* 已经为我们写好了 `build/utils.js`

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
