## 字符串
在Java中字符串属于对象，Java提供了String类来创建和操作字符串。
### 创建
- **字面量方式**  
```
String s1 = "hello";
String s2 = "hello";
System.out.println(s1 == s2); // true，共享常量池
```
- **使用new创建（不推荐）**  
```
String s3 = new String("hello");
System.out.println(s1 == s3); // false，创建两个对象：常量池中的 "hello" + 堆中新对象
```
- **使用拼接**
```
String s4 = "he" + "llo";     // 编译期常量，仍然在常量池中
String s5 = s1 + " world";    // 运行期拼接，生成新对象
```
### 实现原理
1. String类的成员变量value是一个数组，用来存储字符串的内容。
2. value数组由final关键字修饰，保证字符串的**不可变性**。
3. 在Java 9之前，value是char[]类型，每个字符占用2个字节；从Java 9开始，value改为byte[]类型，通过coder字段来标识编码方式（UTF-16或Compact Strings，即拉丁字符使用1个字节，其他字符使用2个字节），这样可以节省内存空间。
4. String类的构造方法和各种方法（如substring、concat等）在操作字符串时，并不会直接修改原有字符串的value数组内容，而是会**创建一个新的String对象**来存放操作后的结果。例如，当你对一个字符串调用substring方法时，它会根据指定的起始索引和结束索引，创建一个新的String对象，并将原字符串中对应范围的字符复制到新对象的value数组中。
### 字符串常量池
- **定义**  
	字符串常量池是Java虚拟机（[[JVM]]）中一个特殊的内存区域，用于存储字符串常量对象。它的主要目的是减少字符串对象的重复创建，节省内存空间。
### 字符串的内存存储