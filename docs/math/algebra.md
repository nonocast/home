# 线性代数 

## 从代数开始

这段摘自[MIT牛人解说数学体系](http://www.penglixun.com/study/science/mit_math_system.html): 

> 如果说古典微积分是分析的入门，那么现代代数的入门点则是两个部分：线性代数(linear algebra)和基础的抽象代数(abstract algebra)——据说国内一些教材称之为近世代数。

> 代数——名称上研究的似乎是数，在我看来，主要研究的是运算规则。一门代数， 其实都是从某种具体的运算体系中抽象出一些基本规则，建立一个公理体系，然后在这基础上进行研究。一个集合再加上一套运算规则，就构成一个代数结构。在主要的代数结构中，最简单的是群(Group)——它只有一种符合结合率的可逆运算，通常叫“乘法”。如果，这种运算也符合交换率，那么就叫阿贝尔群 (Abelian Group)。如果有两种运算，一种叫加法，满足交换率和结合率，一种叫乘法，满足结合率，它们之间满足分配率，这种丰富一点的结构叫做环(Ring)， 如果环上的乘法满足交换率，就叫可交换环(Commutative Ring)。如果，一个环的加法和乘法具有了所有的良好性质，那么就成为一个域(Field)。基于域，我们可以建立一种新的结构，能进行加法和数乘，就构成了线性代数(Linear algebra)。

> 代数的好处在于，它只关心运算规则的演绎，而不管参与运算的对象。只要定义恰当，完全可以让一只猫乘一只狗得到一头猪:-)。基于抽象运算规则得到的所有定理完全可以运用于上面说的猫狗乘法。当然，在实际运用中，我们还是希望用它 干点有意义的事情。学过抽象代数的都知道，基于几条最简单的规则，比如结合律，就能导出非常多的重要结论——这些结论可以应用到一切满足这些简单规则的地 方——这是代数的威力所在，我们不再需要为每一个具体领域重新建立这么多的定理。

Spark & Shine在文中的一段解释也很精彩,

> 线性代数是抽象代数特殊的一类，其代数结构为：向量空间(vector spaces，也叫线性空间) + 线性变换(linear mappings)。很容易将线性代数和矩阵理论等同起来，但其实是不一样的，讨论线性变换是基于选定一组基的前提下。摘抄mathoverflow上的一个回答(原文在这里)：

> When you talk about matrices, you’re allowed to talk about things like the entry in the 3rd row and 4th column, and so forth. In this setting, matrices are useful for representing things like transition probabilities in a Markov chain, where each entry indicates the probability of transitioning from one state to another.

具体操作层面就不做更多的展开了, 最核心的两个概念就是向量空间和线性变换，直接看视频:

- [Essense of Linear Algebra by @3Blue1Brown](https://www.youtube.com/watch?v=fNk_zzaMoSs)
- [【熟肉】线性代数的本质 - 01 - 向量究竟是什么？_哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/video/av5987715)

这个系列15个chapters, 看完你会怀疑人生, 以前学校里学的是什么鬼。
