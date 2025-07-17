## 继承
### 概述
继承是面向对象的三大特征之一，可以使得子类具有父类的属性和方法，还可以在子类中重新定义，追加属性和方法。继承是指在原有类的基础上，进行功能扩展，创建新的类型。
- **特点**  
	1. 继承的本质是对某一批类的抽象，从而实现对现实世界更好的建模。
	2. Java中类只有单继承，没有多继承。
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
        //实例化对象
        Dog dog = new Dog();
        Cat cat = new Cat();
        
        dog.name = "大黄";
        dog.color = "黄色";
        dog.age = 3;
        dog.eat();
        dog.sleep();
        dog.bark();
        System.out.println("===========");
        
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