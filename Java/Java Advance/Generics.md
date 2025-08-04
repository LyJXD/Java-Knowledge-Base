## 泛型
泛型，即“参数化类型”，也就是说在泛型使用过程中，数据类型被设置为一个参数，在使用时再从外部传入一个数据类型；而一旦传入了具体的数据类型后，传入变量（实参）的数据类型如果不匹配，编译器就会直接报错。
- **特点**  
	1. 与使用 Object 对象代替一切引用数据类型对象这样简单粗暴方式相比，泛型使得数据类型的类别可以像参数一样由外部传递进来。它提供了一种扩展能力，更符合面向对象开发的软件编程宗旨。
	2. 当具体的数据类型确定后，泛型又提供了一种类型安全检测机制，只有数据类型相匹配的变量才能正常的赋值，否则编译器就不通过。所以说，泛型一定程度上提高了软件的安全性，防止出现低级的失误。
	3. 泛型提高了程序代码的可读性。在定义泛型阶段（类、接口、方法）或者对象实例化阶段，由于 <类型参数> 需要在代码中显式地编写，所以程序员能够快速猜测出代码所要操作的数据类型，提高了代码可读性。
### 泛型类
- **定义**  
	类型参数用于类的定义中，则该类被称为泛型类。通过泛型可以完成对一组类的操作对外开放相同的接口。最典型的就是各种容器类，如：List、Set、Map等。
- **类型参数定义位置**  
	1. 非静态的成员属性类型。
	2. 非静态方法的形参类型（包括非静态成员方法和构造器）。
	3. 非静态的成员方法的返回值类型。
- **特点** 
	1. 静态方法和静态变量不可以使用泛型类所声明的类型参数，因为**泛型类中的类型参数的确定是在创建泛型类对象的时候**，而静态变量和静态方法在类加载时已经初始化，直接使用类名调用。在泛型类的类型参数未确定时，静态成员有可能被调用，因此泛型类的类型参数是不能在静态成员中使用的。
	2. 静态泛型方法中可以使用自身的方法签名中新定义的类型参数（即泛型方法），而不能使用泛型类中定义的类型参数。
	3. 泛型类不只接受一个类型参数，它还可以接受多个类型参数。
	4. 在创建泛型类的对象时，必须指定类型参数 `T` 的具体数据类型，即尖括号中传入的什么数据类型，`T` 便会被替换成对应的类型。如果尖括号中什么都不传入，则默认是 `<Object>`。
- **语法**  
```java
class 类名称 <泛型标识> {
  private 泛型标识 变量名; 
  .....

  }
}
```
- **示例**  
```java
public class Generic<T> { 
    // key 这个成员变量的数据类型为 T, T 的类型由外部传入  
    private T key;
    
	// 泛型构造方法形参 key 的类型也为 T，T 的类型由外部传入
    public Generic(T key) { 
        this.key = key;
    }
    
	// 泛型方法 getKey 的返回值类型为 T，T 的类型由外部指定
    public T getKey(){ 
        return key;
    }
}

// 当创建一个 Generic<T> 类对象时，会向尖括号 <> 中传入具体的数据类型。
public void Test() {
	// 传入 String 类型
	Generic<String> generic = new Generic<>();
	
	// <> 中什么都不传入，等价于 Generic<Object> generic = new Generic<>();
	Generic generic = new Generic();
}
```
### 泛型接口
- **特点**  
	1. 泛型接口中的类型参数，在该接口被继承或者被实现时确定。
- **语法**
```java
public interface 接口名<类型参数> {
    ...
}
```
- **示例**
```
public interface Inter<T> {
    public abstract void show(T t) ;
}
```
### 泛型方法
当在一个方法签名中的返回值前面声明了一个 `<T>` 时，该方法就被声明为一个泛型方法。`<T>`表明该方法声明了一个类型参数T，并且这个类型参数T只能在该方法中使用。
- **特点**  
	1. 只有在方法签名中声明了 `<T>` 的方法才是泛型方法，仅使用了泛型类定义的类型参数的方法并不是泛型方法。
	2. 泛型方法中可以同时声明多个类型参数。
	3. 泛型方法中也可以使用泛型类中定义的泛型参数，且泛型类中定义的类型参数和泛型方法中定义的类型参数是相互独立的，它们一点关系都没有。
- **语法**
```java
public <类型参数> 返回类型 方法名（类型参数 变量名） {
    ...
}
```
- **示例**
```java
public class Test<U> {
	// 该方法只是使用了泛型类定义的类型参数，不是泛型方法
	public static void testMethod(U u){
		System.out.println(u);
	}
	
	// <T> 真正声明了下面的方法是一个泛型方法
    public static <T> T getData(T data)  
    {  
        return data;  
    }  
    
    public static void main(String[] args) {  
        String str = Demo.getData("hello");  
        int num = Demo.getData(100);  
    }  
}
```
### 泛型通配符
- **无界通配符**
	
- **上界通配符**
	上界通配符，存在一个最上级的界限，即指定一个最高级别的父类，它表示对于该上界类型以及其子类都适用。
- **下界通配符**
	下界通配符，存在一个最低级的界限，即指定一个最低级别的子类，它表示对于该下界类型以及其父类都适用。
- **示例**
```java
public class Wildcards {  
    public static void main(String[] args) {  
        ArrayList<Machine> machineList = new ArrayList<Machine>();  
        ArrayList<Car> carList = new ArrayList<Car>();  
        ArrayList<BENZ> benzList = new ArrayList<BENZ>();  
        ArrayList<BMW> bmwList = new ArrayList<BMW>();  
  
        test(machineList);  
        test(carList);  
        test(benzList);  
        test(bmwList);  
  
        test1(machineList); // ❌ 报错  
        test1(carList);  
        test1(benzList);  
        test1(bmwList);  
  
        test2(machineList);  
        test2(carList);  
        test2(benzList);    // ❌ 报错  
        test2(bmwList);     // ❌ 报错  
    }  
  
    public static void test(ArrayList<?> list)  
    {  
        System.out.println("无界通配符");  
    }  
  
    public static void test1(ArrayList<? extends Car> list)  
    {  
        System.out.println("上界通配符");  
    }  
  
    public static void test2(ArrayList<? super Car> list)  
    {  
        System.out.println("下界通配符");  
    }  
}  
  
class Machine{}  
class Car extends Machine{}  
class BENZ extends Car{}  
class BMW extends Car{}
```