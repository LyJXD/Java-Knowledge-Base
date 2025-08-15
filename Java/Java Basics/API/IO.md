## 输入输出流
输入流(Input Stream)与输出流(Output Stream)合称为数据流(Data Stream)。
输入输出流的来源和接收者可以是文件、内存、网络连接等。
**写入数据的原理** Java程序→JVM→OS→OS调用写入数据的方法→写入成功→手动释放OS资源。
**读取数据的原理** Java程序→JVM→OS→OS调用读取数据的方法→读取成功→手动释放OS资源。
## File类
`java.io.File` 类是文件和目录路径名称的抽象表示，主要用于文件和目录的创建、查找和删除等操作。
- **特点**
	1. 一个 `FIle` 代表的是硬盘中的一个路径或者一个文件。
	2. 无论该路径下是否存在文件或目录，都不影响 `File` 对象的创建。
### 创建
- **构造方法**
	1. `public File(String pathname)` 通过指定文件路径名来创建 `File` 对象。
	2. `public File(String parent, String child)` 通过指定父路径和子路径来创建 `File` 对象。
	3. `public File(File parent, String child)` 通过指定父 `File` 对象和子路径来创建 `File` 对象。
- **示例**
```java
// 绝对路径  
File file01 = new File("E:\\Work Files\\Dev\\Java\\Learning Projects\\JavaSE_Advance\\day11\\lib");  

// 相对路径  
File file02 = new File("day11\\lib");  

File file03 = new File("E:\\Work Files\\Dev\\Java\\Learning Projects\\JavaSE_Advance\\day11\\" + "lib");  
  
File file04 = new File(file03 + "test.txt");  
```
