### 微服务:将服务差分成一个一个个独立的功能

+ 每一个模块都是可以独立部署独立替换的
+ 学习资料：springcloudcc



### 心跳机制

+ 服务方给eureka发送rest请求说明我还活着

### RestTemplate（http请求）

### DiscoveryClient：所有的服务信息（每个注册到eureka的服务的信息）





## Eureka:

服务端

+ 引入启动器

+ 配置spring.application.name=xxxname

+ 引导类上添加 @EnableEurekaServer 

  

  客户端

+ 引入启动器

+ 配置spring.application.name=xxxname

+ eurake.client.server-url.defaultZone=http://localhost:10086/eureka

+ 引导类上添加 @EnableDiscoveryClient



idea快捷操作：

50.fori=

```
for (int i = 0; i < 50; i++) {
    
}
```





## Ribbon(负载均衡器)

+ rureka集成了ribbon
+ 再RestTemplate 上增加注解@loadBalanced 
+ 默认策略是轮巡



## hystrix 

+ 引入hystrix启动器

+ 设置超时时间

+ 在引导器中添加注解 @EnableCircuitBreaker

+ 定义熔断方法（局部：要和原方法参数一直  全局：返回类型要和熔断方法一致，参数列表为空）

+ ```
  局部 方法上面
  @HystrixCommand(fallbackMethod = "xxx")
  
  全局 类上面
  @DefaultProperties(defaultFallback = "getError2")
  ```

## feign

+ 引入feign启动器

+ 在引导类上添加 @EnableFeignClients

+ 创建一个接口 添加@FeignClient

+ ```
  记得开启：
  ribbon:
    eureka:
      enabled: true
  ```

