### springboot 日志（lf4j+logback）

+ 设置springBoot日志等级 在配置文件中  

  + ```xml
    logging.level.com.example.demo.DemoApplicationTests==debug   包+类
    ```

+ springboot 只会输出 当前设置的日志等级之上的日志信息





### springboot JDBC操作

```
1、配置文件配置数据库连接信息
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springbootdata?characterEncoding=utf-8
spring.datasource.username=root
spring.datasource.password=
2、创建DataSource对象 调用getConnection方法
#切换连接池
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource  


3、通过配置类（@Configuration）
@ConfigurationProperties(prefix = "spring.datasource")//加载配置文件
@Bean
的方法配置如druid的特殊属性

```

### 多用包装类 包装类解决了值初始化的问题

## SpringBoot 的页面逻辑

```
pojo包 对象
mapper 放浏览的页面url
controller 放控制类
config 放配置类

在主调用函数被@SpringBootApplication修饰的
配置mapper的加载包 @MapperScan(basePackages = {"com.example.jdbcstudy.mapper"})
```

## springboot 与拦截器 以及三大组件（过滤器，servlet，监听器）

```
拦截器 
创建拦截器对象 实现HandlerInterceptor接口
创建配置类 实现WebMvcConfigurer类  添加拦截器
@Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new MyInterceptor()).addPathPatterns("/get/*");
    }
```

```
servlet
servlet实现HttpServlet  
在配置类中
 //注册servlet
    @Bean
    public ServletRegistrationBean servletRegistrationBean(){
        ServletRegistrationBean bean = new ServletRegistrationBean(new MyServlet(),"/servlet1","/servlet2");
        return bean;
    }
```

```
过滤器
//注册过滤器
    @Bean
    public FilterRegistrationBean filterRegistrationBean(){
        FilterRegistrationBean bean =new FilterRegistrationBean();
        bean.setFilter(new MyFilter());
        bean.addUrlPatterns("/servlet1");
        return bean;
    }
```

```
监听器
  @Bean
    public ServletListenerRegistrationBean listenerRegistrationBean(){
        ServletListenerRegistrationBean bean = new ServletListenerRegistrationBean();
        bean.setListener(new MyListener());
        return bean;
    }
```

