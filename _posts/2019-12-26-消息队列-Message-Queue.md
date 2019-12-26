## 消息队列

In computer science, message queues and mailboxes are software-engineering components used for inter-process communication (IPC), or for inter-thread communication within the same process. They use a queue for messaging - the passing of control or of content. Group communication systems provide similar kinds of functionality.

The message queue paradigm is a sibling of the publisher/subscriber pattern, and is typically one part of a larger message-oriented middleware system. Most messaging systems support both the publisher/subscriber and message queue models in their API.

## 引入消息系统中间件的优势

#### 解耦

消费者不在依赖于生产者生产数据的方法（解耦前，消费者需要调用生产者的方法，获取数据）；

消费者和生产者只需关注消息队列中的数据。

#### 异步

将一个消息发给多人，

同步的做法是，一个一个地給他们打电话；

异步的做法是，将消息发送到群里，等待他们收消息。

#### 削峰

缓冲生产者产生的大量数据，从而减小给消费者带来的负担

## 消息系统中间件的应用场景

- 用户注册系统成功后的一系列操作，例如：发邮件、发私信等
- 实时流处理、离线分析和数据仓库作为信息的消费者
- 站内私信、通知
- 限时抢购活动
- 网站使用情况/活动流（页面访问量、被查看内容方面的信息和搜索情况）
- 系统运行情况/运营数据（日志信息、CPU和内存使用情况）

