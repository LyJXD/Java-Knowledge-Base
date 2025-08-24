## 多线程
- **进程**
	进程是资源分配的最小单位。每个进程都有独立的代码和数据空间（进程上下文），进程间的切换会有较大的开销，一个进程包含1--n个线程。
- **线程**
	线程是操作系统中能够进行运算调度的最小单位。一类线程共享代码和数据空间，每个线程有独立的运行栈和程序计数器，线程切换开销小。线程被包含在进程之中，是进程中的实际运作单位。一个进程中可以并发多个线程，每条线程并行执行不同的任务。
- **并行**
	有点类似使用多块CPU来一起工作，它不会分时间片调度，是真真正正的同时工作。
- **并发**
	多线程就是并发的例子，一块CPU调度时会分为好多个时间片，每个时间片内调度一个线程，这样可以提高CPU的利用率，因为对于像IO操作这种，CPU调度了知乎，IO操作便干活，但是CPU却闲下来了，为了提高CPU利用率，可以让它再去干别的活。只不过由于这个时间片很短，所以看起来每个线程就跟同时工作一样。
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