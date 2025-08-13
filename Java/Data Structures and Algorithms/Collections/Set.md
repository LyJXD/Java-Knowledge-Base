Set接口作为Java集合框架的核心组成部分，与List形成鲜明对比，其核心特征在于**元素唯一性**。与Map接口不同，Set仅存储单一元素而非键值对，但底层实现与Map存在技术同源性。

## HashSet
`HashSet` 是一个底层基于 `HashMap` 实现的Set集合，内部维护一个 `HashMap<E, Object>`，添加的元素作为 `HashMap` 的 `key` ，`value` 是一个空对象。
- **特点**
	1. 插入和查询效率高。  
	2. 无序，无索引，自动去重。
	3. 非线程安全。  
- **使用场景**
	1. 存储不需要顺序的唯一元素。
	2. 快速查找、插入、删除操作。
- **示例**
```java
Set<String> set = new HashSet<>();
set.add("c");
set.add("a");
set.add("b");
System.out.println(set); // 输出顺序不确定，如 [a, b, c] 或 [c, a, b]
```
## LinkedHashSet
`LinkedHashSet` 是一个继承 `HashSet` ，底层基于 `LinkedHashMap` 实现的Set集合，利用 `LinkedHashMap` 的双向链表结构保持插入或访问顺序。
- **特点**
	1. 保留插入顺序，同时支持高效的增删查。
	2. 严格维护FIFO顺序，无索引，自动去重。
	3. 非线程安全。  
- **使用场景**
	需要保持插入顺序或访问顺序，同时需要去重功能。
- **示例**
```java
Set<String> set = new LinkedHashSet<>();
set.add("c");
set.add("a");
set.add("b");
System.out.println(set); // 输出顺序固定：[c, a, b]
```
## TreeSet
`TreeSet` 是一个底层基于 `TreeMap` 实现的有序集合，存储的元素必须实现 `Comparable` 接口，或者构造时传入 `Comparator` ，**即元素必须可排序**。
- **特点**
- **示例**
```java
        TreeSet<Integer> set = new TreeSet<>();
        set.add(10);
        set.add(20);
        set.add(30);
        set.add(40);
        
        // 获取 [20, 40) 区间内的子集
        System.out.println(set.subSet(20, 40)); // 输出：[20, 30]
        // 获取小于 30 的元素
        System.out.println(set.headSet(30)); // 输出：[10, 20]
        // 获取大于等于 20 的元素
        System.out.println(set.tailSet(20)); // 输出：[20, 30, 40]
        
        //返回严格大于给定元素的最小元素
        System.out.println(set.higher(25)); // 输出：30
        System.out.println(set.higher(40)); // 输出：null（没有更大的）
        
        //返回小于等于给定元素的最大元素
        System.out.println(set.floor(25)); // 输出：20
        System.out.println(set.floor(30)); // 输出：30
        
        //返回大于等于给定元素的最小元素
        System.out.println(set.ceiling(25)); // 输出：30
        System.out.println(set.ceiling(30)); // 输出：30
```