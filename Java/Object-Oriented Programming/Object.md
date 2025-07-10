## 对象
对象是类的实例，具有状态和行为。
例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
### 创建对象
对象是根据类创建的。在Java中，使用关键字new来创建一个新的对象。
创建对象需要以下三步：
- **声明**  
	声明一个对象，包括对象名称和对象类型。
- **实例化**  
	使用关键字new来创建一个对象。
- **初始化**  
	使用new创建对象时，会调用构造方法初始化对象。
- **示例**
```
public class Person {  
    public String name;  
    public int id;  
    public int age;  
    
    public Person(String name, int id, int age) {  
        this.name = name;  
        this.id = id;  
        this.age = age;   
    }   
}

public class TestPerson{
    public static void main(String[] args) {  
        Student student1 = new Student("张三", 1, 18);  
    }  
}
```
- **this关键字**  
	在Java中，当局部变量（比如方法的参数）和类的成员变量重名时，就会产生命名冲突。在这种情况下，如果直接使用变量名，Java默认会使用局部变量。而`this`关键字的一个重要作用就是用来引用当前对象的成员变量，从而区分局部变量和成员变量。
