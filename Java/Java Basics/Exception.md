## 异常
异常就是程序在运行过程中出现的一些错误，通过面向对象的思想，把这些错误也用类来描述，那么一旦产生一个错误，即就是创建了某一个错误的对象，这个对象就是我们所说的异常对象。

## 异常类型
`RuntimeException`、`Error` 以及它们的子类都称为免检异（unchecked exception)。所有其他异常（编译时异常）都称为必检异常（checked exception), 意思是指编译器会强制程序员检査并通过 `try catch` 块处理它们，或者在方法头进行声明。
### 系统错误（Error）
系统錯误是Java虚拟机([[JVM]])抛出的，用 `Error` 类表示。`Error` 类描述的是内部系统错误。这样的错误很少发生。如果发生，除了通知用户以及尽量稳妥地终止程序外，几乎什么也不能做。
- **常见错误**
	1. OutOfMemoryError：内存耗尽。
	2. NoClassDefFoundError：无法加载某个Class。
	3. StackOverflowError：栈溢出。
### 编译时异常（Exception）
编译时异常是 `Exception` 及其子类(除了 `RuntimeException` )，在编译时期抛出的异常，在编译期间检查程序是否可能会出现问题，如果可能会有，则预先防范：捕获声明。
- **常见错误**
	1. FileNotFoundException：未找到文件。
	2. IOException：输入输出操作期间可能发生的错误或异常情况。
### 运行时异常（RuntimeException）
运行时异常是用 `RuntimeException` 类表示的，它描述的是程序设计错误，例如，错误的类型转换、访问一个越界数组或数值错误。
`RuntimeException` 是那些可能在Java虚拟机正常运行期间抛出的异常的超类，可能在执行方法期间抛出但未被捕获的 `RuntimeException` 的任何子类都无需在 `throws` 子句中进行声明，指的就是这些问题不需要提前被预防（本质上也可以的，只不过没必要），因为只有在真正运行的时候才能发现是否发生问题，一旦在运行期间发生了问题，则一般不会修正，程序直接终端。
- **常见错误**
	1. ArithmeticException：一个整数除以0。	
	2. NullPointerException：对某个 `null` 的对象调用方法或字段。
	3. ArrayIndexOutOfBoundsException：数组索引越界。

## 处理编译时异常
### 声明异常
在Java中，当前执行的语句必属于某个方法。Java解释器调用 `main` 方法开始执行一个程序。每个方法都必须声明它可能抛出的必检异常的类型，这称为声明异常，只对编译时异常进行声明，告知方法的调用者有异常。
为了在方法中声明一个异常，就要在方法头中使用关键字 `throws` ，如果方法可能会抛出多个异常，就可以在关键字 `throws` 后添加一个用逗号分隔的异常列表。
- **示例**
```java
public void myMethodO throws Exceptionl, Exception2, …, ExceptionN
```
### 抛出异常
检测到错误的程序可以创建一个合适的异常类型的实例并抛出它，这就称为抛出一个异常。
声明异常的关楗字是 `throws` ，抛出异常的关键字是 `throw` 。
- **示例**
```java
// 发现传递给方法的参数与方法的合约不符,创建 IllegalArgumentException 的一个实例并抛出它
throw new IllegalArgumentException("Wrong Argument");
```
### 捕获异常
当抛出一个异常时，可以在 `try catch` 块中捕获和处理它。
**try语句块中**放的是可能出现问题的代码。
**catch语句块中**：放的是出现问题并捕获后，处理问题的代码code，如果问题在try语句块中没有出现 则catch中不会运行。
**finally语句块中**：放的是不管问题异常是否产生 都要执行的代码code。
- **示例**
```java
try {
    codeA
    throw ...
    codeB
} catch(Exception e) { 
	code 
} finally { 
	code//关闭资源（IO 数据库 网络），结尾处理的一些工作 
}
```