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
### 相关方法
- **`sleep()`**  
	`sleep()` 是Thread类中的一个静态本地方法，通过设置方法中的时间参数，使调用它的线程休眠指定时间，线程从RUNNING状态转为BLOCKED状态，这个过程中会释放CPU资源，给其他线程运行机会时不考虑线程的优先级，但如果**有同步锁则 `sleep()` 不会释放锁**即其他线程无法获得同步锁，需要注意的是 `sleep()` 使用时要处理异常。休眠时间未到时，可通过调用 `interrupt()` 方法来唤醒休眠线程。
- **`wait()`**  
	`wait()` 是Object类的成员本地方法，**会让持有对象锁的线程释放锁**，进入线程等待池中等待被再次唤醒(`notify()` 随机唤醒，`notifyAll()` 全部唤醒，线程结束自动唤醒)，即放入锁池中竞争同步锁，同时释放CPU资源。它的调用必须在同步方法或同步代码块中执行，也需要捕获 `InterruptedException` 异常。
- **`join()`**  
	`join()` 同样是Thread类中的一个方法，调用 `join()` 的线程拥有**优先使用CPU时间片的权利**，其他线程需要等待 `join()` 调用的线程执行结束后才能继续执行。探索其底层会发现，它的底层是通过 `wait()` 进行实现，因此它也需要处理异常。
- **`yield()`**
	`yield()` 是Thread类中的一个静态方法，它的调用不需要传入时间参数，并且 `yield()` 方法只会**给相同优先级或更高优先级的线程运行的机会**，并且调用 `yield()` 的线程状态会转为就绪状态，调用 `yield()` 方法只是一个建议，告诉线程调度器我的工作已经做的差不多了，可以让别的线程使用CPU了，没有任何机制保证采纳。所以可能它刚让出CPU时间片，又被线程调度器分配了一个时间片继续执行了。使用时不需要处理异常。
- **方法对比**
	- **`sleep()` 对比 `wait()`**
		1. `sleep()` 是Thread类的静态本地方法；`wait()` 是Object类的成员本地方法。
		2. JDK1.8 后`sleep()` 和 `wait()` 均需要捕获 `InterruptedException` 异常。
		3. `sleep()` 可以在任何地方使用；`wait()` 则只能在同步方法或同步代码块中使用。
		4. `sleep()` 会休眠当前线程指定时间，释放CPU资源，不释放对象锁，休眠时间到自动苏醒继续执行；`wait()` 方法放弃持有的对象锁，进入等待队列，当该对象被调用 `notify()` 或 `notifyAll()` 方法后才有机会竞争获取对象锁，进入运行状态。
	- **`sleep()` 对比 `join()`**
		1. JDK1.8 `sleep()` 和 `join()` 均需要捕获 `InterruptedException` 异常。
		2. `sleep()` 是Thread的静态本地方法，`join()` 是Thread的普通方法。
		3. `sleep()` 不会释放锁资源，`join()` 底层是 `wait()` 方法，会释放锁。
	- **`sleep()` 对比 `yield()`**
		1. `sleep()` 给其他线程运行机会时不考虑线程的优先级；`yield()` 只会给相同优先级或更高优先级的线程运行的机会。
		2. `sleep()` 声明抛出 `InterruptedException`；`yield()` 没有声明抛出异常。
		3. 线程执行 `sleep()` 后进入超时等待状态；线程执行 `yield()` 转入就绪状态，可能马上又得得到执行。
		4. `sleep()` 需要指定时间参数；`yield()` 让出CPU的执行权时间由JVM控制。
- **常用方法示例**
```java
class mythresd extends Thread{
    @Override
    public void run() {
        for(int i = 0;i<=100;i++){
            try {
                    sleep(100); // 休眠100毫秒
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+" "+i); // 输出线程名
            }
        }
    }
}

public class Test {
    public static void main(String[] args) {
        mythresd mythresd = new mythresd();
        mythresd.setName("线程一"); // 设置线程名
        mythresd.start(); // 启动线程
        
        Thread.currentThread().setName("主线程");
        for(int i = 0;i<=100;i++){
            if(i%2==0){   
                if(i==20){
                    mythresd.join(); // 阻断主线程
                } 
                System.out.println(Thread.currentThread().getName()+" "+i);
            }
        }
        // 判断mythread线程是否还存活
        System.out.println(mythresd.isAlive());
    }
}
```

## 线程安全
线程安全并不是一个“非黑即白”单项选择题。按照“线程安全”的安全程度由强到弱来排序，我们可以将java语言中各种操作共享的数据分为以下5类：
**不可变**
在java语言中，不可变的对象一定是线程安全的，无论是对象的方法实现还是方法的调用者，都不需要再采取任何的线程安全保障措施。如final关键字修饰的数据不可修改，可靠性最高。
**绝对线程安全**
绝对的线程安全完全满足Brian GoetZ给出的线程安全的定义，这个定义其实是很严格的，一个类要达到“不管运行时环境如何，调用者都不需要任何额外的同步措施”通常需要付出很大的代价。
**相对线程安全**
相对线程安全就是我们通常意义上所讲的一个类是线程安全的。它需要保证对这个对象单独的操作是线程安全的，我们在调用的时候不需要做额外的保障措施，但是对于一些特定顺序的连续调用，就可能需要在调用端使用额外的同步手段来保证调用的正确性。
在java语言中，大部分的线程安全类都属于相对线程安全的，例如Vector、HashTable、Collections的 `synchronizedCollection()` 方法保证的集合。
**线程兼容**
线程兼容就是我们通常意义上所讲的一个类不是线程安全的。
线程兼容是指对象本身并不是线程安全的，但是可以通过在调用端正确地使用同步手段来保证对象在并发环境下可以安全地使用。Java API中大部分的类都是属于线程兼容的。如与前面的Vector和HashTable相对应的集合类ArrayList和HashMap等。
**线程对立**
线程对立是指无论调用端是否采取了同步错误，都无法在多线程环境中并发使用的代码。由于java语言天生就具有多线程特性，线程对立这种排斥多线程的代码是很少出现的。
一个线程对立的例子是Thread类的 `suspend()` 和 `resume()` 方法。如果有两个线程同时持有一个线程对象，一个尝试去中断线程，另一个尝试去恢复线程，如果并发进行的话，无论调用时是否进行了同步，目标线程都有死锁风险。正因如此，这两个方法已经被废弃。
### 多线程和数据安全性问题
在多线程编程中，多个线程可以同时访问和修改共享的数据。这种并发访问可能导致以下问题：
- **竞态条件（Race Condition）**  
	多个线程试图同时修改共享数据，导致数据不一致性。
- **死锁（Deadlock）**
	多个线程因为互相等待对方释放资源而陷入无限等待的状态。
- **数据损坏**  
	多个线程同时修改数据可能导致数据的损坏，使其不再可用或不正确。
- **性能问题**  
	不合理的同步策略可能导致程序的性能下降。
### synchronized
`synchronized` 是一种内置的 Java 关键字，它用于实现线程的同步。当一个线程进入`synchronized`块或方法时，它获得了锁，这会阻止其他线程同时进入相同的`synchronized`块或方法，从而确保了共享资源的互斥访问。
- **同步代码块**
### lock

## 线程池
![[线程池.png]]