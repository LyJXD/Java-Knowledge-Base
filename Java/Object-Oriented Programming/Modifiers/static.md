## 静态变量 (static [[Variable]])
在类([[Class]])中一个成员变量可用 `static` 关键字来修饰，这样的成员变量称为 `static` 成员变量，或静态成员变量。而没有用 `static` 关键字修饰的成员变量称为非静态成员变量。
- **生命周期**  
	当[[JVM]]第一次加载类，例如创建对象([[Object]])或访问静态变量时，类的 `.class` 文件就会被加载，同时，静态变量会被分配内存并初始化一次（在方法区 / 元空间中）。
	静态变量的生命周期从类加载开始时初始化，一直存在，直到程序结束或类被卸载。
- **作用域**
	静态变量在整个类中可见，它们的作用域覆盖整个类。可以在类的任何方法内部或外部访问静态变量。静态变量在类加载时初始化一次，这份变量内存就是类共享的，始终存在，它的作用域不会因为对象的创建和销毁而改变，即使不创建对象，也可以访问和操作这个静态变量。
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
## 静态方法（static [[Method]])
- **用途**  
	1. 静态方法是属于类而不是类的实例的方法，它可以在不创建类的实例的情况下被调用。
	2. 静态方法通常用于执行与类相关的操作，而不需要访问或修改特定实例的状态。
- **静态方法与实例方法的区别**  
	1. 关联性：静态方法与类本身相关，而实例方法与类的实例相关。
	2. 调用方式：静态方法通过类名调用，而实例方法需要通过对象实例来调用。
	3. 访问权限：静态方法可以访问类的静态成员，但不能访问非静态成员（实例成员）。实例方法可以访问类的静态和非静态成员。
	4. 内部引用：静态方法中不能使用 `this` 关键字，因为它没有当前对象的引用。实例方法可以使用 `this` 来引用当前对象。
	5. 生命周期：静态方法在类加载时初始化，而实例方法在对象创建时初始化。
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
## 静态代码块（static [[Code Block]])
[[Code Blocks#静态代码块]]
## 静态内部类