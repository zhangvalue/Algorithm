# Algorithm
图论中最小生成树中的prim和kruskal介绍实现以及多源最短路径算法—Floyd算法
# 最小生成树(Prim算法和Kruskal算法)
## 最小生成树定义：
**在数据结构与算法的图论中，(生成)最小生成树算法是一种常用并且和生活贴切比较近的一种算法。
一个有 n 个结点的连通图的生成树是原图的极小连通子图，且包含原图中的所有 n 个结点，并且有保持图连通的最少的边。 最小生成树可以用kruskal（克鲁斯卡尔）算法或prim（普里姆）算法求出。**

**通俗易懂的讲就是最小生成树包含原图的所有节点而只用最少的边和最小的权值距离。因为n个节点最少需要n-1个边联通，而距离就需要采取某种策略选择恰当的边。
从定义上分析，最小生成树其实是一种可以看作是树的结构。而最小生成树的结构来源于图(尤其是有环情况)。通过这个图我们使用某种算法形成最小生成树的算法就可以叫做最小生成树算法。具体实现上有两种实现方法、策略分别为kruskal算法和prim算法**
## 城市道路规划实际问题：
各个城市没有高速公路(铁路)。
政府打算各个城市铺设公路(铁路)，每个城市都想成为交通枢纽，快速到达其他城市！但是这种情况下国家集体资源跟不上、造价太昂贵。并且造成巨大浪费！
最终国家选择一些主要城市进行联通，有个别城市只能稍微绕道而行，而绕道太远的、人流量多的国家考虑新建公路(铁路)。适当提高效率。![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126160956482.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
我们要从有环图中选取代价和最小的路线一方面代价最小(总距离最小最省黄金)另一方面联通所有城市。
然而根据上图我们可以得到以下最小生成树：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126161045842.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
唯物辩证法认为：

问题的主要矛盾对问题起着决定性作用。主要矛盾次要矛盾相互影响，相互渗透，一定程度可以相互转化。故我们看问题要抓关键、找核心。
在公路时代城市联通的主要矛盾是时间慢，而造价相比运输时间是次要矛盾。所以在公路时代我们尽量使得城市能够直接联通，缩短城市联系时间。而稍微考虑建路成本！随着科技发展、信息传输相比公路运输很快，从而事件的主要矛盾从运输时间转变为造价成本。所以我们会关注联通所有点的路程(最短)。这就用到最小生成树算法。
而类似的还有局部区域岛屿联通修桥，海底通道这些高成本的都多多少少会运用。
## Kruskal算法：
上面介绍了最小生成树是什么，但是我们需要掌握和理解最小生成树如何形成。给你一个图，生成一个最小生成树，当然需要一定规则。而在实现最小生成树方面有prim和kruskal算法，这两种算法的策略有所区别，但是时间复杂度一致。
而针对kruskal的定义为：
**先构造一个只含 n 个顶点、而边集为空的子图，把子图中各个顶点看成各棵树上的根结点，之后，从网的边集 E 中选取一条权值最小的边，若该条边的两个顶点分属不同的树，则将其加入子图，即把两棵树合成一棵树，反之，若该条边的两个顶点已落在同一棵树上，则不可取，而应该取下一条权值最小的边再试之。依次类推，直到森林中只有一棵树，也即子图中含有 n-1 条边为止。**
简而言之，Kruskal算法进行调度的单位是边,它的信仰为:所有边能小则小，算法的实现方面和并查集(不相交集合)很像，要用到并查集判断两点是否在同一集合。
而算法的具体步骤为：
1、将边(以及2顶点)的对象依次加入集合(优先队列)q1中。初始所有点相互独立。
2、取出当前q1最小边，判断边的两点是否联通。
3、如果联通，跳过，如果不连通，则使用union（并查集合并）将两个顶点合并。这条边被使用(可以储存或者计算数值)。
4、重复2，3操作直到集合（优先队列）q1为空。此时被选择的边构成最小生成树。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126161337359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126162702681.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
## Prim算法
除了Kruskal算法以外，普里姆算法（Prim算法）也是常用的最小生成树算法。虽然在效率上差不多。但是贪心的方式和Kruskal完全不同。prim算法的核心信仰是：从已知扩散寻找最小。它的实现方式和Dijkstra算法相似但稍微有所区别，Dijkstra是求单源最短路径。而每计算一个点需要对这个点从新更新距离。而prim甚至不用更新距离。直接找已知点的邻边最小加入即可！

对于具体算法具体步骤，大致为：

寻找图中任意点，以它为起点，它的所有边V加入集合(优先队列)q1,设置一个boolean数组bool[]标记该位置已经确定。
从集合q1找到距离最小的那个边v1并判断边另一点p是否被标记(访问)，如果p被标记说明已经确定那么跳过，如果未被标(访问)记那么标记该点p,并且与p相连的未知点(未被标记)构成的边加入集合q1，边v1(可以进行计算距离之类，该边构成最小生成树) .
重复1，2直到q1为空，构成最小生成树 ！
大体步骤图解为：![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126161421982.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126162650197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
因为prim从开始到结束一直是一个整体在扩散，所以不需要考虑两棵树合并的问题，在这一点实现上稍微方便了一点。

当然，要注意的是最小生成树并不唯一，甚至同一种算法生成的最小生成树都可能有所不同，但是相同的是无论生成怎样的最小生成树：

能够保证所有节点连通(能够满足要求和条件)
能够保证所有路径之和最小(结果和目的相同)
最小生成树不唯一，可能多样的
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126161513925.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
## 程序结果
根据上图中提供的例子发现prim和kruskal算法最终的结果都是连接距离为28
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126163016415.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126163054839.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly96aGFuZ3ZhbHVlLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
## 总结
最小生成树算法理解起来也相对简单，实现起来也不是很难。Kruskal和Prim主要是贪心算法的两种角度。
一个从整体开始找最小边，遇到关联不断合并，
另一个从局部开始扩散找身边的最小不断扩散直到生成最小生成树。在学习最小生成树之前最好学习一下dijkstra算法和并查集。

