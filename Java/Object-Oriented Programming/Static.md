
## 静态变量


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

## 静态方法

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