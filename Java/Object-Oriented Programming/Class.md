## 类
类是具有相同属性和行为的一组对象([[Object]])的集合，是对现实世界中一类事物的抽象描述。它定义了该类所有对象的共同特征（属性）和行为（方法[[Method]]）。
### 定义
一个Java类主要由属性（成员变量）、构造方法、成员方法以及主方法四要素组成：
- **属性**  
	用于描述该类的共性特性，一个类可以有多个属性。
- **构造方法**  
	一般用于在创建对象时给对象的属性赋值，构造方法的名称和类名称必须相同。
- **成员方法**  
	用于描述该类所具有的行为，一个类可以有多个成员方法。
- **主方法**  
	是一个非常特殊的方法，它是Java程序的入口，当我们要运行某个类时就需要在该类中定义主方法，主方法对于类并非都是必要的。
### 创建类
一个java文件中可以定义多个class类，但只有一个类被 `public` 修饰，该类名必须为文件名。
- **语法**  
```java
访问修饰符 class 类名 {
    // 定义属性
    属性1;
    属性
    属性3;
    
    // 定义方法
    构造方法1;
    构造方法2;
    构造方法3;
    成员方法1;
    成员方法2;
    成员方法3;
    
    主方法;
}
```
- **示例**  
```java
class Person {  
    // 定义属性  
    String name;  
    int age;  
    
    // 构造方法  
    Person() {  
    }    
    Person(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
    
    // 成员方法  
    void eat() {  
        System.out.println("吃东西");  
    }  
    void sleep() {  
        System.out.println("睡觉");  
    }  
    void introduceMyself() {  
        System.out.println("my name is " + name + ", " + age + " years old.");  
    }  
}
```
### 构造方法
- **特点**  
	1. 方法名与类名相同，大小写也要一致。
	2. 没有返回值类型，连 `void` 都没有。
	3. 没有具体的返回值（不能由 `return` 带回结果数据）。
- **执行时机**  
	1. 创建对象的时候由[[JVM]]调用，不能手动调用构造方法。
	2. 每创建一次对象，就会调用过一次构造方法。
- **构造方法的定义**  
	如果没有定义构造方法，系统将给出一个默认的无参数构造方法；如果定义了构造方法，系统将不再提供默认的构造方法。
- **构造方法的重载** 
	带参构造方法，和无参构造方法，两者方法名相同，但是参数不同，这叫做构造方法的重载。
- **语法**
```java
public class Person{  
    修饰符 类名（参数）{  
        方法体;  
    }  
}
```
### 主方法
每个类都可以定义一个特殊的方法——主方法，有了这个方法就可以让JVM来执行这个类程序。
- **语法**  
```java
// 主方法的格式为固定句式
public static void main(String[] args)
```

## 实体类
### JavaBean
- **定义**  
	JavaBean是一种遵循特定命名规范的Java实体类，主要用于封装([[Encapsulation]])数据并进行组件间的数据传递。
- **规范**    
	1. 有一个无参构造方法。
	2. 所有属性必须是 `private` 修饰。
	3. 为每个属性提供 `public` 的getter和setter方法。
	4. 实现Serializable接口（可选）。
- **示例**  
```java
public class User implements Serializable {  
    private int id;  
    private String name;  
    private String email;  
    
    public User() {  
        // 无参构造器  
    }  
    
    // Getter 和 Setter 方法  
    public int getId() {  
        return id;  
    }  
    
    public void setId(int id) {  
        this.id = id;  
    }  
    
    public String getName() {  
        return name;  
    }  
    
    public void setName(String name) {  
        this.name = name;  
    }  
    
    public String getEmail() {  
        return email;  
    }  
    
    public void setEmail(String email) {  
        this.email = email;  
    }  
    
    @Override  
    public String toString() {  
        return "User{id=" + id + ", name='" + name + "', email='" + email + "'}";  
    }  
}
```

## 抽象类
当一个类中给出的信息不够全面时，（比方说有无法确定的行为），它给出的信息不足以描绘出一个具体的对象，这时我们往往不会实例化该类，这种类就是抽象类。
- **语法**  
	在Java中，我们通过在类前添加关键字 `abstract` 来定义抽象类。
```
 访问权限修饰符  abstract  class  类名{ // }
```
- **抽象方法**  
	 1. 我们将只有方法声明，没有方法体的一类方法统称为抽象方法，抽象方法用关键字 `abstract` 修饰。
	 2. 若父类中定义了一个抽象方法，其所有非抽象子类都必须重写该抽象方法。
	 3. 通过抽象方法，父类引用可以调用子类重写的方法，实现运行时多态。
	 4. 抽象方法允许父类定义接口，而将具体实现推迟到子类中完成，适用于模板方法模式等设计模式。
	 5. 抽象方法不能再使用 `private`，`final`，`static` 关键字来修饰，这几个关键字都和方法重写的目的背道而驰。
- **示例**  
```java
public abstract class Animal {   /** 父类 */
    //将Animal类中的eat() 方法定义为抽象类，具体实现延迟到子类。
    public abstract void eat();
}
 
class Dog extends Animal {      /** 子类 */
    //子类重写父类的抽象方法，也称为子类实现了该抽象方法。
    public void eat() {
        System.out.println("狗是杂食性动物，喜食肉类，喂养时应该以动物蛋白为主，素食为辅。");
    }
}
 
class Test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();
    }
}
```
- **特点**  
	1. 抽象类不能被实例化，只能被继承。
	2. 抽象类可以包含：成员变量，构造方法，抽象方法，具体方法。
	3. 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
	4. 抽象类中的抽象方法只是声明，不包含方法体，即不给出方法的具体功能。
	5. 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。
	6. 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。
- **作用**  
	1. 抽象类作为模板类，为子类提供了一个通用的模板，子类必须实现抽象方法，同时可以复用抽象类中的具体方法。
	2. 抽象类允许在父类中实现一些通用逻辑，而将特定实现延迟到子类中完成。
	3. 抽象类不能被实例化，只能被继承。这确保了某些类只能作为父类使用，不能直接创建对象。
	4. 抽象类是实现多态的一种方式，可以通过父类引用指向子类对象，调用重写的方法。
	5. 抽象类可以为多个子类提供默认行为，避免重复实现相同逻辑，提高代码可维护性和可扩展性。