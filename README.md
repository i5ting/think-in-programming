think-in-programming
====================


## ddd


### CQRS

- http://martinfowler.com/bliki/CQRS.html
- http://www.tuicool.com/articles/7BVjie（中文）

命令查询的责任分离Command Query Responsibility Segregation (简称CQRS)模式是一种架构体系模式，能够使改变模型的状态的命令和模型状态的查询实现分离。这属于DDD应用领域的一个模式，主要解决DDD在数据库报表输出上处理方式。

http://www.jdon.com/37891



http://www.infoq.com/interviews/greg-young-ddd



## NoSQL

CAP原理和BASE思想

### 分布式领域CAP理论，
Consistency(一致性), 数据一致更新，所有数据变动都是同步的
Availability(可用性), 好的响应性能
Partition tolerance(分区容错性) 可靠性

定理：任何分布式系统只可同时满足二点，没法三者兼顾。
忠告：架构师不要将精力浪费在如何设计能满足三者的完美分布式系统，而是应该进行取舍。

关系数据库的ACID模型拥有 高一致性 + 可用性 很难进行分区：
Atomicity原子性：一个事务中所有操作都必须全部完成，要么全部不完成。
Consistency一致性. 在事务开始或结束时，数据库应该在一致状态。
Isolation隔离层. 事务将假定只有它自己在操作数据库，彼此不知晓。
Durability. 一旦事务完成，就不能返回。
跨数据库事务：2PC (two-phase commit)， 2PC is the anti-scalability pattern (Pat Helland) 是反可伸缩模式的，JavaEE中的JTA事务可以支持2PC。因为2PC是反模式，尽量不要使用2PC，使用BASE来回避。

### BASE思想

BASE模型反ACID模型，完全不同ACID模型，牺牲高一致性，获得可用性或可靠性：
Basically Available基本可用。支持分区失败(e.g. sharding碎片划分数据库)
Soft state软状态 状态可以有一段时间不同步，异步。
Eventually consistent最终一致，最终数据是一致的就可以了，而不是时时高一致。

BASE思想的主要实现有
1.按功能划分数据库
2.sharding碎片 

BASE思想主要强调基本的可用性，如果你需要High 可用性，也就是纯粹的高性能，那么就要以一致性或容错性为牺牲，BASE思想的方案在性能上还是有潜力可挖的。

现在NoSQL运动丰富了拓展了BASE思想，可按照具体情况定制特别方案，比如忽视一致性，获得高可用性等等，NOSQL应该有下面两个流派：
1. Key-Value存储，如Amaze Dynamo等，可根据CAP三原则灵活选择不同倾向的数据库产品。
2. 领域模型 + 分布式缓存 + 存储 （Qi4j和NoSQL运动），可根据CAP三原则结合自己项目定制灵活的分布式方案，难度高。

这两者共同点：都是关系数据库SQL以外的可选方案，逻辑随着数据分布，任何模型都可以自己持久化，将数据处理和数据存储分离，将读和写分离，存储可以是异步或同步，取决于对一致性的要求程度。

不同点：NOSQL之类的Key-Value存储产品是和关系数据库头碰头的产品BOX，可以适合非Java如PHP RUBY等领域，是一种可以拿来就用的产品，而领域模型 + 分布式缓存 + 存储是一种复杂的架构解决方案，不是产品，但这种方式更灵活，更应该是架构师必须掌握的

## 先写spec

https://github.com/haml/haml-spec

然后测试

然后coding

举个例子mcollina的msgpack5



https://github.com/mcollina/msgpack5