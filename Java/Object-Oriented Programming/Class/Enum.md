## 枚举
Java 枚举是一个特殊的类，一般表示一组常量，比如一年的 4 个季节，一年的 12 个月份，一个星期的 7 天，方向有东南西北等。
- **特点**
	1. **有限的实例集合** 枚举类型是一种有限的实例集合，每个实例都是该枚举类型的一个唯一的、已命名的常量。枚举类型的实例在定义时就被预先确定，并且不可修改。
	2. **类型安全** 枚举类型在编译时进行静态类型检查，这意味着编译器可以检测到在使用枚举常量时的类型错误。这提供了更高的类型安全性，避免了一些常见的编程错误。
	3. **唯一性和可比性** 每个枚举常量在枚举类型中都是唯一的，并且可以使用 `==` 操作符进行比较。这使得可以在代码中使用枚举常量来进行精确的比较和判断。
	4. **可读性和可维护性** 枚举类型的常量是有意义的、自描述的，可以直观地理解其含义。这使得代码更易读、易理解和易于维护。同时，枚举类型的常量也可以提供更好的文档和注释。
	5. **可迭代性** 枚举类型可以通过 `values()` 方法获取包含所有枚举常量的数组，并且支持for-each循环遍历。这使得可以方便地对枚举常量进行迭代和处理。
	6. **支持方法和字段** 枚举常量可以具有字段和方法，可以为每个常量定义特定的属性和行为。这使得可以将相关的属性和操作封装在枚举常量内部。
	7. **序列化支持** 枚举类型默认实现了 `Serializable` 接口，可以被序列化和反序列化。这使得可以在网络传输、存储和持久化等场景下使用枚举类型。
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
    RED("RED", 1),
    GREEN("GREEN", 2),
    BLACK("BLACK", 3);
    
    private String color;
    private int ori;
    
    // 构造方法
    private TestEnum(String color, int ori) {
        this.color = color;
        this.ori = ori;
    }
    
    // 主方法
    public static void main(String[] args) {
        TestEnum[] values = TestEnum.values();
        for (TestEnum value : values) {
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