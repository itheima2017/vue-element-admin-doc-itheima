# 下载&运行

?> 本项目是前后端分离，需要先启动后端服务，然后再运行前端项目。

## 后端服务

* 下载项目

```bash
git clone https://github.com/itheima2017/vue-element-admin-api-java-itheima.git
```

* 新建数据库

  登录mysql，创建名为 vue_element_admin 的数据库

* 修改默认配置

```bash
#修改默认配置
vim ./vue-element-admin-api/src/main/resources/application.yml

#修改数据库配置
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/vue_element_admin?useUnicode=true&characterEncoding=utf8
    username: root   #数据库账号
    password: 123456 #数据库密码

#修改端口
server:
  port: 7999
```

* 初始化数据库

```bash
#进入数据库初始化文件目录
cd ./vue-element-admin-api/db

#运行初始化文件
mysql -uroot -p123456 -Dvue_element_admin < init.sql
```

> mysql -u账号 -p密码 -D数据库名称 < sql文件路径

* 打包及运行

```bash
#进入项目目录
cd vue-element-admin-api

#打包
mvn clean package

#运行
nohup ./vue-element-admin-api/target/vue-element-admin-api-1.0.0.jar
```

?> 启动后 `http://localhost:7999` 就是 `API` 地址了

## 前端项目

* 下载项目

```bash
# 克隆项目
git clone https://github.com/itheima2017/vue-element-admin-itheima.git

# 安装依赖
npm install
# 或者 用淘宝镜像加速
npm install --registry=https://registry.npm.taobao.org
```

?> 强烈建议不要用直接使用 cnpm 安装有各种诡异的 bug，可以通过重新指定 registry 来解决 npm 安装速度慢的问题

```bash
npm install --registry=https://registry.npm.taobao.org
```

* 修改 `API` 地址

编辑文件 `config/index.js`

```js
  ...
  proxyTable: {
    '/api': {
      target: 'http://localhost:7999',
      changeOrigin: true,
      pathRewrite: {
        '^/api': ''
      }
    }
  },
  ...
```

> 修改 `target` 的值为 `http://localhost:7999`

* 运行

```bash
# 本地开发 启动项目
npm run dev
```

打开浏览器访问 http://localhost:9527

![](https://wpimg.wallstcn.com/1bc334a6-32a8-4f29-a037-ac3f5ce32588.png)
