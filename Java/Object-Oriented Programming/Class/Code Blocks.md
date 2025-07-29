## 局部代码块
- **定义**  
	在方法中出现，可以限定变量生命周期，及早释放，提高内存利用率。
- **示例**
```java
public class Test1{
    public static void main(String[] args) {
        //局部代码块
        {
            int n = 100;
        }
        // 局部代码块中声明的变量在代码块外部访问不到！
        // System.out.println(n);
    }
}
```
## 静态代码块
- **定义**  
	必须有static修饰，必须放在类下。与类一起加载执行。并且静态代码块执行一次
- **示例**
```java
public class Test2 {
    public static String name;
    
    // 静态代码块
    static {
        // 初始化静态资源
        name = "张三";
        System.out.println("静态代码块执行...");
    }
    
    public static void main(String[] args) {
        System.out.println("main方法执行...");
        System.out.println(name);
    }
}
// 输出
// 静态代码块执行...
// main方法执行...
// 张三
```
- **作用**  
	1. **一次性初始化** 静态代码块只在类加载时执行一次，适合用于一次性的初始化操作。
	2. **初始化静态变量** 静态初始化块可以用于初始化静态变量，通常在静态变量的初始值不能直接赋值时使用。
	3. **执行复杂初始化逻辑** 如果静态变量的初始化需要复杂的逻辑或依赖于其他类的加载，可以在静态初始化块中执行这些操作。
	4. **资源管理** 静态初始化块可以用于管理资源，如数据库连接或文件句柄的初始化和释放。
## 构造代码块
- **定义**  
	没有static修饰，必须放在类下。与对象初始化一起加载，即每次调用构造方法都会执行，并且在构造方法前执行。
- **示例**
```java
public class Test3{
    private String name;
    
    // 实例代码块。 无static修饰。
    {
        System.out.println("实例代码块执行...");
        name = "张三";
    }
    
    // 构造器
    public Test3(){
        System.out.println("无参构造方法执行...");
    }
    
    // 有参数构造器
    public Test3(String name){
        System.out.println("有参构造方法执行...");
        this.name = name;
    }
    
    public static void main(String[] args) {
        Test3 t1 = new Test3();
        Test3 t2 = new Test3("李四");
        System.out.println(t1.name + t2.name);
    }
}
// 输出
// 实例代码块执行...
// 无参构造方法执行...
// 实例代码块执行...
// 有参构造方法执行...
// 张三李四
```
## 同步代码块
