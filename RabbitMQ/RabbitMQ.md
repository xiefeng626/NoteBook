## RabbitMQ工作模式

### 简单模式

```
一对一发送接收，
只需要绑定队列
```



### work模式

```
提高任务处理速度（竞争的消费者模式）
生产者产生许多消息 
多个消费者在工作队列中争抢消息
只需要绑定队列
```

### 订阅模式

### 广播模式

```
fanout
一个消息可以被多个消费者消费调

绑定交换机和队列 （spring配置文件里得绑定好）（可以是一个交换机多个队列）
```

### 路由工作模式

```
direct
交换机 routeingkey 队列 三个绑定  
把消息经过routeingkey经过删选后传给相应的队列
```

### 通配符模式

```
Topic
用*（一个单词） 或者# （多个单词） 来匹配路由
交换机 路由 队列 三者绑定
```

