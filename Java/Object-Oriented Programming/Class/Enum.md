## 枚举
Java 枚举是一个特殊的类，一般表示一组常量，比如一年的 4 个季节，一年的 12 个月份，一个星期的 7 天，方向有东南西北等。
- **特点**
	1. 枚举是 `final` 的，不能被继承，也不能继承其他类，已隐式继承 `java.lang.Enum`，但可以实现接口。
	2. 枚举类的对象只允许我们显式声明的那几个，这几个实例在类加载时就被创建好了，并且是 `static final` 的。
	3. 枚举跟普通类一样可以用自己的变量、方法和构造方法，构造方法只能使用 `private` 访问修饰符，所以枚举类不能被 `new` 创建对象。。
- **语法**
```java
enum EnumName {
    CONSTANT1,
    CONSTANT2,
    // ...
}
```
- **示例**
```java
public enum TestEnum {
    RED("RED", 0),
    GREEN("GREEN", 1),
    BLACK("BLACK", 2);
    
    private String color;
    private int ori;
    
    // 构造方法
    private TestEnum(String color, int ori) {
        this.color = color;
        this.ori = ori;
    }
    
    public static void main(String[] args) {
        TestEnum[] values = TestEnum.values();
        for (TestEnum value : values) {
	        // ordinal()方法可以找到每个枚举常量的索引，就像数组索引一样。
            System.out.println(value + " ori: " + value.ordinal());
        }
        System.out.println("======================");
        System.out.println(TestEnum.valueOf("RED"));
        System.out.println("======================");
        System.out.println(RED.compareTo(BLACK));
        System.out.println(BLACK.compareTo(GREEN));
    }
}
```
- **优点**
	1. **类型安全** 枚举常量本质是 `public static final` 枚举类实例，确保该常量不可修改且能被外部直接访问。
	2. **命名空间** 枚举常量位于其枚举类型的命名空间内，避免了命名冲突。
	3. **可读性** 枚举值在打印时使用其名称，而不是一个可能没有意义的数字。
	4. **内置方法** Java枚举自带了许多有用的方法，如 `values()`（返回所有枚举常量的数组）和 `valueOf(String)`（将字符串转换为枚举常量）。
	5. **可扩展性**：枚举可以有构造函数、字段、方法和实现接口，这使它们比简单的常量声明更强大。
	6. **集合支持**：枚举可以很容易地与Java集合框架（如EnumSet和EnumMap）一起使用，这些专为枚举设计的集合比一般的集合更高效。