# Java API Knowledge

## ArrayList 和 LinkedList

- ArrayList是基于索引的数据接口，它的底层是数组。它可以以O(1)时间复杂度对元素进行随机访问。
- LinkedList是以元素列表的形式存储它的数据，每一个元素都和它的前一个和后一个元素链接在一起，在这种情况下，查找某个元素的时间复杂度是O(n)。
- 相对于ArrayList，LinkedList的插入，添加，删除操作速度更快，因为当元素被添加到集合任意位置的时候，不需要像数组那样重新计算大小或者是更新索引。
- LinkedList比ArrayList更占内存，因为LinkedList为每一个节点存储了两个引用，一个指向前一个元素，一个指向下一个元素。
- ArrayList的实现用的是数组，LinkedList是基于链表，**ArrayList适合查找**，**LinkedList适合增删**。

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