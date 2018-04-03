# 图标

在 [iconfont.cn](http://iconfont.cn/) 上选择并生成自己的业务图标库，再进行使用。

## 生成图标库代码

首先，搜索并找到你需要的图标，将它采集到你的购物车里，在购物车里，你可以将选中的图标添加到项目中（没有的话，新建一个），后续生成的资源/代码都是以项目为维度的。

下载完成之后将下载好的 .svg 文件放入 `@/icons/svg` 文件夹下之后就会自动导入。

* 使用方式

```js
<svg-icon icon-class="password" /> //icon-class 为 icon 的名字
```

## 改变颜色

`svg-icon` 默认会读取其父级的 color `fill: currentColor;`

你可以改变父级的`color`或者直接改变`fill`的颜色即可。
