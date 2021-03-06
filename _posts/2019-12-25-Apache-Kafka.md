## Apache kafka 

Jay Kreps chose to name the software after the author Franz Kafka because it is "a system optimized for writing", and he liked Kafka's work.[^1]

Apache kafka是一个开源分布式发布订阅消息系统，消息系统[参见](https://robindm.github.io/2019/12/26/%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97-Message-Queue.html)



### 架构图及其组件说明

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/Overview_of_Apache_Kafka.svg/1280px-Overview_of_Apache_Kafka.svg.png)

- Producer（生产者）：生产数据的
  - Producer和Broker之间采用Push的方式交换数据
- Consumer（消费者）：消费数据的
  - Consumer和Broker之间采用Pull的方式交换数据
- Consumer Group（消费组）：一至多个消费者，可以组成消费组
  - 消费组内成员只能有一人消费某个消息，即消息的单播
  - 不同消费组可以同时消费某个消息，及消息的多播
- Broker（中间商）：用于消息存储与分发
  - Kafka集群中的一台服务器节点
  - 每个Broker可以包含一至多个Topic
- Topic（主题）：也可以理解成消息通道，通道间的数据彼此隔离
  - 每个Topic包含一至多个Partition
- Partition（分区）：也可以理解成实际存储数据的目录



### Consumer消费Broker数据的方式

kafka采用Pull方式获取Broker的数据，也有些消息队列中间件采用Broker Push的方式向Consumer推送数据

- Pull方式使Consumer可以更加灵活地获取数据，避免了数据的拥塞
- Push方式则更注重数据消费的时效性



### Producer向Broker发送数据的策略

At most once：消息可能丢失，但不会重复传输

At least once：消息不会丢失，但可能重复传输

Exactly once：消息只传输一次，且不会丢失



## 问题与思考

- 问题一：消费组内的消费者，是均衡消费数据的吗？
  - 实验环境：一个生产者，一个kafka集群，一个包含两个消费者的消费组。
  - 实验过程：启动两个消费者进程，再执行生产者脚本。
  - 实验猜想：消费组中的消费者，均衡消费数据。
  - 实验结果：
    - 两个消费者进程中，只有一个能消费到数据；
    - 如果关闭了那个一直消费数据的消费者，另一个消费者才开始消费数据；
    - 重启那个已关闭的消费者进程，又开始消费数据，而另一个消费者将不会消费到数据。
  - 实验结论：消费者中的消费者，并没有均衡消费数据，而是采用了其他消费数据的机制！
  - 疑问：消费组中消费者，其消费数据的机制是什么？
    - 经查，消费组内有一种rebalance机制，作用是使组内消费者达成一致来分配订阅topic的每个分区。
- 问题二：rebalance机制的组内消费策略？
  - partition被均匀分配给消费组内成员，每个成员只能消费其分区内的消息
  - partition会随组内成员的动态变化而重新均匀分配
- 问题三：消费者api可以指定订阅的topic分区，如果同一消费组内的消费者订阅相同topic的分区，消息会在组内均衡消费吗？


## 引用

[^1]: 维基百科

