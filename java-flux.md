# Webflux响应式编程

响应式编程是一种基于数据流和变化传递的声明式的编程范式。用一个形象的例子来形容响应式编程，你会发现Excel简直就是一个响应式的典范。当你在某个单元格中使用了公式，其单元格中的值，假设是a1,a2,a3的汇总，那么这时候，只要a1，a2，a3中任意项的值被修改了，就会直接体现到这个汇总的单元格中。这个过程充分体现了变化传递，每一次的修改可以视为数据流，而设定的好的公式则是它的声明，这恰恰贴合了关于响应式编程的描述。

Spring Webflux是随着Spring5推出的响应式Web框架。它以Reactor 库为基础，开发人员可以使用 WebFlux 创建高性能的 Web 应用和客户端。这个模块当中，包含了对响应式Http、服务器推送事件和 WebSocket 的客户端和服务器端的支持。对于后端开发来说，比较重要的就是服务器端的开发。在服务器端，Webflux在同样的响应式底层架构之上，提供了两种不同的代码编写方式，一种是在Spring MVC中使用注解的方式，另一种是基于lambda表达式的函数式编程模型。Webflux程序运行时，是需要容器支持的，它可以运行在支持非阻塞IO API的Servlet容器上，或者是其他异步运行时环境，如Netty等。

这里我们简单介绍一下如何运用注解的方式进行开发。

```java
@RestController
public class HelloController {
    @RequestMapping(value = "/hello")
    public Mono<String> hello(){
        return Mono.just("hello itheima");
    }
    @RequestMapping(value = "/hellos")
    public Flux<String> hellos(){
        List<String> hellos=new ArrayList<>();
        hellos.add("hello itheima1");
        hellos.add("hello itheima2");
        return Flux.fromIterable(hellos);
    }
}
```

从上面的代码中，我们不难看出使用Webflux与Spring MVC的不同在于，在于使用了与响应式编程相关的Flux和Mono等，而不是简单的对象。在简单的示例程序中，两者之间并没有太大的区别。而对于复杂的应用，响应式编程和抗压能力将会给整个应用带来性能的提升。而Webflux模块提供的另外一种开发模式以及服务器推送实践和WebSocket并未在项目中使用，因此在这里暂时不进行讨论，如对此感兴趣，可以查阅相关文档[《Webflux框架》](https://docs.spring.io/spring-framework/docs/5.0.0.BUILD-SNAPSHOT/spring-framework-reference/html/web-reactive.html)。

通过少量的代码修改，我们即可运用Webflux来提升我们应用的性能。由于Spring框架的流行，WebFlux 会成为开发 Web 应用的重要趋势之一，为我们开发高性能 Web 应用带来了新的机会和挑战。