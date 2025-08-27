## 多线程
### 基础概念
- **进程**  
	进程是资源分配的最小单位。每个进程都有独立的代码和数据空间（进程上下文），进程间的切换会有较大的开销，一个进程包含1--n个线程。
- **线程**  
	线程是操作系统中能够进行运算调度的最小单位。一类线程共享代码和数据空间，每个线程有独立的运行栈和程序计数器，线程切换开销小。线程被包含在进程之中，是进程中的实际运作单位。一个进程中可以并发多个线程，每条线程并行执行不同的任务。
- **并行**  
	多个任务真正同时执行，需要硬件支持（如多核CPU、分布式系统）。
	适合**计算密集型任务**。
- **并发**  
	多个任务交替执行，通过时间片轮转或事件驱动实现“看似同时”的效果。
	适合**I/O密集型任务**。

## 线程的生命周期
![[线程生命周期.png]]
### NEW（新建）
- **定义**  
    线程对象被创建但尚未启动。
- **触发条件**  
    通过 `new Thread()`​ 创建线程对象，但未调用 `start()`​ 方法。
- **特点**：
    1. 线程未与操作系统线程关联，仅是一个Java对象实例。
    2. 无法执行任何代码，直到调用 `start()`​。
### RUNNABLE（可运行）
- **定义**  
    线程已启动，等待CPU调度运行。
- **触发条件**  
    调用 `start()`​ 方法后。
- **特点**
	包含两种子状态：就绪和运行。
	1. **就绪（Ready）** 线程准备运行，等待CPU时间片分配。
	2. **运行（Running）** 线程获得CPU时间片，正在执行代码。
### BLOCKED（阻塞）
- **定义**  
    线程因等待锁而被阻塞。
- **触发条件**  
    尝试获取一个被其他线程持有的锁（如 `synchronized` ​锁）。
- **特点**  
    需等待锁释放后，线程才能重新进入RUNNABLE状态。
### WAITING（等待）
- **定义**  
    线程主动进入无限期等待，需其他线程显式唤醒。
- **触发条件**  
	调用 `Object.wait()`​、`Thread.join()`​ 或 `LockSupport.park()`​。
- **特点**  
    需通过 `notify()`​、`notifyAll()`​ 或 `interrupt()`​唤醒。
### TIMED_WAITING（计时等待）
- **定义**  
    线程进入有限期等待，超时后自动恢复。
- **触发条件**  
    调用 `Thread.sleep(long millis)`​、`Object.wait(long timeout)`、`Thread.join(long millis)` ​等带超时参数的方法。
- **特点**  
    超时后自动返回RUNNABLE状态，或被其他线程唤醒。
### TERMINATED（终止）
- **定义**  
    线程运行结束或因异常退出。
- **触发条件**  
    1. `run()`​方法执行完毕。
	2. 线程因未捕获异常终止。
- **特点**  
    终止后不可再次启动。

## 使用线程
### 创建线程
- **继承Thread类**
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
- **实现Runnable接口**
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
- **实现Callable接口**  
	无论实现Runnable接口，还是继承Thread类，都存在一些缺陷，我们无法获得线程的执行结果，无法处理执行过程的异常。  
	Callable是JDK 1.5新增的接口，Callable接口里面定义了 `call()` 方法，`call()` 方法是 `run()` 方法的增强版，可以通过实现Callable接口时传入泛型来指定 `call()` 方法的返回值，并且可以声明抛出异常。  
	- **实现步骤**  
		1. 创建一个实现Callable的实现类。
		2. 实现call方法,将操作声明在 `call()` 方法中。
		3. 创建Callable实现类的对象。
		4. 将此实现类的对象作为参数传递到FutureTask构造器，创建FutureTask对象。
		5. 将FutureTask的对象作为参数传递到Thread类的构造器中，创建Thread对象。
```java
public class Test implements Callable<String> {
    @Override
    public String call() throws Exception {
        System.out.println("Thread is Created");
        return "OK";
    }0.
    public static void main(String[] args) throws Exception {
        Test test = new Test();
        FutureTask futureTask = new FutureTask(test);
        Thread thread = new Thread(futureTask);
        thread.start();
        // 调用FutureTask对象的 get() 方法来获得子线程执行结束后的返回值。
        String str = (String) futureTask.get(5,TimeUnit.SECONDS);
        System.out.println(str);
        System.out.println(Thread.currentThread().getName());
    }
} 
```
### 常用方法
- **`currentThread()`**  
	静态方法，返回当前代码的线程。
- **`getName()`**  
	获得当先线程的名字。
- **`setName()`**  
	设置当前线程的名字。
- **`yield()`**  
	释放当前cpu的执行权。
- **`join()`**  
	在线程a中调用线程b的 `join()`，则线程a进入阻塞状态，等线程b结束后结束阻塞状态。
- **`sleep（Long militime）`**  
	让当前线程阻断指定的militime毫秒，此时为阻塞状态。
- **`isAlive()`**  
	判断线程是否存活。
```java
class mythresd extends Thread{
    @Override
    public void run() {
        for(int i = 0;i<=100;i++){
            try {
                    sleep(100); //阻断100毫秒
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+" "+i); //输出线程名
            }
        }
    }
}

public class Test {
    public static void main(String[] args) {
        mythresd mythresd = new mythresd();
        mythresd.setName("线程一"); //设置线程名
        mythresd.start();
        
        Thread.currentThread().setName("主线程");
        for(int i = 0;i<=100;i++){
            if(i%2==0){   
                if(i==20){
                    mythresd.join(); //阻断主线程
                } 
                System.out.println(Thread.currentThread().getName()+" "+i);
            }
        }
        //判断mythread线程是否还存活
        System.out.println(mythresd.isAlive());
    }
}
```

## 线程安全

## 线程池
![[线程池.png]]