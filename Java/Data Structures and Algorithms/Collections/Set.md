Set接口作为Java集合框架的核心组成部分，与List形成鲜明对比，其核心特征在于**元素唯一性**。与Map接口不同，Set仅存储单一元素而非键值对，但底层实现与Map存在技术同源性。

## HashSet
`HashSet` 是一个底层基于 `HashMap` 实现的Set集合，内部维护一个 `HashMap<E, Object>`，添加的元素作为 `HashMap` 的 `key` ，`value` 是一个空对象。
- **特点**
	1. 插入和查询效率高。  
	2. 非线程安全。  
	3. 无序，无索引，自动去重。
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
	2. 严格维护FIFO顺序。
	3. 无索引，自动去重。  
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