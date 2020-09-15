# Spring Boot 2.0

## Spring Boot 三个特性

1. 组件的自动装配：web mvc， web flux
2. 嵌入 web 容器：tomcat、jetty、undertow
3. 生产准备特性：指标、健康检查、外部化配置

start.spring.io 初始化工程



### 组件自动装配

1. 激活：@EnableAutoConfiguration
2. 配置：/META_INF/spring.factories （相对 classpath 的目录）
3. 实现：xxxAutoConfiguration，@SpringBootApplication 包含 @EnableAutoConfiguration



### 嵌入式 web 容器

1. web servlet：tomcat、jetty、underrow
2. web reactive：netty、web server



### 生产准备特性

1. 指标：/actuator/metrics
2. 健康检查：/actuator/health
3. 外部化配置：/actuator/configprops



# Web 应用



## 传统 Servlet 应用

- Servlet 组件：Servlet、Filter、Listener（事件监听者模式）
- Servlet 注册：Servlet 注解、Spring Bean、RegistrationBean
- 异步非阻塞：异步 Servlet（Servlet 3.0）、非阻塞 Servlet（Servlet 3.1）



### Servlet 组件

- Servlet
  - 实现
    1. `@WebServlet`
    2. HttpServlet
    3. 注册
  - URL 映射
    - `@WebServlet(urlPatterns = "/my/servlet")`
  - 注册
    - `@ServletComponentScan(basePackages = "com.demo.test.web.servlet")`
- Filter
- Listener



### Servlet 注册

- `@ServletComponentScan`
  - `@WebServlet`
  - `@WebFilter`
  - `@WebListener`



### 异步非阻塞

```java
@WebServlet(urlPatterns = "/my/servlet", asyncSupported = true)

AsyncContext asyncContext = req.startAsync();
asyncContext.start(()->{
    try {
        resp.getWriter().println("hello world");
        // 触发完成
        asyncContext.complete();
    } catch (IOException e) {
        e.printStackTrace();
    }
});
```



## Spring Web MVC 应用



### Web MVC 视图

- ViewResolver
- View



#### 模板引擎

- Thymeleaf
- Freemarker
- JSP



#### 内容协商

- ContentNegotiationConfigurer
- ContentNegotiationStrategy
- ContentNegotiatingViewResolver



#### 异常处理

- `@ExceptionHandler`
- HandlerExceptionResolver
  - ExceptionHandlerExceptionResolver
- BasicErrorController(String boot)



### Web MVC REST



#### 资源服务

- `@RequestMapping`
  - `@GetMapping`
- `@ResponseBody`
- `@RequestBody`



#### 资源跨域

- CrossOrigin
- WebMvcConfigure#addCoreMappings



#### 服务发现

- HATEOS



#### Web MVC 核心

