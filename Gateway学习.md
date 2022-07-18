# Gateway学习

## 学习背景

接触到工作项目后，第一个上手的任务是网关流量的配置，需要做到

- 对网关整体流量的限制

- 对个人流量的限制

## 限流算法

### 计数器算法

![](https://img-blog.csdnimg.cn/20210520112004377.png)

假定 **X min** 内限制请求数量为 **Y** ，一个请求则计数器`counter+1`。当`counter`大于 **Y** 且还在当前的 **X min** 内，触发限流；**X min** 过后，`counter`重新计数。



计数器算法存在临界问题。

### 漏桶算法（Leaky Bucket）

![](https://img-blog.csdnimg.cn/20210521094438143.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM3NTQzNjI3,size_16,color_FFFFFF,t_70)

桶的上面是个水龙头，请求从水龙头流到桶中，水龙头流出的水速不定，有时快有时慢。忽快忽慢的流量叫做 **Bursty flow**。如果桶中水满，多余的水就会溢出，即请求被丢弃。从桶底部漏出的水速是固定的，因此漏桶算法可以平滑请求的速率。

对于漏桶算法，桶的容量不变，流出的速率不变，其底层结构是个队列（如下图所示）。当请求到来时，不是直接处理，而是放入队列中，另一个线程以固定的速率从队列读取请求，从而达到限流的目的。

![](https://img-blog.csdnimg.cn/20210521094827385.png)

基于漏桶算法的特点，该算法主要用途是保护服务，无法处理突发流量，而流出速率缓慢，可能造成服务资源的浪费。

### 令牌桶算法（Token Bucket）

![](https://img-blog.csdnimg.cn/20210521103943677.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM3NTQzNjI3,size_16,color_FFFFFF,t_70)

令牌桶算法是应用最广泛的限流算法，主要有两部分组成：生产令牌、消费令牌。

- 生产令牌：系统以持续的速率向桶中装入令牌

- 消费令牌：当请求到来时，需要消耗一个令牌。当令牌为空时则拒绝新的请求

### 总结

令牌桶限制的是平均流入速率。与漏桶算法相比，令牌桶支持一定程度的并发情况。

使用计数器进行限流，主要限制总并发数，比如数据库连接池大小、线程池大小、秒杀并发数都是计数器的用法。只要全局总请求数或者一定时间段的总请求数达到设定的阈值，则进行限流。这种方式是简单粗暴的总数量限流，而不是平均速率限流。
