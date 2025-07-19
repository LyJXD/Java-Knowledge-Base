## 接口
Java接口是一系列方法([[Method]])的声明，是一些方法特征的集合，一个接口只有方法的特征没有方法的实现，因此这些方法可以在不同的地方被不同的类实现，而这些实现可以具有不同的功能。
- **语法**  
```java
// 接口声明
修饰符 interface 接口名称 [extends 其他的接口名称] {
	// 声明变量
	// 抽象方法
}

// 接口实现
 class 类名 implements 接口名称1, 接口名称2...{
	@Override
	// 重写抽象方法
 }
```
- **示例**  
```java
public interface USB {  
    public void read();  
    public void write();  
}

class KeyBoard implements USB {
    @Override
    public void read() {
        System.out.println("键盘正在通过USB功能读取数据");
    }
    @Override
    public void write() {
        System.out.println("键盘正在通过USB功能写入数据");
    }
}
```
- **接口特点**  
	1. 接口中每一个方法也是隐式抽象的，接口中的方法会被隐式的指定为 `public abstract`（只能是 `public abstract`，其他修饰符都会报错）。
	2. 接口中可以含有变量，但是接口中的变量会被隐式的指定为 `public static final` 变量（并且只能是 `public`，用 `private` 修饰会报编译错误）。
	3. 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。
### 接口与类
- **接口与类的相似点**  
	1. 一个接口可以有多个方法。
	2. 接口文件保存在 .java 结尾的文件中，文件名使用接口名。
	3. 接口的字节码文件保存在 .class 结尾的文件中。
	4. 接口相应的字节码文件必须在与包名称相匹配的目录结构中。
- **接口与类的区别**  
	1. 接口不能用于实例化对象。
	2. 接口没有构造方法。
	3. 接口中所有的方法必须是抽象方法，Java 8 之后 接口中可以使用 `default` 关键字修饰的非抽象方法。
	4. 接口不能包含成员变量，除了 [[Static]] 和 [[Final]] 变量。
	5. 接口不是被类继承了，而是要被类实现。
	6. 接口支持多继承。
- **接口与抽象类的区别**  
	1. 抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
	2. 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 `public static final` 类型的。
	3. 接口中不能含有静态代码块以及静态方法(用 [[Static]] 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
	4. 一个类只能继承一个抽象类，而一个类却可以实现多个接口。
### 接口的继承
- **规则**
	1. 一个接口能继承另一个接口，和类之间的继承方式比较相似。接口的继承使用extends关键字，子接口继承父接口的方法。
	2. 在Java中，类的多继承是不合法，但接口允许多继承。
- **示例**
```java
interface A {
    void methodA();
}

interface B {
    void methodB();
}

// 接口 C 同时继承接口 A 和 B
interface C extends A, B {
    void methodC();
}
```