## 字符串
在Java中字符串属于对象，Java提供了String类来创建和操作字符串。
### 创建
- **字面量方式**  
```java
String s1 = "hello";
String s2 = "hello";
System.out.println(s1 == s2); // true，共享常量池
```
- **使用new创建（不推荐）**  
```java
String s3 = new String("hello");
System.out.println(s1 == s3); // false，创建两个对象：常量池中的 "hello" + 堆中新对象
```
- **使用拼接**
```java
String s4 = "he" + "llo";     // 编译期常量，仍然在常量池中
String s5 = s1 + " world";    // 运行期拼接，生成新对象
```
### 实现原理
```java
// String 实现源码（JDK21）
public final class String implements java.io.Serializable, Comparable<String>, Constable,ConstantDesc{
	@Stable
	private final byte[] value;
	...
}
```
1. String类的成员变量value是一个数组，用来存储字符串的内容。
2. value数组由final关键字修饰，保证字符串的**不可变性**。
3. 在Java 9之前，value是char[]类型，每个字符占用2个字节；从Java 9开始，value改为byte[]类型，通过coder字段来标识编码方式（UTF-16或Compact Strings，即拉丁字符使用1个字节，其他字符使用2个字节），这样可以节省内存空间。
4. String类的构造方法和各种方法（如 `substring()` 、`concat()` 等）在操作字符串时，并不会直接修改原有字符串的value数组内容，而是会**创建一个新的String对象**来存放操作后的结果。例如，当你对一个字符串调用 `substring()` 方法时，它会根据指定的起始索引和结束索引，创建一个新的String对象，并将原字符串中对应范围的字符复制到新对象的value数组中。
### 字符串常量池
- **定义**  
	字符串常量池是Java虚拟机（[[JVM]]）中一个特殊的内存区域，用于存储字符串常量对象。它的主要目的是减少字符串对象的重复创建，节省内存空间。JDK6的版本，常量池在持久代中分配；JDK7及以上的版本，常量池在堆内存中分配；
- **存储内容**  
	字符串常量池中存储的是通过双引号声明的字符串常量（如 `"hello"` ），以及通过String类的 `intern()` 方法被手动添加到常量池的字符串。
* **工作原理**    
	1. 当程序中出现字符串常量时（如 `String str = "hello";` ），JVM会先在字符串常量池中查找是否存在内容相同的字符串对象。如果存在，就直接将 `str` 指向常量池中的那个对象；如果不存在，JVM会创建一个新的字符串对象，并将其放入常量池中，然后让 `str` 指向这个新对象。  
	2. 对于通过 `new String()` 创建的字符串对象，它们默认不会被放入字符串常量池。但是，如果调用了 `intern()` 方法（如 `new String("hello").intern();`），JVM会检查字符串常量池中是否存在内容相同的字符串对象。如果存在，就返回常量池中的那个对象的引用；如果不存在，就会将当前字符串对象添加到常量池中，并返回其引用。
### 字符串的内存存储
- **使用双引号创建的字符串**
```java
String test = "ab";
```
字符串 `"ab"` 会直接出现在字符串常量池中。
![[string1.jpg]]
- **使用new创建的字符串**
```java
String test = new String("ab");
```
字符串 `"ab"` 同样会出现在字符串常量池中，同时在堆内存中也会分配一块空间存放test对象。
![[string2.jpg]]
- **拼接字符串**
```java
// 案例1
String test = "ab" + "cd";
// 字节码中实际变成如下代码
String test = "abcd";
```
 该案例`"ab"` 和 `"cd"` 都是字符串字面量（常量），编译器会在编译期间自动拼接成 `"abcd"`。
![[string3.jpg]]
 ```java
// 案例2
String ab = "ab";
String cd = "cd";
String test = ab + cd;
```
`"ab"` 和 `"cd"` 是变量（即使它们指向常量），编译器不能确定它们的值（可能是运行期变化的），所以无法在编译期拼接。编译器生成的是字符串连接操作，底层其实会变成：
```java
new StringBuilder().append(ab).append(cd).toString();
```
该案例 `"ab"` 和 `"cd"` 是常量字面量，仍会进入字符串常量池。
拼接生成的新字符串 `"abcd"` 是运行时创建的，存在**堆内存中**，不会自动加入常量池。
![[string4.jpg]]