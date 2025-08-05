## 工厂模式
- **核心本质**  
	实例化对象不使用new，用工厂方法创建对象。
	使用工厂统一管理对象的创建，将调用者跟实现类解耦。

## 简单工厂
建立一个工厂类，对实现了同一接口的一些类进行实例的创建。
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


```
## 工厂方法

## 抽象工厂