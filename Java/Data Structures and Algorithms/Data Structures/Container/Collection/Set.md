Set接口作为Java集合框架的核心组成部分，与List形成鲜明对比，其核心特征在于**元素唯一性**。与Map接口不同，Set仅存储单一元素而非键值对，但底层实现与[[Map]]存在技术同源性。

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
`TreeSet` 是一个底层基于 `TreeMap` 实现的集合，存储的元素必须实现 `Comparable` 接口，或者构造时传入 `Comparator` ，**即元素必须可排序**。
- **特点**
	1. 插入和删除效率较低。
	2. 自动排序，无索引，自动去重。
	3. 不允许 null 元素，非线程安全。
	4. 有丰富的导航和范围查询方法。
- **使用场景**
	1. 需要按键排序存储。
	2. 支持范围查询（如获取大于某值的所有元素）。
- **示例**
```java
public class SetLearn {  
    public static void main(String[] args) {  
		TreeSet<Integer> set1 = new TreeSet<>();  
        set1.add(10);  
        set1.add(20);  
        set1.add(30);  
        set1.add(40);  
        
        // 获取 [20, 40) 区间内的子集  
        System.out.println(set1.subSet(20, 40)); // 输出：[20, 30]  
        // 获取小于 30 的元素  
        System.out.println(set1.headSet(30));    // 输出：[10, 20]  
        // 获取大于等于 20 的元素  
        System.out.println(set1.tailSet(20));    // 输出：[20, 30, 40]  
        
        //返回严格大于给定元素的最小元素  
        System.out.println(set1.higher(25));     // 输出：30  
        System.out.println(set1.higher(40));     // 输出：null（没有更大的）  
        
        //返回小于等于给定元素的最大元素  
        System.out.println(set1.floor(25));      // 输出：20  
        System.out.println(set1.floor(30));      // 输出：30  
        //返回大于等于给定元素的最小元素  
        System.out.println(set1.ceiling(25));    // 输出：30  
        System.out.println(set1.ceiling(30));    // 输出：30  
        
        // treeSet 可排序
        // 学生类实现排序功能（不推荐）  
        // 匿名内部类实现排序功能（推荐）  
        Set<Student> set2 = new TreeSet<>(new Comparator<Student>() {  
            @Override            
            public int compare(Student o1, Student o2) {  
                return o1.getAge() - o2.getAge();  
            }  
        });  
        set2.add(s1);  
        set2.add(s2);  
        set2.add(s3);  
        System.out.println(set2);  
    }  
}  
  
class Student /*implements Comparable<Student>*/{  
    private String name;  
    private int age;  
    
    public Student(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
     
    @Override  
    public String toString() {  
        return "Student{" +  
                "name='" + name + '\'' +  
                ", age=" + age +  
                '}';  
    }  
    
    //@Override  
    //public int compareTo(Student o) {    
    //    // 正 this排o后面  
    //    // 负 this排o前面  
    //    // 0 不存(去重）  
    //  
    //    int res = this.getAge() - o.getAge();    
    //    // 如果年龄一样，根据名字排序  
    //    res = res == 0 ? this.getName().compareTo(o.getName()) : res;  
    //    
    //    return res;    
    //}
}
```