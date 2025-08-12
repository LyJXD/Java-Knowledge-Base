List是一种常用的集合类型，它可以存储任意类型的对象，也可以结合泛型来存储具体的类型对象，本质上就是一个容器。由于List是接口，因此无法从中创建对象。
- **为了使用List接口的功能，我们可以使用以下类**
	1. 数组列表（ArrayList类）
	2. 链表（LinkedList类）
	3. 向量（vector类）
	4. 堆栈（Stack类）
- **特点**  
	1. 有序性：List中的元素是按照添加顺序进行存放的。有下标，下标从0开始。
	2. 可重复性：List中可以存储重复的元素。
	3. List接口包括Collection接口的所有方法，因为Collection是List的超级接口。

## ArrayList
`ArrayList` 是Java集合框架中的一个类，实现了 `List` 接口。它使用动态数组来存储元素，因此能够快速地进行随机访问和迭代操作。与 `LinkedList` 相比，`ArrayList` 提供了更快的查找和更新操作，但在插入和删除大量元素时性能较差。
- **特点**
	1. `ArrayList` 的底层使用数组，提供了O(1)时间复杂度的随机访问。
	2. `ArrayList` 在末尾插入或删除元素的时间复杂度为O(1)，在中间插入或删除元素的时间复杂度为O(n)。
	3. 当数组满时，`ArrayList` 会将其容量增加到原来的 1.5 倍
	4. `ArrayList` 是线程不安全的，没有 `synchronized` 关键字修饰。
	5. jdk8的 `ArrayList` 刚开始创建是空数组，只有添加数据的时候才会进行加入容量默认10。
### 使用
- **示例**
```java
public class ArrayListExample {
    public static void main(String[] args) {
        // 创建 ArrayList
        ArrayList<String> list = new ArrayList<>(Arrays.asList("a", "b", "c"));
        // 添加元素
        list.add("d");
        list.add(1, "e");
        list.addAll(Arrays.asList("f", "g", "h"));
        
        // 访问元素
        System.out.println("Element at index 2: " + list.get(2));
        System.out.println("List size: " + list.size());
        
        // 修改元素
        list.set(1, "x");
        
        // 删除元素
        list.remove(2);
        list.remove("g");
        
        // 遍历列表
        for (String element : list) {
            System.out.println(element);
        }
        
        // 检查元素
        System.out.println("List contains 'a': " + list.contains("a"));
        System.out.println("Index of 'a': " + list.indexOf("a"));
        
        // 转换为数组
        String[] array = list.toArray(new String[0]);
        System.out.println("Array: " + Arrays.toString(array));
        
        // 克隆列表
        ArrayList<String> clonedList = (ArrayList<String>) list.clone();
        System.out.println("Cloned list: " + clonedList);
        
        // 线程安全的列表
        List<String> synchronizedList = Collections.synchronizedList(new ArrayList<>(list));
        
        synchronized (synchronizedList) {
            Iterator<String> iterator = synchronizedList.iterator();
            while (iterator.hasNext()) {
                System.out.println(iterator.next());
            }
        }
    }
}
```

## LinkedList
