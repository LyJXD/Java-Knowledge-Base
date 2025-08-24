## 多线程
## 生命周期

## 创建线程
### 继承Thread类
- **示例**
```java
public class Test extends Thread{
    @Override
    public void run() {
        System.out.println("Thread is Created");
    }
    public static void main(String[] args) {
        Test test = new Test();
        Thread thread = new Thread(test);
        thread.start();
        System.out.println(Thread.currentThread().getName());
    }
}
```
### 实现Runnable接口
- **示例**
```java
public class Test implements Runnable{
    @Override
    public void run() {
        System.out.println("Thread is Created");
    }
    public static void main(String[] args) {
        Test test = new Test();
        Thread thread = new Thread(test);
        thread.start();
        System.out.println(Thread.currentThread().getName());
    }
}
```
### 实现Callable接口
无论实现Runnable接口，还是继承Thread类，都存在一些缺陷，我们无法获得线程的执行结果，无法处理执行过程的异常。
Callable是JDK 1.5新增的接口，Callable接口里面定义了 `call()` 方法，`call()` 方法是 `run()` 方法的增强版，可以通过实现Callable接口时传入泛型来指定 `call()` 方法的返回值，并且可以声明抛出异常。
- **实现步骤**
	1. 创建线程类实现Callable接口，重写 `call()` 方法。
	2. 创建FutureTask实例，将实现Callable接口的线程类实例化对象作为FutureTask的target。
	3. 创建Thread类，将FutureTask实例化对象作为Thread的target。
- **示例**
```java
public class Test implements Callable<String> {
    @Override
    public String call() throws Exception {
        System.out.println("Thread is Created");
        return "OK";
    }
    
    public static void main(String[] args) throws Exception {
        Test test = new Test();
        FutureTask futureTask = new FutureTask(test);
        Thread thread = new Thread(futureTask);
        thread.start();
        String str = (String) futureTask.get(5,TimeUnit.SECONDS);
        System.out.println(str);
        System.out.println(Thread.currentThread().getName());
    }
}
```

## 线程池