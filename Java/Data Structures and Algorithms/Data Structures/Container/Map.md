在Java的集合框架中，Map是一个接口类，该类没有继承自Collection，该类中存储的是 `<K,V>`结构的键值对，并且 **`K` 一定是唯一的，不能重复**。
Map提供了一种基于键进行查找和操作的数据结构。Map接口的实现类提供了丰富的方法来操作键值对，例如添加、删除、更新和查找。
- **特点**
	1. Map是一个接口，不能直接实例化对象，只能实例化其实现类。
	2. Map中存放键值对的 Key 是唯一的， value 是可以重复的。
	3. Map中的 Key 可以全部分离出来，存储到 Set 中来进行访问。
	4. Map中的 value 可以全部分离出来，存储在Collection的任何一个子集合中。
	5. Map中键值对的 Key 不能直接修改， value 可以修改，如果要修改 key ，只能先将该 key 删除掉，然后再来进行重新插入。
	6. Map的自动去重，需要重写 `hashCode()` 保证两个对象的存储位置一致，并重写 `equals()` 保证对象的值一致，**去重后将新对象将覆盖原对象**。
## HashMap
### 基本概念
- **工作原理**
	`HashMap` 使用哈希表来存储数据。键的哈希值通过 `hash()` 方法计算，然后通过哈希函数将哈希值映射到数组的索引位置上。通过链地址法（chaining）来解决哈希冲突，即在每个数组索引处存储一个链表（Java 8及之后版本采用红黑树以提高性能）。
- **Java 8 对HashMap做的优化**
	1. 数据结构
		变化：从 数组+链表 改为 **数组+链表或红黑树**。
		原因：链表是为了解决哈希冲突的，当数组中发生哈希冲突的时候，会使用拉链法将冲突的元素连成一个链表，一个链表中都是冲突的元素。当链表的长度大于8，同时还满足容量大于或等于 MIN_TREEIFY_CAPACITY（默认为 64）的时候，链表就会转换为红黑树，查找时间复杂度由 O(n) 降低至 O(logn)。当红黑树的节点个数小于6的时候，就会将红黑树转换为链表。
		![[Hashmap源代码对红黑树转化阈值的说明.png]]
	2. 链表插入方式
		变化：从头插法改为**尾插法**。
		说明：在 JDK 1.7 中，新元素被放置到链表头部；而在 JDK 1.8 中，遍历链表并将新元素放置到链表尾部。
		原因：JDK 1.7 的头插法在扩容时可能导致链表反转，在多线程环境下可能会产生环状结构，而尾插法则避免了这一问题。
	3. 扩容机制（rehash）
		变化：采用更简单的判断逻辑来决定新位置。
		说明：JDK 1.7 在扩容时需要重新计算每个元素的新哈希值以确定其在新数组中的位置；JDK 1.8 则通过更简化的逻辑直接确定新位置，通常是原索引或者原索引加上新增容量大小。
		原因：这种改变提高了扩容操作的效率。
	4. 扩容时机
		变化：从先判断是否需要扩容再进行插入，变更为先执行插入操作，之后再判断是否需要扩容。
		原因：这样可以减少不必要的扩容检查次数，尤其是在频繁插入但不经常达到扩容阈值的情况下。
	5. 散列函数
		变化：减少了散列函数的操作次数。
		说明：JDK 1.7 的散列函数执行了四次位移和异或操作，而 JDK 1.8 只执行一次。
		原因：尽管多次操作可能提供更好的分布性，但实际上边际效益不大，简化后的散列函数提高了计算速度且对于大多数应用场景来说足够有效。
- **特点**
	1. HashMap 是一个散列表，它存储的内容是键值对映射。
	2. HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 `null`，不支持线程同步。
	3. HashMap 是**无序**的，即不会记录插入的顺序。
	4. HashMap 继承于 AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口。
	5. HashMap 是**非线程安全**的，多线程情况下需要手动同步。
### 常用方法使用
- **示例**
```java
public class MapLearn {  
    public static void main(String[] args) {  
        Map<String, Integer> map = new HashMap<>();  
        // put方法若添加已有元素则返回上一个键对应的值，否则返回null
        map.put("张三", 18);  
        map.put("李四", 19);  
        map.put("王五", 17);  
        map.put("赵六", 20);  
        System.out.println(map);  
        System.out.println(map.size());  
        System.out.println(map.isEmpty());  
        System.out.println(map.get("张三"));  
        System.out.println(map.containsKey("张三"));  
        
        // 遍历  
        // 获取所有的键，通过遍历键获取值  
        Set<String> keys = map.keySet();  
        for (String key : keys) {  
            System.out.println("键：" + key + " 值：" + map.get(key));  
        }  
        System.out.println("--------------------");  
        // 获取所有的键值对，通过遍历键值对获取键和值  
        Set<Map.Entry<String, Integer>> entries = map.entrySet();  
        for (Map.Entry<String, Integer> entry : entries) {  
            System.out.println("键：" + entry.getKey() + " 值：" + entry.getValue());  
        }  
        System.out.println("--------------------");  
        // 使用匿名内部类
        map.forEach((new BiConsumer<String, Integer>() {  
            @Override            
            public void accept(String key, Integer value) {  
                System.out.println("键：" + key + " 值：" + value);  
            }  
        }));  
        // 使用lambda表达式  
        map.forEach((key, value) -> System.out.println("键：" + key + " 值：" + value)); 
    }  
}
```
## LinkedHashMap
`LinkedHashMap` 的底层结构是基于 `HashMap` 实现的，但它在 `HashMap` 的基础上添加了**双向链表**来维护顺序。每个节点在哈希表中存储数据时，不仅存储了键值对，还存储了指向前一个节点和后一个节点的引用。
## TreeMap
`TreeMap` 的底层实现是**红黑树算法**。
红黑树是一种自平衡的二叉查找树，每个节点都只能是红色或者黑色，根节点是黑色，每个叶子节点是黑色的。如果一个结点是红的，则它两个子节点都是黑的。从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。
### 使用
- **示例**
```java
public class TreeMapLearn {  
    public static void main(String[] args) {  
        Map<Integer, String> map1 = Map.of(18, "张三", 19, "李四", 17, "王五");  
        // 存储基本类型的键值对不需要指定排序规则  
        TreeMap<Integer, String> treeMap1 = new TreeMap<>(map1);  
        System.out.println(treeMap1);   // {10=李四, 20=王五, 30=张三}  
        
	    // Student类省略
	    Map<Student, String> map2 = Map.of(  
                new Student("张三", 18), "上海",  
                new Student("李四", 19), "浙江",  
                new Student("王五", 17), "北京");  
        // 存储对象类型的键值对必须指定排序规则  
        TreeMap<Student, String> treeMap2 = new TreeMap<>(new TreeMap<>((o1, o2) ->  
                o1.getAge() - o2.getAge() == 0 ? 
                o1.getName().compareTo(o2.getName()) : o1.getAge() - o2.getAge()  
        ));  
        treeMap2.putAll(map2);  
        treeMap2.forEach((k,v) -> System.out.println(k + ":" + v));  
    }  
}
```