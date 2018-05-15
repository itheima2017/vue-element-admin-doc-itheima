# SpringBoot2 说明

本项目中使用了SpringBoot2，这个版本做了很多的变更。

##### 主要的变更

- 基于Java8,支持Java9

  SpringBoot2完全基于Java8,对Java9做了一些支持。

- 引入Webflux

  它是一个新的响应式的Reactive Web框架，可以用来建立异步、非阻塞，以事件驱动的服务，并且扩展性很好，性能比之SpringMVC方式有了一定的提高。

- 默认引入HikariCP

  用于替代之前的tomcat-pool作为底层数据库连接池，相比tomcat-pool，HikariCP有更好的性能，能够有效的提高db的访问速度。

- 为各种组件的响应式编程提供了自动配置，如Reactive Spring Data、Reactive Spring Security等

##### 依赖组件的升级

- Tomcat升级至 8.5
- Flyway升级至 5
- Hibernate升级至 5.2
- Thymeleaf升级至 3

##### 配置重定位

在一些配置上，SpringBoot2进行了修改，例如一些servlet相关的server.*属性重定位到了server.servlet前缀下：

| Old property                   | New property                           |
| ------------------------------ | -------------------------------------- |
| `server.context-parameters.*`  | `server.servlet.context-parameters.*`  |
| `server.context-path`          | `server.servlet.context-path`          |
| `server.jsp.class-name`        | `server.servlet.jsp.class-name`        |
| `server.jsp.init-parameters.*` | `server.servlet.jsp.init-parameters.*` |
| `server.jsp.registered`        | `server.servlet.jsp.registered`        |
| `server.servlet-path`          | `server.servlet.path`                  |

更多的变化、配置重定位等，请查阅官方升级手册：https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Migration-Guide

##### 总结

实际上，升级或使用SpringBoot2不会像想象中的那样高风险，虽然它推出了很多的功能，但是对于原有功能的支持并没有抛弃。因此，在我们不使用Webflux的基础上，我们仅仅只需做一些依赖和配置上的调整就能继续将应用正常的运行起来。