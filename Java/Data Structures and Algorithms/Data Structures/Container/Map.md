在Java的集合框架中，Map是一个接口类，该类没有继承自Collection，该类中存储的是 `<K,V>` 结构的键值对，并且 `K` 一定是唯一的，不能重复。
Map提供了一种基于键进行查找和操作的数据结构。Map接口的实现类提供了丰富的方法来操作键值对，例如添加、删除、更新和查找。
- **特点**
	1. Map是一个接口，不能直接实例化对象，只能实例化其实现类。
	2. Map中存放键值对的 Key 是唯一的， value 是可以重复的。
	3. Map中的 Key 可以全部分离出来，存储到 Set 中来进行访问。
	4. Map中的 value 可以全部分离出来，存储在Collection的任何一个子集合中。
	5. Map中键值对的 Key 不能直接修改， value 可以修改，如果要修改 key ，只能先将该 key 删除掉，然后再来进行重新插入。
	6. Map的自动去重，需要重写 `hashCode()` 保证两个对象的存储位置一致，并重写 `equals()` 保证对象的值一致，去重后将新对象将覆盖原对象。
## HashMap
`HashMap` 在JDK1.8之后底层数据结构是**数组+链表+红黑树**。
链表是为了解决哈希冲突的，当数组中发生哈希冲突的时候，会使用拉链法将冲突的元素连成一个链表，一个链表中都是冲突的元素。当链表长度过长的时候，会将链表自动转换为红黑树，以提高检索性能。在 Java 8 中，当链表的长度大于 8 的时候，链表就会转换为红黑树。当红黑树的节点个数小于 6 的时候，就会将红黑树转换为链表。
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