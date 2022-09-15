#MapReduce预习报告#

---
## MapReduce概述 ##
MapReduce是一种用于在大型商用硬件集群中（成千上万的结点）对海量数据（多个兆字节数据集）实施可靠的、高容错的分布式计算的框架，也是一种经典的并行计算模型。核心功能是将用户编写的业务逻辑代码和自带默认组件整合成一个完整的分布式运算程序，并发运行在一个Hadoop集群上。MapReduce模型适合于大文件的处理，对很多小文件的处理效率不是很高。

## MapReduce基本原理 ##
将一个复杂的问题（数据集）分成若干个简单的子问题（数据块）进行解决（Map函数）；然后对子问题的结果进行合并（Reduce函数），得到原有问题的解（结果）。
MapReduce思想核心：“分而治之”。
Map负责“分”，Mapper负责“分”，即把复杂的任务分解为若干个“简单的任务”来处理。“简单的任务”包含三层含义：一是数据或计算的规模相对原任务要大大缩小；二是就近计算原则，即任务会分配到存放着所需数据的节点上进行计算；三是这些小任务可以并行计算，彼此间几乎没有依赖关系。Reducer负责对map阶段的结果进行汇总。至于需要多少个Reducer，用户可以根据具体问题，通过在mapred-site.xml配置文件里设置参数mapred.reduce.tasks的值，缺省值为1。

## MapReduce做什么？##
Map函数：接受一个键值对，产生一组中间键值对。MapReduce框架会将map函数产生的中间键值对里键相同的值传递给一个reduce函数。
Reduce函数：接受一个键，以及相关的一组值，将这组值进行合并产生一组规模更小的值（通常只有一个或零个值）。

## MapReduce工作机制 ##
实体一：客户端，用来提交MapReduce作业。
实体二：JobTracker，用来协调作业的运行。
实体三：TaskTracker，用来处理作业划分后的任务。
实体四：HDFS，用来在其它实体间共享作业文件。
比喻：我们要数图书馆中的所有书。你数1号书架，我数2号书架。这就是“Map”。我们人越多，数书就更快。现在我们到一起，把所有人的统计数加在一起。这就是"Reduce”。

## MapReduce编程模型 ##
MapReduce编程模型主要由两个抽象类构成，即Mapper类和Reducer类。Mapper用以对切分过的原始数据进行处理，Reducer则对Mapper的结果进行汇总，得到最后的输出结果。根据其工作原理，可将MapReduce编程模型分为两类：MapReduce简单模型和MapReduce复杂模型。

## MapReduce数据流 ##
Mapper处理的是<key,value>形式的数据，即不能直接处理文件流。
1.分片、格式化数据源（InputFormat）
InputFormat主要有两个任务，一个是对源文件进行分片，并确定Mapper的数量；另一个是对各分片进行格式化，处理成<key,value>形式的数据流并传给Mapper。
2.Map过程
Mapper接收<key,value>形式的数据，并处理成<key,value>的数据，具体的处理过程可由用户定义。
3.Combiner过程
每一个map()都可能会产生大量的本地输出，Combiner()的作用就是对map()端的输出先做一次合并，以减少在Map和Reduce结点之间的数据传输量，提高网络I/O性能。
4.Shuffle过程
Shuffle过程是指从Mapper产生的直接输出结果，经过一系列的处理，成为最终的Reducer直接输入数据为止的整个过程，这一过程也是MapReduce的核心过程。
5.Reduce过程
Reducer接收<key,{value list}>形式的数据流，形成<key,value>形式的数据输出，输出数据直接写入HDFS，具体的处理过程可由用户定义。

## MapReduce框架的组成 ##
1.JobTracker
JobTracker负责调度构成一个作业的所有任务，这些任务分布在不同的TaskTracker上。你可以将其理解为公司的项目经理，项目经理接受项目需求，并划分具体的任务给下面的开发工程师.
2.TaskTracker
TaskTracker负责执行由JobTracker指派的任务，这里我们就可以将其理解为开发工程师，完成项目经理安排的开发任务即可。

