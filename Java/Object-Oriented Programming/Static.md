
## 静态变量
在类中一个成员变量可用 `static` 关键字来修饰，这样的成员变量称为 `static` 成员变量，或静态成员变量。而没有用 `static` 关键字修饰的成员变量称为非静态成员变量。
- **示例** 
```java
public class Student {
    // 静态成员变量
    private static String SchoolName;
    private static int nums;
    
    // 非静态成员变量
    private String name;
    private int age;
}
```
建议使用类名来访问静态变量，因为它们与类相关联，而不是与特定对象实例相关。
## 静态方法
静态方法是属于类而不是类的实例的方法。它可以在不创建类的实例的情况下被调用。静态方法通常用于执行与类相关的操作，而不需要访问或修改特定实例的状态。
- **示例**
```java
public class Student {
    private static String SchoolName;
    private static int nums;
    
    // 静态成员方法
    public static String getSchoolName() {
        return Student.SchoolName;
    }
}
```

## 静态代码块
