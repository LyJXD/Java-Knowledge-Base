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
String类的成员变量 value 是一个字符数组，用来存储字符串的内容。在 Java 9 之前，`value` 是 `char[]` 类型，每个字符占用 2 个字节；从 Java 9 开始，`value` 改为 `byte[]` 类型，通过 `coder` 字段来标识编码方式（UTF-16 或 Compact Strings，即拉丁字符使用 1 个字节，其他字符使用 2 个字节），这样可以节省内存空间。
`String` 类的构造方法和各种方法（如 `substring`、`concat` 等）在操作字符串时，并不会直接修改原有字符串的 `value` 数组内容，而是会创建一个新的 `String` 对象来存放操作后的结果。例如，当你对一个字符串调用 `substring` 方法时，它会根据指定的起始索引和结束索引，创建一个新的 `String` 对象，并将原字符串中对应范围的字符复制到新对象的 `value` 数组中。