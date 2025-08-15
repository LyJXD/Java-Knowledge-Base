## 输入输出流
输入流(Input Stream)与输出流(Output Stream)合称为数据流(Data Stream)。
输入输出流的来源和接收者可以是文件、内存、网络连接等。
 
写入数据的原理：Java程序→JVM→OS→OS调用写入数据的方法→写入成功→手动释放OS资源。

读取数据的原理：Java程序→JVM→OS→OS调用读取数据的方法→读取成功→手动释放OS资源。

## File类
java.io.File类是文件和目录路径名称的抽象表示，主要用于文件和目录的创建、查找和删除等操作。
- **特点**
	1. 一个FIle代表的是硬盘中的一个路径或者一个文件
	2. 无论该路径下是否存在文件或目录，都不影响File对象的创建
### 创建
- **构造方法**
	1. public File(String pathname)：通过将给定的路径名 字符串转换为抽象类路径 来创建新的实例
	2. public File(String parent,String child)：从父路径字符串 和 子路径字符串创建新的File实例
	3. public File(File parent,String child)：从父抽象路径名 和 子路径名字符串创建新的File实例
- **示例**
```java
        File file1 = new File("D:\\aaa\\a.txt");
        File file2 = new File("D:\\aaa","a.txt");
        File file3 = new File("a.txt");
        System.out.println(file1);
        System.out.println(file2);
        System.out.println(file3);
        
        System.out.println("=================================");
        // 关键File类对象表示"D:\aaa\bbb"文件夹路径
        File file4 = new File("D:\\aaa\\bbb");
        File file5 = new File("D:\\aaa","bbb");
        File file6 = new File("bb");
        System.out.println(file4);
        System.out.println(file5);
        System.out.println(file6);
        
        System.out.println("=================================");
        File file7 = new File("D:\\aaa\\abcdefg");
        System.out.println(file7);
```