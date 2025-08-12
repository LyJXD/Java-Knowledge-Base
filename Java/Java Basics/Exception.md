## 异常
异常就是程序在运行过程中出现的一些错误，通过面向对象的思想，把这些错误也用类来描述，那么一旦产生一个错误，即就是创建了某一个错误的对象，这个对象就是我们所说的异常对象。

## 异常类型
`RuntimeException`、`Error` 以及它们的子类都称为免检异（unchecked exception)。所有其他异常（编译时异常）都称为必检异常（checked exception), 意思是指编译器会强制程序员检査并通过 `try catch` 块处理它们，或者在方法头进行声明。
### 系统错误（Error）
系统錯误是Java虚拟机([[JVM]])抛出的，用 `Error` 类表示。`Error` 类描述的是内部系统错误。这样的错误很少发生。如果发生，除了通知用户以及尽量稳妥地终止程序外，几乎什么也不能做。
- **常见错误**
	1. OutOfMemoryError ：内存耗尽。
	2. NoClassDefFoundError ：无法加载某个Class。
	3. StackOverflowError ：栈溢出。
### 编译时异常（Exception）
编译时异常是 `Exception` 及其子类(除了 `RuntimeException` )，在编译时期抛出的异常，在编译期间检查程序是否可能会出现问题，如果可能会有，则预先防范：捕获声明。
### 运行时异常（RuntimeException）
运行时异常是用 `RuntimeException` 类表示的，它描述的是程序设计错误，例如，错误的类型转换、访问一个越界数组或数值错误。运行时异常通常是由Java虚拟机抛出的。