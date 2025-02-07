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

熔断出问题：以后解决





## Zuul 网关

```
路由：分发给不同的微服务
负载均衡：同一个微服务的不同实例
```

+ 四种不同的路由方式

![](..\NoteSource\Image\Snipaste_2021-01-13_17-36-00.png)

+ 路由过滤

![](..\NoteSource\Image\Snipaste_2021-01-13_17-53-33.png)

+ 自定义过滤器

  继承 ZuulFilter 实现四个方法 

```

1.引入启动器
2.覆盖默认配置
3.在引导类上启用组件

1.高可用 itcast-eureka
10086 10087

2.心跳过期 itcast-service-provider
eureka：
	instance:
		lease-renewal-interval-in-seconds: 5 # 心跳时间
		lease-expiration-duration-in-seconds: 15 # 过期时间

3.拉取服务的间隔时间 itcast-service-consumer
eureka:
  client:
    registry-fetch-interval-seconds: 5

4.关闭自我保护，定期清除无效连接
eureka:
  server:
    eviction-interval-timer-in-ms: 5000 
    enable-self-preservation: false

ribbon: 负载均衡组件
	1.eureka集成了
	2.@LoadBalanced：开启负载均衡
	3.this.restTemplate.getForObject("http://service-provider/user/" + id, User.class);
	
hystrix：容错组件
	降级：检查每次请求，是否请求超时，或者连接池已满
		1.引入hystrix启动器
		2.熔断时间，默认1s， 6s
		3.在引导类上添加了一个注解：@EnableCircuitBreaker  @SpringCloudApplication
		4.定义熔断方法：局部（要和被熔断的方法返回值和参数列表一致）  全局（返回值类型要被熔断的方法一致，参数列表必须为空）
		5.@HystrixCommand(fallbackMethod="局部熔断方法名")：声明被熔断的方法
		6.@DefaultProperties(defaultFallback="全局熔断方法名")
	熔断：不再发送请求
		1.close：闭合状态，所有请求正常方法
		2.open：打开状态，所有请求都无法访问。如果在一定时间内容，失败的比例不小于50%或者次数不少于20次
		3.half open：半开状态，打开状态默认5s休眠期，在休眠期所有请求无法正常访问。过了休眠期会进入半开状态，放部分请求通过
		
feign
	1.引入openFeign启动器
	2.feign.hystrix.enable=true,开启feign的熔断功能
	3.在引导类上 @EnableFeignClients
	4.创建一个接口，在接口添加@FeignClient(value="服务id", fallback=实现类.class)
	5.在接口中定义一些方法，这些方法的书写方式跟之前controller类似
	6.创建了一个熔断类，实现feign接口，实现对应的方法，这些实现方法就是熔断方法
	
zuul
	1.引入zuul的启动器
	2.配置：
		zuul.routes.<路由名称>.path=/service-provider/**
		zuul.routes.<路由名称>.url=http://localhost:8082
		
		zuul.routes.<路由名称>.path=/service-provider/**
		zuul.routes.<路由名称>.serviceId=service-provider
		
		zuul.routes.服务名=/service-provider/**   *******************
		
		不用配置，默认就是服务id开头路径
		
	3.@EnableZuulProxy
	
	过滤器：
		创建一个类继承ZuulFilter基类
		重写四个方法
			filterType：pre route post error
			filterOrder：返回值越小优先级越高
			shouldFilter：是否执行run方法。true执行
			run：具体的拦截逻辑
	
	
	
	
	
	
	
	
	
	
	
```

## 总结

+  [springCloud.pdf](..\NoteSource\pdf\springCloud.pdf) 

