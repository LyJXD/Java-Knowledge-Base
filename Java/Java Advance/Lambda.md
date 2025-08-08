Lambda表达式，也可称为闭包，它是推动 Java 8 发布的最重要新特性。
Lambda表达式是一个匿名函数，是匿名函数的简写形式，我们可以把Lambda表达式理解为是一段可以传递的代码（将代码像数据一样进行传递），可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使Java的语言表达能力得到了提升。
- **特点**  
	Lambda表达式不是万能的，他需要函数式接口的支持。
	函数式接口就是一个有且仅有一个抽象方法，但是可以有多个非抽象方法的接口。
- **语法**
```java
实现的这个接口中的抽象方法中的形参列表 -> 抽象方法的处理
```
- **示例**
```java
public class Test {
    public static void main(String[] args) {
        Integer[] ints = {98, 243, 35, 13, 57, 243};
        List<Integer> list = Arrays.asList(ints);
        
        list.sort(new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2-o1;
            }
        });
        System.out.println(list);
        //[243, 243, 98, 57, 35, 13]
        
        //使用Lambda表达式
        list.sort((o1,o2)->(o1-o2));
        System.out.println(list);
        //[13, 35, 57, 98, 243, 243]
    }
}
```