## 输入输出流
输入流(Input Stream)与输出流(Output Stream)合称为数据流(Data Stream)。
输入输出流的来源和接收者可以是文件、内存、网络连接等。
 
写入数据的原理：Java程序→JVM→OS→OS调用写入数据的方法→写入成功→手动释放OS资源。

读取数据的原理：Java程序→JVM→OS→OS调用读取数据的方法→读取成功→手动释放OS资源。

## File类
java.io.File类是文件和目录路径名称的抽象表示，主要用于文件和目录的创建、查找和删除等操作。