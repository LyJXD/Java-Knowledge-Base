## 多态
多态是面向对象程序设计的三大特性之一，意思是同一个方法([[Method]])，在不同对象([[object（对象）]])上有不同表现。简单理解就是：一个父类引用可以指向多个子类对象，调用方法时会根据实际对象类型执行对应的方法。
### 编译时多态（静态多态）
- **实现条件**  
	编译时多态通过[[Method#方法的重载]]实现，在编译阶段就确定调用哪个方法。
- **示例**
```java
 public class Test {
    public void sayHello(String name) {
        System.out.println("Hello " + name);
    }
    
    public void sayHello(int times) {
        System.out.println("Hello x" + times);
    }
}
```
### 运行时多态（动态多态）
- **定义**  
	父类引用调用子类重写的方法，在运行时决定调用哪一个。
- **实现条件**  
	1. **继承关系** 存在继承([[Inheritance]])关系的类之间才能够使用多态性。多态性通常通过一个父类用变量引用子类对象来实现。
	2. **方法重写** 子类必须[[Inheritance#重写]]父类的方法。通过在子类中重新定义和实现父类的方法，可以根据子类的特点行为改变这个方法的行为，如猫和狗吃东西的独特行为。
	3. **父类引用指向子类对象** 使用父类的引用变量来引用子类对象。这样可以实现对不同类型的对象的统一操作，而具体调用哪个子类的方法会在运行时多态决定。
- **示例**
```java
class Animal {
    public void sound() {
        System.out.println("动物发出声音");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("狗叫：汪汪汪");
    }
}

class Cat extends Animal {
    @Override
    public void sound() {
        System.out.println("猫叫：喵喵喵");
    }
}

// 测试运行时多态
public class OverrideExample {
    public static void main(String[] args) {
        Animal animal; // 父类引用
        
        animal = new Dog();
        animal.sound(); // 输出：狗叫：汪汪汪
        
        animal = new Cat();
        animal.sound(); // 输出：猫叫：喵喵喵
    }
}
```
### 转型
- **向上转型**  
	1. 向上转型(Upcasting)是指将一个子类的对象引用赋值给其父类类型的引用变量。这是在面向对象编程中的一种常见操作，用于实现多态性和灵活的对象处理。
	2. 子类对象可以隐式地转型为父类对象，不需要任何显式的类型转换操作。
	3. 父类引用变量可以引用子类对象，但通过父类引用变量只能访问到子类对象中定义的父类成员，无法访问子类独有的成员。
	4. 子类对象中重写的方法，在通过父类引用变量调用时，会调用子类中的实现（动态多态）。
	5. 向上转型是安全的操作，因为子类对象本身就是一个父类对象。
- **向下转型**  
	1. 向下转型(Downcasting)是指将一个父类类型的引用变量转换为其子类类型的引用变量。它与向上转型相反，需要进行显式的类型转换操作。
	2. 在某些情况下，当一个对象被向上转型后，它的具体类型信息会丢失，只保留了父类类型的信息。如果我们需要访问子类中特有的成员或调用子类重写的方法，就需要使用向下转型。
	3. 向下转型是有风险的，因为转换的对象必须是实际上是子类对象才能成功，否则会在运行时抛出 `ClassCastException` 异常。因此，在进行向下转型之前，应该使用 `instanceof` 运算符进行类型检查，以避免出现异常情况。
- **示例**
```java
class Animal {
    public void eat() {
        System.out.println("Animal is eating.");
    }
}

class Dog extends Animal {
    @Override
    public void eat() {
        System.out.println("Dog is eating.");
    }
    
    public void bark() {
        System.out.println("Dog is barking.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();  // 向上转型
        animal.eat();      // 调用的是 Dog 类中的 eat() 方法
        // animal.bark();  // ❌ 报错：无法访问 Dog 类中独有的方法
        
        // 使用向下转型之前，需要先检查对象是否实际上是子类的实例
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;  // 向下转型
            dog.bark();  // 调用 Dog 类中的 bark() 方法
        } else {
            System.out.println("animal is not an instance of Dog");
        }
    }
}
```
### 多态的优缺点
- **优点**  
	1. **灵活性和可扩展性** 多态性使得代码具有更高的灵活性和可扩展性。通过使用父类类型的引用变量，可以以统一的方式处理不同类型的对象，无需针对每个具体的子类编写特定的代码。
	2. **代码复用** 多态性可以促进代码的复用。可以将通用的操作定义在父类中，然后由子类继承并重写这些操作。这样一来，多个子类可以共享相同的代码逻辑，减少了重复编写代码的工作量。
	3. **可替换性** 多态性允许将一个对象替换为其子类的对象，而不会影响程序的其他部分。这种可替换性使得系统更加灵活和可维护，可以方便地添加新的子类或修改现有的子类，而无需修改使用父类的代码。
	4. **代码扩展性** 通过引入新的子类，可以扩展现有的代码功能，而无需修改现有的代码。这种可扩展性使得系统在需求变化时更加容易适应和扩展。
- **缺点**  
	1. **运行时性能损失** 多态性需要在运行时进行方法的动态绑定，这会带来一定的性能损失。相比于直接调用具体的子类方法，多态性需要在运行时确定要调用的方法，导致额外的开销。
	2. **代码可读性下降** 多态性使得代码的行为变得更加动态和不确定。在某些情况下，可能需要跟踪代码中使用的对象类型和具体的方法实现，这可能降低代码的可读性和理解性。
	3. **限制访问子类特有成员** 通过父类类型的引用变量，只能访问父类及其继承的成员，无法直接访问子类特有的成员。如果需要访问子类特有的成员，就需要进行向下转型操作，这增加了代码的复杂性和维护的难度。