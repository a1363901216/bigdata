# bigdata

作者：Si Luvenia
链接：https://www.zhihu.com/question/19795366/answer/106364880
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

终于看到我能贡献一点力量的问题了，摩拳擦掌，不请自来，只是不知道还有没有人对这个问题感兴趣。 先自我介绍一下，Hadoop System Engineer & Hadoop Training Specialist，坐标美西，一直在招人和做training做得比较多，所以这题比较对口。
关于入门：
我比较赞同有位匿名同学的回答，如果看书一头雾水的话，先从实际例子出发会比较容易上手。WordCount和Weather Data这种“Hello World”的例子网上有很多，可以复制下来自己跑一遍，基本上就知道Hadoop是个什么东西，能用来干什么了。跑这些例子都不需要一个完整的Hadoop集群，自己本地的VM上就可以完成。
之所以我觉得这是比较好上手的方式，是因为我也认为Hadoop是一个工具，而不是一门学科。工具的一般用法是你有一个实际的问题需要解决（求和，求平均值之类的问题都可以，两三行数据，不需要“大数据”），然后把这个工具运用到你的问题里面，能够使用工具之后再开始研究怎么更好的更有效的使用这个工具。
入门会Google就行了！
关于进阶：
知道是什么，能干什么之后，需要知道为什么。这很重要，这关系到你的任务是跑三个小时还是要跑三天，是需要三台服务器还是需要三十台服务器，就直接关系到最后要花三十还是花三百。
进阶之前需要一点准备工作：Linux －（这对于所有Distributed System都非常重要），Java（能看得懂代码就可以了），Maven（能用就可以），Scala（optional，可以边学边用），SBT（optional，可以照着tutorial用），
进阶就需要看书（绝对不需要看源代码。。看得下去嘛那），前面有很多位同学推荐了各种书各种博客，都应该不错。唯一就是时间和版本问题，有些书和博客可能写得比较早，介绍的Hadoop和其他应用都是很早的版本，现在已经完全不对了。尤其是Hadoop1和Hadoop2，这个区别是很大的，有时候碰到来面试的同学侃侃而谈Hadoop1，忍不住扶额。
我只推荐两个
－ Hadoop The Definitive Guide最新版，这也是我当时的入门书，写的非常好。强烈强烈建议看英文版的，否则容易交流障碍。。。这本书的例子都在github上可以下载下来，都跑一跑。另外Hadoop相关职位的面试问题大部分都来自于这本书，这本书看两遍基本上面试没问题。这是唯一一本我觉得从头到尾必看的书。
－ Cloudera的tutorial，user guide，blog和best practice。这个比较官方和实效性。这不是说你要一页一页看完，是你有实际问题自己解决不了了来找参考资料。
The "Getting Started With Hadoop" tutorialThe "Getting Started With Hadoop" tutorialCloudera Engineering BlogCloudera Engineering BlogCloudera Engineering Blog－另外还有一个传说中的Google三篇论文，那是Distributed System 和Big Data的开山始祖。其实我没看懂。。有兴趣也可以翻一翻。
关于深入：
关于怎么深入学Hadoop，我看了前面很多答主的回答，觉得需要补充一点点。Hadoop分为两个大块：HDFS和MapReduce。
HDFS － Hadoop Distributed FileSystem。这个概念很好，但是其实我不觉得很实用。但是如果你之后要往Non SQL方面深入的话这个还是很重要，HDFS是HBASE的基础，Hbase又可以延伸到Big Table，DynamoDB，Mango等。HDFS概念不难，Hadoop The Definitive Guide里面讲的很清楚，看书就好。
MapReduce － 前面说最好看英文版，因为不管中文怎么翻译，Map，Reduce都是没办法像读英文那样容易理解的。这里面有个YARN的概念，是最最最重要的。MapReduce是管数据怎么流动的，YARN是管集群中的资源怎么分配的。除了YARN以外，MapReduce还有几个很重要的概念，比如Partition, combine, shuffle, sort, 都在书里很小的位置，但是都对理解整个MapReduce非常有帮助。
关于log：
我的日常，感觉每天看log都快要看到眼瞎。
如果你使用Hadoop，那么看log的时间估计会占了一大半。怎么看log，先从Resource Manager web UI开始入手吧。这是个web UI，可以让你查看每个任务的具体进展，container的运行等等。
关于其他应用：
再下一步就是Hadoop上其他的应用， Hive，Pig，Spark，Cassandra，Presto什么的，都很容易掌握。因为这些都是为了方便Data Scientist什么的更容易上手掌握Hadoop而编写的比较上层的应用，一两个小时就可以上手了，建议继续看Hadoop The Definitive Guide。
但是Spark要单独提出来讲一讲，Spark其实不是Hadoop上面的应用，它也可以使用除了YARN之外的其他资源分配系统。但是Spark使用的人很多，很多任务用Spark比用Hadoop MR要快一些，Spark也比其他的应用要复杂一点。如果有兴趣还是可以从Hadoop The Definitive Guide开始，然后边做实际的例子边学习。
关于Hadoop的使用方式：
感觉现在各个公司使用Hadoop的方式都不一样，主要我觉得有两种吧。
第一种是long running cluster形式，比如Yahoo，不要小看这个好像已经没什么存在感的公司，Yahoo可是Hadoop的元老之一。这种就是建立一个Data Center，然后有几个上千Node的Hadoop Cluster一直在运行。比较早期进入Big Data领域的公司一般都在使用或者使用过这种方式。
另一种是只使用MapReduce类型。毕竟现在是Cloud时代，比如AWS的Elastic MapReduce。这种是把数据存在别的更便宜的地方，比如s3，自己的data center， sql database等等，需要分析数据的时候开启一个Hadoop Cluster，Hive/Pig/Spark/Presto/Java分析完了就关掉。不用自己做Admin的工作，方便简洁。
所以个人如果要学Hadoop的话我也建议第二种，AWS有免费试用时间（但是EMR并不免费，所以不要建了几千个Node一个月后发现破产了。。），可以在这上面学习。最重要的是你可以尝试各种不同的配置对于任务的影响，比如不同的版本，不同的container size，memory大小等等，这对于学习Spark非常有帮助。
最后如果对hadoop学习有疑问，对相关职业有兴趣，或者身在北美干脆要跳槽的，非常欢迎来找我：）
PS，我的回答好像也超纲了。不过也许会有人想要知道这些。
