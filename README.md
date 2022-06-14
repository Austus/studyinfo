# studyinfo
学习笔记项目


## 20220614学习amqp协议 总结：
amqp全称是advanced message queuing protocal  高级消息队列协议，应用层的开放标准，面向消息中间件的一个协议，该协议不受不同消费者生产者的不同产品，不同语言的限制，该协议的实现有rabbitmq。 

工作流程：生产者publisher --> 交换机exchange --> 路由键routeKey --> 队列queue --> 消费者consumer 




### 交换机exchange
 交换机有4种类型
 1. 直连模式 dirt：直连模式会直接把消息中的routingKey和队列绑定交换机的routingKey匹配，完全相等，则匹配成功，发送消息给所有匹配的队列。
 2. 扇形模式 fanout：扇形模式不会匹配routingKey，消息来了之后，会发送消息到所有绑定该交换机的队列。
 3. 主题模式 topic：主题模式在直接模式dict的基础上，加上了模糊匹配规则，“\*”匹配一个单词，“#”匹配多个或者0个单词(模糊匹配是放在队列绑定交换机的routingKey上的，发送消息指定的routingKey不支持模糊匹配)； 单词的意思是在消息的routingKey上通过.分割来计算单词数，例如A.B.C有3个单词分别是A,B，C； happy.wishPace.hope是3个单词分别是：happy,wishPace,hope。
 4. 头部模式 header：根据消息的头部信息去匹配（用的比较少）


### 队列queue
  1. 创建队列之后，需要绑定交换机才能接收到消息，绑定交换机需要指定交换机名称，和routingKey
  2. 队列持久化，未持久化的队列存在内存中，宕机之后无法恢复，持久化的队列才能恢复。rabbitMq可设置队列的Durability属性为Durable标识持久化，队列持久化会存储在磁盘中。

### 消息message
  1. 发送消息的时候，需要指定交换机exchange，路由键routingKey。
