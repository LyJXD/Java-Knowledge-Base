## 继承
### 定义
继承是面向对象的三大特征之一，可以使得子类具有父类的属性和方法，还可以在子类中重新定义，追加属性和方法([[Method]])。即在原有类([[class]])的基础上，进行功能扩展，创建新的类型。
- **特点**  
	1. 继承的本质是对某一批类的抽象，从而实现对现实世界更好的建模。
	2. Java中类只有单继承，没有多继承，允许多层继承。
	3. 成员变量访问遵循就近原则，自己有优先自己的，如果没有则向父类中找。
	4. 在继承关系之中，如果要实例化子类对象，会默认先调用父类构造，再调用子类构造。
	5. 子类默认会调用父类的无参构造器，如果父类没有无参构造器，子类一定需要指定一个带参构造器。
	6. 若子类重写了方法，调用子类的方法。若未重写，调用父类方法（前提是可访问）。
- **语法**
```java
修饰符 class 子类 extends 父类{
    //...
}
```
- **示例** 
```java
class Animal{
    public String name;
    public int age;
    public String color;
    
    public void eat(){
        System.out.println(name + "正在吃饭");
    }
    
    public void sleep() {
        System.out.println(name + "正在睡觉");
    }
}
 
class Cat extends Animal{
    public void bark(){
        System.out.println(name + "正在喵喵喵");
    }
}

class Dog extends Animal{
    public void bark(){
        System.out.println(name + "正在汪汪汪");
    }
}

public class test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Cat cat = new Cat();
        
        dog.name = "大黄";
        dog.color = "黄色";
        dog.age = 3;
        dog.eat();
        dog.sleep();
        dog.bark();
        
        cat.name = "小灰灰";
        cat.color = "灰白";
        cat.age = 1;
        cat.eat();
        cat.sleep();
        cat.bark();
    }
}
```
- **优点**  
	1. 实现了数据和方法的共享。
	2. 提高了代码的复用性(多个类相同的成员可以放到同一个类中)。
	3. 提高了代码的维护性(如果方法的代码需要修改，修改一处即可)。
	4. 提高了代码的可扩展性。
- **缺点**  
	继承让类与类之间产生了关系，类的耦合性增强了，当父类发生变化时子类实现也不得不跟看变化，削弱了子类的独立性。
### super关键字
- `super` 关键字能够实现对父类成员的访问，用来引用当前对象的父类。
- `super(参数)` 调用父类的构造方法（应该为构造方法中的第一条语句）。
- **示例**
```java
class Animal {
	public Animal() { 
		System.out.println("Animal类的无参数构造方法"); 
	}
    void eat() {
        System.out.println("animal : eat");
    }
}
 
class Dog extends Animal {
	public Dog() { 
		super();     // super() 调用父类的构造方法
		System.out.println("Dog类的无参数构造方法"); 
	}
    void eat() {
        System.out.println("dog : eat");
    }
    void eatTest() {
        this.eat();   // this 调用自己的方法
        super.eat();  // super 调用父类方法
    }
}
 
public class Test {
    public static void main(String[] args) {
        Animal a = new Animal();
        a.eat();
        Dog d = new Dog();
        d.eatTest();
    }
}
```
### 重写
重写也称覆盖，是子类对父类非静态、非private、非final方法的实现过程进行重新编写，返回值和形参都不能改变。
- **特点**  
	1. 发生在父类与子类之间。
	2. 子类在重写父类的方法时，一般必须与父类方法原型一致：`修饰符 返回值类型 方法名(参数列表) ` 要完全一致。
	3. JDK7以后，被重写的方法返回值类型可以不同，但是必须是具有父子关系的。
	4. 访问权限不能比父类中被重写的方法的访问权限更低。父类被 `static`、`private` `final` 修饰的方法不能被重写。
	5. 重写方法一定不能抛出新的检查异常或者比被重写方法申明更加宽泛的检查型异常。
- **示例**
```java
public class Father {
    public void eat() {
        System.out.println("吃饭");
    }
}

class Son extends Father{
    @Override
    public void eat() {
        System.out.println("吃烤串");
    }
}

public class test {
	public static void main(String[] args) {
        Son son = new Son();
        son.eat();
    }
}
```
- **toString()**  
	1. 当我们打印一个对象的引用时，实际是默认调用这个对象的toString()方法。
	2. 当打印的对象所在类没有重写Object中的toString()方法时，默认调用的是Object类中toString()方法，返回此对象所在的类及对应的堆空间对象实体的首地址值。
```java
// Obeject类源代码
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```
- **equals()**
	[[String]] 重写了 `equals()` 方法因此可以进行值比较，`equals` 底层代码与 `==` 没有区别。
```java
// Objects类源代码
public boolean equals(Object obj) {  
    return (this == obj);  
}

// String重写
public boolean equals(Object anObject) {  
    if (this == anObject) {  
        return true;  
    }  
    return (anObject instanceof String aString)  
            && (!COMPACT_STRINGS || this.coder == aString.coder)  
            && StringLatin1.equals(value, aString.value);  
}
```
- **hashCode()**
	1. hashCode就是对象的散列码，是根据对象的某些信息推导出的一个整数值，默认情况下表示是对象的存储地址。通过散列码，可以提高检索的效率，主要用于在散列存储结构中快速确定对象的存储地址。
	2. 重写 `equals()` 方法必须重写 `hashCode()` 方法。
	3. 如果两个对象 `equals()` 相等，那么这两个对象的hashCode一定也相同。
	4. 如果两个对象的hashCode相同，不代表两个对象就相同，只能说明这两个对象在散列存储结构中，存放于同一个位置。