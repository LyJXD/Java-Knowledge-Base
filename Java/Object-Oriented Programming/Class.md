## 类
Java的类是所有Java同类对象的集合，它就像是一个模板，通过该模板可以创建出具有该类所定义的属性和方法的Java对象。类所描述的是所有对象的共性特征，类是一个共性的概念。

### 定义
一个 Java 类主要由属性（变量）、构造方法、成员方法以及主方法四要素组成：
- **属性**  
	用于描述该类的共性特性，一个类可以有多个属性；
- **构造方法**  
	一般用于在创建对象时给对象的属性赋值，构造方法的名称和类名称必须相同；
- **成员方法**  
	用于描述该类所具有的行为，一个类可以有多个成员方法；
- **主方法**  
	是一个非常特殊的方法，它是 Java 程序的入口，当我们要运行某个类时就需要在该类中定义主方法，主方法对于类并非都是必要的。
- **语法**  
```
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
```
class Person {  
    // 定义属性  
    String name;  
    int age;  
    
    // 构造方法  
    Person() {  
    }    Person(String name, int age) {  
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