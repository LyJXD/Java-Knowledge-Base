## 封装
封装是指一种将抽象性函式接口的实现细节部分包装、隐藏起来的方法。
封装可以被认为是一个保护屏障，防止该类的代码和数据被外部类定义的代码随机访问。
要访问该类的代码和数据，必须通过严格的接口控制。
封装最主要的功能在于我们能修改自己的实现代码，而不用修改那些调用我们代码的程序片段。
### 实现
```java
public class Person{
    private String name;
    private int age;
    ​
    public int getAge(){
      return age;
    }
    ​
    public String getName(){
      return name;
    }
    ​
    public void setAge(int age){
      this.age = age;
    }
    ​
    public void setName(String name){
      this.name = name;
    }
}
```
- **修改属性可见性**
	这段代码中，将 `name` 和 `age` 属性设置为私有的，只能本类才能访问，其他类都访问不了，如此就对信息进行了隐藏。
- **公共方法**  
	为私有属性创建一对公共的赋取值方法，用于其他类访问私有属性。
- **优点**  
	1. 良好的封装能够减少耦合。
	2. 类内部的结构可以自由修改。
	3. 可以对成员变量进行更精确的控制。
	4. 隐藏信息，实现细节。
	5. 适当的封装可以让代码更容易理解与维护，也加强了代码的安全性。