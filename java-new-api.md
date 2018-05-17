# 新增 SpringBoot2 Rest Api

在黑马 Admin 中，新增一个 Rest Api 是非常方便的。通常我们会在 controller 包，创建一个名为\*Controller.java 的类文件，然后在该类当中定义所需添加的 rest api。具体步骤如下：

* 第一步，在 itcast.research.controller 包下，创建名为 HelloController 的 Java 类。

  ```bash
  -itcast
  	-research
  		-controller
  			-HelloController.java
  ```

* 第二步，打开 HelloController，开始编写相关代码。

  ```java
  package itcast.research.controller;

  import org.springframework.web.bind.annotation.RestController;

  @RestController
  public class HelloController {
  }
  ```

  在 HelloController 类头添加 @RestController 注解，将该控制器声明为 rest 控制器，该控制器中定义的 api 将以 json 方式返回信息。

* 第三步，定义一个 api,例如/hello。

  ```java
  package itcast.research.controller;

  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RestController;

  @RestController
  public class HelloController {
      @RequestMapping(value = "/hello")
      public String hello(){
          return "hello itheima";
      }
  }
  ```

  添加名为 hello 的方法，并在方法上定义请求的链接"/hello"，即 api 访问地址。

* 第四步，验证。

  为方便验证，我们暂时先将身份认证关闭，即接口访问时，无需验证身份。

  ```java
  //修改 itcast.research.config.WebSecurityConfig，并注释如下代码
  .anyRequest().authenticated()
  //注释后
  //.anyRequest().authenticated()
  ```

  运行项目，并使用 Postman 或者类似工具，对新建的接口进行访问。

  ```bash
  #这里使用 curl
  [root@ss]# curl http://localhost:7999/hello
  #返回信息
  hello itheima
  ```

  至此，我们已经完成了新增简单的 rest api 操作，更多的内容，请结合具体的业务，对数据操作层(Dao)以及服务层(Service)进行扩展。
