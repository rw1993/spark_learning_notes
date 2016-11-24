---
spark技术内幕读书笔记 第一章
---

### 1.3 spark架构

#### 主要构成

1. Driver:用户写的数据处逻辑（里面有sparkContext）
2. Cluster Manager:负责集群资源的管理和调度
3. Work node：可以执行计算任务的计算节点
4. Executor：work node上的进程。任务呗分被到work node上，然后再由该任务对应的executor计算。

#### 工作流程

1. 用户创建sparkContext实例，实例连接cluster manager，cluster manager根据该实例中的设置分配计算资源，启动executor
2. Driver将用户程序分成不同的执行阶段，没阶段由完全相同的task组成，处理划分出来的各个部分数据。划分完成和task创建后，Driver向executor发送task。
3. Executor接收到task后，下载task运行时的依赖，准备好环境之后，执行，并且向driver汇报task的运行状态。
4. Driver收到task的运行状态来处理不同的状态更新。task分为shuffle map task和result task，分别负责数据洗牌和得到结果。
5. Driver会不停地将task发送给Executor。

*我们可以注意到，driver最终负责任务的调度，而cluster manager负责的是更加宏观的分配计算资源。driver在得到这些计算资源（executors）后，不断向其发送任务，并不断监控它*

### 1.4 spark 核心组件概述

1. spark streaming:流式计算分解成一系列短小的批处理。
2. mlib：机器学习框架
3. spark sql:解决数据源问题(hbase?)
4. graphx:图

