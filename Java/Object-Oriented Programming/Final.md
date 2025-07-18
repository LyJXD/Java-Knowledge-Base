## final修饰类
- **定义**  
	当final关键字修饰一个类[[Class]]，则该类会成为最终类，该类不能被继承，但是可以有父类。适用于工具类、常量类、安全性要求高的类。
- **示例**
```java
// 类名为Father的类被final关键字修饰，不能被继承
final class Father {
} 

// ❌ 报错 
class Son extends Father {
}
```

## final修饰变量
- **定义**  
	1. `final` 修饰的变量只能被赋值一次，赋值后不能修改，适用于定义常量，一般与 `static` 连用。
	2. `final` 修饰引用类型变量时，不能再指向其他对象，但对象内部内容是可变的。
- **示例**
```java
// final 修饰的变量只能被赋值一次，赋值后不能修改
final int MAX_COUNT = 100;
MAX_COUNT = 200;          // ❌ 报错

// final 修饰引用类型变量时，不能再指向其他对象，但对象内部内容是可变的。
final List<String> list = new ArrayList<>();
list.add("abc");          // ✅ 合法
list = new ArrayList<>(); // ❌ 报错
```
## final修饰成员方法
- **定义**  
	`final` 修饰的方法不能被子类[[Inheritance#重写]]，保证方法行为在继承体系中保持一致。
- **示例**  
