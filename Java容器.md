# 一、概要
容器主要包含了Collection和Map两种，Collection存储着对象的集合，而Map存储着健值对（两个对象）的映射表
## Collection
![](./picture/JavaCollection.png)
### 1.set
- TreeSet:基于红黑树实现，支持有序性操作，例如根据一个范围查找元素的操作，但是查找效率不如HashSet, HashSet查找的时间复杂度为O(1),TreeSet则为O(logN)
- HashSet:基于哈希表实现，支持快速查找，但不支持有序性操作。并且失去了元素的插入顺序信息，也就是说使用Iterator遍历HashSet得到的结果是不确定的。
- LinkedHashSet:具有HashSet的查找效率，且内部使用双向链表维护元素的插入顺序。
### 2.List
- ArrayList:基于动态数组实现，支持随机访问
- Vector：和ArrayList类似，但它是线程安全的
- LinkedList：基于双向链表实现，只能顺序访问，但是可以快速地在链表中间插入和删除元素。不仅如此，LinkedList还可以用作栈、队列和双向队列
### 3.Queue
- LinkedList:可以使用它来实现双向队列
- PriorityQueue:基于堆结构实现，可以用它来实现优先队列
## Map
![](./picture/JavaMap.png)

- TreeMap:基于红黑树实现的
- HashMap:基于哈希表实现的
- HashTable:和HashMap类似，但它是线程安全的，但它是遗留类，不应该去使用它。可以使用ConcurrentHashMap来支持线程安全。
- LinkedHashMap:使用双向链表来维护元素的顺序，顺序为插入顺序或者最近最少使用（LRU）顺序。
# 容器中的设计模式
## 迭代器模式
![](./picture/JavaIterable.png)

Collection继承了Iterable接口，其中的iterator()方法能够产生一个Iterator对象，通过该对象就可以迭代遍历Collection中的元素。
	
	List<String> list = new ArrayList<>();
	list.add("a");
	list.add("b");
	for (String item : list){
		System.out.println(item);
	}

## 适配器模式
java.util.Arrays的asList()可以把数组类型转换为List类型，需要注意的是asList()的参数为泛型的变长参数，不能使用基本类型数组作为参数，只能使用相应的包装类型数组。

	Integer[] arr = {1,2,3};
	List list = Arrays.asList(arr);
	List list = Arrays.asList(1,2,3);

