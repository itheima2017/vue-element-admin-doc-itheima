# JPA 配置

在黑马Admin中，我们使用了SpringDataJPA来完成数据访问层的实现。而SpringBoot2中的JPA的配置与SpringBoot1有所区别。

```yaml
#SpringBoot1配置方式
spring :
  datasource : 
    driverClassName : com.mysql.jdbc.Driver
    url : jdbc:mysql://ip:port/database?useUnicode=true&characterEncoding=utf8
    username : root
    password : 123456
  jpa :
    database : MySQL
    show-sql : true
    generate-ddl : true
    hibernate :
      ddl-auto : update
      naming :
        physical-strategy : org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy
    open-in-view : true

#SpringBoot2配置方式
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://ip:port/database?useUnicode=true&characterEncoding=utf8
    username: root
    password: 123456
  jpa:
    database: MySQL
    show-sql: true
    generate-ddl: true
    hibernate:
      ddl-auto: update
      naming:
        physical-strategy: org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy
    open-in-view: true
    database-platform: org.hibernate.dialect.MySQL5InnoDBDialect
```

从上述代码中，可以看到两个版本中，关于JPA的配置基本一致，少数的一些地方有所区别。因此，在使用新版本时，遇到不支持的配置项或api，尽量到官网阅读新版本的文档，以便找到替换的方法或者不支持的原因，才能对项目进行正确的调整。