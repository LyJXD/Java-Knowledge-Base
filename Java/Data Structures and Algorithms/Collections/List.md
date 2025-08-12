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
- **Collection接口中提供了一些常用的List接口方法**
	1. add() - 将元素添加到列表
	2. addAll() - 将一个列表的所有元素添加到另一个
	3. get() - 有助于从列表中随机访问元素
	4. iterator() - 返回迭代器对象，该对象可用于顺序访问列表的元素
	5. set() - 更改列表的元素
	6. remove() - 从列表中删除一个元素
	7. removeAll() - 从列表中删除所有元素
	8. clear() - 从列表中删除所有元素（比removeAll()效率更高）
	9. size() - 返回列表的长度
	10. toArray() - 将列表转换为数组
	11. contains() -  如果列表包含指定的元素，则返回true

## ArrayList
- **特点**
	1. ArrayList的底层是数组。
	2. ArrayList的扩容是1.5倍的扩容。
	3. ArrayList是线程不安全的，没有synchronized关键字修饰。
	4. vector与ArrayList基本相同，是线程安全的，有synchronized关键字修饰方法。
	5. jdk8的ArrayList刚开始创建是空数组，只有添加数据的时候才会进行加入容量默认10。

## LinkedList