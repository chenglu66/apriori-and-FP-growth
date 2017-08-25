# apriori
关联性分析
关联分析怎么讲就是在众多数据中找到相关性，我们前面知道要是可以量化的可以用方差，相关系数，但假如不是一些数字而是一些汉字，那怎么处理。
假想物品A和物品B那么AB同时出现的次数除以A出现的次数是不是就是A和B到底有多少相关，但是如果用次数会不会对其他人不公平。感觉应该不太会。不过有个问题如果一个物品在所有集合中出现的次数较少数据还真实吗？所以最好能用频率的方式。这样就能筛选出来支持度高的数据。
这样我需要统计每个项的频数毫无疑问非常复杂，有没有什么好办法解决。可以想象如果某个项是频繁那么他的子集也一定是频繁的。虽然这样说可能没什么用但是如果倒着说，假如某个项是不频繁的那么他的母集也一定不是频繁的。比如我计算出了{2,3}的支持度发现不是频繁，那么{1,2,3}也不是频繁项，这样就省去了很多计算，下面就是怎么发现项少的。我先找单个元素计算支持度，支持度小的直接pass，这样就直接pass那些不太行的集合。想法很好算法怎么实现：
首先找出所有的单项，然后计算下每个项的概率，小于某个阀值直接pass。
下面怎么办把有用的合并把看看那个得到了要求，怎么合并就是并集|，那么得有相同项才能合并把，就是比较两项的前面的相等就合并吧，那么就要排序。
好吧也不难，找到这些之后在计算频繁项把不符合要求的都过滤了。（这个合并还是蛮关键的）
找到频繁项了就是生成规则了。（11:30，看完休息）
下面就是生成规则了，
要是元素个数小于=1就直接忽略，要是两个直接算，要是再多就需要比较详细了。因为生成的规则比较多，比如3个3队2，3对1都是规则。先是右边只包含一个元素，知道包含需要的。这个过程比较需要技巧。因为我需要递归，就是递归中把不符合去掉，当然小集合不满足那么他的其它母集合也不会满足。所以生成规则也好弄了。就是一个个组合。
现在看一个实例：
发现国会的投票模式
首先问题定义：要想找到投票的模式，那么我下次提案时就有更大几率通过。那么我要知道议案的名字，和是否通过。但是政党不同关注点也会不同，所以收集数据时要分政党来收集。所以统计时要收集到这个数据，然后直把可信度低的去掉。最后在生成规则，看下那些议案更容易被通过，就是议题和通过之间的关联性。
第二个实例是发现毒蘑菇的相似特征，特征有一推，那些特征和毒蘑菇比较相关，还是关联分析。
所以关联分析的算法不难，定义也不难，难就难在算法实现上，要仔细思考。
假设我要把apriori用在工业上就是特征和结果的相关性也就是那些特征的出现会影响导致某个结果。就是那些变量的组合起来能推到需要的特征，这就时关联性分析。他可以处理多个变量之间的关系。他适合那种定性的比如有或者没有，是或否。
再来分析一下过程，假使我加工时有很多数据，这些数据和加工效果好坏同时出现，那么我可以发现到底哪些变量对加工效果影响比较大，这就是关联分析，当然LR也可以得到需要的，不过在此之前最好做下关联分析。
比如我处在电解加工行业，加工条件有很多我怎么确定哪些加工条件对加工效果有影响，或者加工效果的评价标准有很多个，这时候关联性分析比较好了。
FP-growth算法来提高发现频繁项集
在apriori中发现频繁项得做法有点复杂，据说FP算法可以在遍历两次数据库的时候。（10：49）
FP树的思想：FP树会存储相集的出现频率，每个相集会以路径的方式储存在树中，存在相似的元素的集合会共享树的一部分。只有当集合之间完全不同时，树才会分叉。相似项之间的链接即节点链接（node link），用于快速发现相似项的位置。
FP-growth算法的工作流程如下：首先构建FP树，然后利用它来挖掘频繁项集。为构建FP树，需要对原始数据集扫描两遍，第一遍对所有元素项的出现次数进行计数。
并统计频率，第二遍只考虑频繁项集。
如何构建：
遍历数据集去掉不满足支持度的项集，在构建时读入每个相集.
大致了解其过程，我们看看代码怎么写。







