## 工厂模式
- **核心本质**  
	实例化对象不使用new，用工厂方法创建对象。
	使用工厂统一管理对象的创建，将调用者跟实现类解耦。

## 简单工厂
简单工厂模式的核心是定义一个创建对象的接口，将对象的创建和本身的业务逻辑分离，降低系统的耦合度，使得两个修改起来相对容易些，当以后实现改变时，只需要修改工厂类即可。
![[简单工厂.png]]
- **示例**
```java
// 手机接口类
public interface Phone {
    public void call();
}

// 手机实现类
public class IPhone implements Phone{
    @Override
    public void call() {
        System.out.println("用苹果手机打电话！");
    }
}
public class MPhone implements Phone{
    @Override
    public void call() {
        System.out.println("用小米手机打电话！");
    }
}

// 工厂类
public class PhoneFactory {
    public Phone create(String type){
        if (type.equals("IPhone")){
            return new IPhone();
        }else if (type.equals("MPhone")){
            return new MPhone();
        }else
            return null;
    }
}

public class Test {
    public static final String IPhone = "IPhone";
    
    public static final String MPhone = "MPhone";
    
    public static void main(String[] args) {
		// 生产手机  
		PhoneFactory factory = new PhoneFactory();  
		factory.create(MPhone).call();  
		factory.create(IPhone).call();
    }
}
```
- **优点**  
	客户端不需要知道创建对象的具体类，只需知道工厂类和产品类的接口即可。
- **缺点**  
	工厂类的职责过重，增加新的产品时需要修改工厂类，违反了开闭原则。

## 工厂方法
工厂方法将工厂抽象化，并定义一个创建对象的接口。每增加新产品，只需增加该产品以及对应的具体实现工厂类，由具体工厂类决定要实例化的产品是哪个，将对象的创建与实例化延迟到子类。
![[工厂方法.png]]
- **示例**
```java
// 手机类略

// 工厂接口
public interface PhoneFactory {
    public Phone create();
}

// 小米手机工厂
public class MPhoneFactory implements PhoneFactory{
    @Override
    public Phone create() {
        return new MPhone();
    }
}
// 苹果手机工厂
public class IPhoneFactory implements PhoneFactory{
    @Override
    public Phone create() {
        return new IPhone();
    }
}

// 测试类
public class Test {
    public static void main(String[] args) {
        // 生产小米手机
        PhoneFactory factory1 = new MPhoneFactory();
        factory1.create().call();
        // 生产苹果手机
        PhoneFactory factory2 = new IPhoneFactory();
        factory2.create().call();
    }
}
```
- **优点**  
	遵循开闭原则，可以在不修改现有代码的情况下添加新产品。
- **缺点**  
	增加了系统的复杂性，需要为每个产品创建一个工厂类。

## 抽象工厂
抽象工厂将工厂抽象成两层，抽象工厂和具体实现的工厂子类。程序员可以根据创建对象类型使用对应的工厂子类。这样将单个的简单工厂类变成了工厂集合，更利于代码的维护和扩展。
![[抽象工厂.png]]
- **示例**
```java
// 手机、电脑类略

// 超级工厂
public interface Factory {
    public Phone createPhone();
    public Book createBook();
}

// 苹果工厂
public class AppleFactory implements Factory{
    @Override
    public Phone createPhone() {
        return new IPhone();
    }
    
    @Override
    public Book createBook() {
        return new MacBook();
    }
}
// 小米工厂
public class XiaoMiFactory implements Factory{
    @Override
    public Phone createPhone() {
        return new MPhone();
    }
    
    @Override
    public Book createBook() {
        return new MiBook();
    }
}

// 测试类
public class Test {
    public static void main(String[] args) {
        // 实例化苹果工厂，生产苹果手机和电脑
        Factory factory = new AppleFactory();
        factory.createBook().play();
        factory.createPhone().call();
        // 实例化小米工厂，生产小米手机和电脑
        Factory factory1 = new XiaoMiFactory();
        factory1.createBook().play();
        factory1.createPhone().call();
    }
}
```
- **优点**  
	1. 分离了具体类的生成，符合开闭原则。
	2. 提供了一个一致的产品族创建方式。
- **缺点**  
	- 增加了系统的抽象性和复杂性。