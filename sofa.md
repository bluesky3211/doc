## 1. SOFA基本介绍
### 1.1 概念
SOFARPC是蚂蚁金服开源的一种高可扩展性、高性能、生产级的Java RPC服务框架，为应用之间提供远程服务调用能力。
### 1.2 功能特性
-   透明化、高性能的远程服务调用
-   支持多种服务路由及负载均衡策略
-   支持多种注册中心的集成
-   支持多种协议，包括 Bolt、Rest、Dubbo 等
-   支持同步、单向、回调、泛化等多种调用方式
-   支持集群容错、服务预热、自动故障隔离
-   强大的扩展功能，可以按需扩展各个功能组件
### 1.3 实现原理
![image.png |  ç¦»å¼€|  748x404](https://gw.alipayobjects.com/zos/nemopainter_prod/46b1967d-0c27-4e00-ae63-dbdf315516a8/sofastack-sofa-rpc-zh_CN/resources-home_1.png)
1. SOFARPC服务端启动时，会注册服务到注册中心
2. 当引用服务的客户端启动时，会向注册中心发起订阅
3. 注册中心返回订阅到的服务的元信息
4. 客户端拿到服务调用地址后，调用服务
### 1.4 架构
SOFARPC从下到上分为两层：

1.  核心层：包含了我们的RPC的核心组件（例如我们的各种接口，API，公共包）以及一些通用的实现（例如随机等负载均衡算法）。
2.  功能实现层：所有的功能实现层的用户都是平等的，都是基于扩展机制实现的。

![æž¶æž„å›¾](https://gw.alipayobjects.com/zos/nemopainter_prod/157f9b93-8b09-40a2-b1b9-9a255fdb06a4/sofastack-sofa-rpc-zh_CN/resources-dg_1.png)

### 1.5 主要模块
各个模块的实现类都只在自己模块中出现，一般不交叉依赖。需要交叉依赖的全部已经抽象到核心或者共同的模块中。目前模块划分如下：

![æ¨¡å—åˆ’åˆ†](https://gw.alipayobjects.com/zos/nemopainter_prod/704888fb-63a0-4fe8-b1fa-04af11a4cfb3/sofastack-sofa-rpc-zh_CN/resources-dg_2.png)

主要模块及其依赖如下（基于5.5.0）：
| 模块名 | 子模块名 | 中文名 |  说明 | 依赖 |
|--|--|--|--|--|
| 所有 | all | 发布打包模块 |  | 需要打包的全部模块 |
| BOM | bom | 依赖管控模块 | 依赖版本管控	| 无 |
| 案例 | example |示例模块 | 	| 所有 |
| 核心 | api | api模块 | 各种基本流程接口、消息、上下文、扩展接口等| 共同 |



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NTM2NDgxMzBdfQ==
-->