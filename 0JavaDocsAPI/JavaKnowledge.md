# Java API Knowledge

## ArrayList 和 LinkedList

- ArrayList是基于索引的数据接口，它的底层是数组。它可以以O(1)时间复杂度对元素进行随机访问。
- LinkedList是以元素列表的形式存储它的数据，每一个元素都和它的前一个和后一个元素链接在一起，在这种情况下，查找某个元素的时间复杂度是O(n)。
- 相对于ArrayList，LinkedList的插入，添加，删除操作速度更快，因为当元素被添加到集合任意位置的时候，不需要像数组那样重新计算大小或者是更新索引。
- LinkedList比ArrayList更占内存，因为LinkedList为每一个节点存储了两个引用，一个指向前一个元素，一个指向下一个元素。
- ArrayList的实现用的是数组，LinkedList是基于链表，**ArrayList适合查找**，**LinkedList适合增删**。

## Stack 和 Deque

一个更加完整，一致的，后进先出的栈相关的操作，应该由 Deque 接口提供。并且，也推荐使用 Deque 这种数据结构（比如 ArrayDeque）来实现。

```java
Deque<Integer> stack = new ArrayDeque<Integer>();
```

1. Java 中的 Stack 类到底怎么了？
   
Java 中的 Stack 类，最大的问题是，继承了 Vector 这个类。Vector 就是一个动态数组。继承使得子类继承了父类的所有公有方法。而 Vector 作为动态数组，是有能力在数组中的任何位置添加或者删除元素的。因此，Stack 继承了 Vector，Stack 也有这样的能力。这就破坏了栈这种数据结构的封装。

2. 为什么使用接口？

接口在 OOP 设计中，也是非常重要的概念。并且，在近些年，变得越来越重要。甚至发展出了“面向接口的编程”这一思想（Interface-based programming）。

在 Java 语言中，Queue 就是一个接口。我们想实现一个队列，可以这么写：

```java
Queue<Integer> q1 = new LinkedList<>();
Queue<Integer> q2 = new ArrayDeque<>();
```

q1 和 q2 的底层具体实现不同，一个是 LinkedList，一个是 ArrayDeque。但是，从用户的角度看，q1 和 q2 是一致的：都是一个队列，只能执行队列规定的方法。

底层开发人员可以随意维护自己的 LinkedList 类或者 ArrayDeque 类，只要他们满足 Queue 接口规定的规范；**接口的设计相当于做了访问限制。**

3. LinkedList 还是 ArrayQueue 来实现 Deque

Java 官方推荐的创建栈的方式，使用了 Deque 接口。并且，在底层实现上，使用了 ArrayDeque，也就是基于动态数组的实现。为什么？

动态数组是可以进行扩容操作的。在触发扩容的时候，时间复杂度是 O(n) 的，但整体平均时间复杂度（Amortized Time）是 O(1)。

动态数组是可以进行扩容操作的。在触发扩容的时候，时间复杂度是 O(n) 的，但整体平均时间复杂度（Amortized Time）是 O(1)。

虽然如此，可是实际上，当数据量达到一定程度的时候，链表的性能是远远低于动态数组的。

这是因为，对于链表来说，每添加一个元素，都需要重新创建一个 Node 类的对象，也就是都需要进行一次 new 的内存操作。而对内存的操作，是非常慢的。

因此，甚至有人建议：在实践中，尤其是面对大规模数据的时候，不应该使用链表！

4. Vector 

实际上，Vector 这个类不仅仅是简单的一个动态数组而已，而更进一步，保证了线程安全。

因为要保证线程安全，所以 Vector 实际上效率也并不高。

Java 官方的 Vector 文档中明确指出了：如果你的应用场景不需要线程安全的特性，那么对于动态数组，应该使用 ArrayList。

## map 和 set

## java箭头函数，lambda表达式

## 常用数据结构的时间复杂度

|Data Structure|新增|查询/Find|删除/Delete|GetByIndex|
|---|---|---|---|---|
|数组  Array (T[]) |	O(n) |	O(n) 	|O(n) |	O(1)
|链表 Linked list (LinkedList<T>) |	O(1)| 	O(n) |	O(n) |	O(n)
Resizable array list (List<T>) |	O(1) 	|O(n) |	O(n) |	O(1)
|Stack (Stack<T>) |	O(1) |	- |	O(1) |	-|
|Queue (Queue<T>) 	|O(1) 	|- |	O(1) |	-|
|Hash table (Dictionary<K,T>) |	O(1) |	O(1) |	O(1) |	-|
|Tree-based dictionary(SortedDictionary<K,T>) |	O(log n) |	O(log n) |	O(log n)| 	-|
|Hash table based set (HashSet<T>) |	O(1) |	O(1) |	O(1) |	-|
|Tree based set (SortedSet<T>) |	O(log n) |	O(log n) 	|O(log n) |	-|

## Java 运算符优先级

下表中具有最高优先级的运算符在的表的最上面，最低优先级的在表的底部。

|类别|操作符|关联性|
|:---:|:---:|---|
|后缀|() [] . (点操作符)|左到右|
|一元|++ -- ！ ~|从右到左|
|乘性|*  /  ％|左到右|
|加性|+ -|左到右|
|移位|>> >>> <<|左到右|
|关系|> >= <> <=|左到右|
|相等|== !=|左到右|
|按位与|＆|左到右|
|按位异或|^|左到右|
|按位或|\||左到右|
|逻辑与|&&|左到右|
|逻辑或|\| \||左到右|
|条件|？：|从右到左|
|赋值|= += -= *= /= ％= >>= <<= ＆= ^= |从右到左|
|逗号|，|左到右|

## 由数据范围反推算法复杂度以及算法内容

一般ACM或者笔试题的时间限制是1秒或2秒。
在这种情况下，C++代码中的操作次数控制在 107107 为最佳。

下面给出在不同数据范围下，代码的时间复杂度和算法该如何选择：

1. $n≤30$, 指数级别, dfs+剪枝，状态压缩dp
2. $n≤100 => O(n3)$，floyd，dp
3. $n≤1000 => O(n2)，O(n2logn)$，dp，二分，朴素版Dijkstra、朴素版Prim、Bellman-Ford
4. $n≤10000 => O(n∗\sqrt{n})$，块状链表、分块、莫队
5. $n≤100000 => O(nlogn)$ => 各种sort，线段树、树状数组、set/map、heap、dijkstra+heap、6. prim+heap、spfa、求凸包、求半平面交、二分
6. $n≤1000000 => O(n), 以及常数较小的 O(nlogn) 算法 => hash、双指针扫描、并查集，kmp、AC自动机，常数比较小的 O(nlogn)的做法：sort、树状数组、heap、dijkstra、spfa
7. $n≤10000000 => O(n)$，双指针扫描、kmp、AC自动机、线性筛素数
8. $n≤10^9 => O(\sqrt{n})$，判断质数
9. $n≤10^18 => O(logn)$，最大公约数，快速幂
10. $n≤10^1000 => O((logn)^2)$，高精度加减乘除
11. $n≤10^100000 => O(logn×loglogn)$，高精度加减、FFT/NTT

作者：yxc
链接：https://www.acwing.com/blog/content/32/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。