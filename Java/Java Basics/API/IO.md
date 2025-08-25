## IO流
在Java IO中，流是一个非常重要的概念。可以把流想象成一条数据传输的通道，数据就像水流一样在这个通道中流动。它具有方向性，数据从数据源流向程序（输入流），或者从程序流向数据目的地（输出流）。并且，流中的数据是按顺序依次传输的，就像水流是依次流淌一样。数据在流中是以字节或者字符为单位进行传输的。例如，当从一个文本文件中读取数据时，数据会以字节或者字符的形式通过输入流进入程序；当向文件写入数据时，数据会以字节或字符的形式通过输出流从程序流向文件。
![[IO流.png]]
### 字节流
以字节（8 位）为单位处理数据，适用于处理任何类型的数据，包括二进制数据，如图片、音频、视频等 。`InputStream` 和 `OutputStream` 是字节流的抽象基类，它们的子类如`FileInputStream` `FileOutputStream` 等，广泛应用于各种字节数据的读写操作。
- **示例**
```java
try (InputStream inputStream = new FileInputStream("test.txt")) {
	byte[] buffer = new byte[1024];
	int length;
	while ((length = inputStream.read(buffer)) != -1) {
		for (int i = 0; i < length; i++) {
			System.out.print(buffer[i] + " ");
		}
	}
	
	// jdk11后新方法，一次读取所有字节  
	// 如果文件过大，创建的字节数组也会过大，可能会导致内存溢出  
	byte[] bytes = fis.readAllBytes();  
	System.out.println("读取到的长度" + bytes.length);  
	System.out.println(new String(bytes));
} catch (IOException e) {
	e.printStackTrace();
}
```
### 字符流
以字符（16位Unicode）为单位处理数据，主要用于处理文本数据。`Reader` 和 `Writer` 是字符流的抽象基类，其常见子类有 `FileReader` 、`FileWriter` 、`BufferedReader` 、`BufferedWriter`等。字符流在处理文本时，会自动进行字符编码转换，方便处理不同编码格式的文本文件。
- **示例**
```java
public class CharacterStreamExample {
    public static void main(String[] args) {
        try (Reader reader = new FileReader("text.txt");
            BufferedReader bufferedReader = new BufferedReader(reader)) {
            String line;
            while ((line = bufferedReader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## File类
`java.io.File` 类是文件和目录路径名称的抽象表示，主要用于文件和目录的创建、查找和删除等操作。
- **特点**
	1. 一个 `FIle` 代表的是硬盘中的一个路径或者一个文件。
	2. 无论该路径下是否存在文件或目录，都不影响 `File` 对象的创建。
- **构造方法**
	1. `public File(String pathname)` 通过指定文件路径名来创建 `File` 对象。
	2. `public File(String parent, String child)` 通过指定父路径和子路径来创建 `File` 对象。
	3. `public File(File parent, String child)` 通过指定父 `File` 对象和子路径来创建 `File` 对象。
- **示例**
```java
public class Demo {  
    public static void main(String[] args) {  
        // 绝对路径    
		File file01 = new File("E:\\Work Files\\Dev\\Java\\Learning Projects\\JavaSE_Advance\\day11\\lib");  
		
        // 相对路径    
		File file02 = new File("day11\\lib");  
		
        File file03 = new File("E:\\Work Files\\Dev\\Java\\Learning Projects\\JavaSE_Advance\\day11\\" + "lib");  
        
        File file04 = new File(file03 + "test.txt");  
        findFile("Demo.java", new File("day11"));  
        deleteFile(new File("lib"));  
    } 
     
    public static void findFile(String fileName, File file){  
	    // 获取当前目录下的所有文件
        File[] files = file.listFiles();  
        if (files == null){  
            return;  
        }  
        for (File f : files){  
            if (f.isFile() && f.getName().equals(fileName)){  
                System.out.println(f.getAbsoluteFile());  
            }else if (f.isDirectory()){  
                findFile(fileName, f);  
            }  
        }  
    }  
  
    public static void deleteFile(File file){  
        File[] files = file.listFiles();  
        if (files == null){  
            return;  
        }  
        for (File f : files){  
            if (f.isFile()){  
                System.out.println(f.delete());  
            }else if (f.isDirectory()){  
                deleteFile(f);  
            }  
        }  
        System.out.println(file.delete());  
    }  
}
```

## 特殊文件类型
### Properties
### XML

## Log

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <!--  
        CONSOLE ：表示当前的日志信息是可以输出到控制台的。  
    -->  
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">  
        <!--输出流对象 默认 System.out 改为 System.err-->    
        <target>System.out</target>  
        <encoder>            
        <!--格式化输出：%d表示日期，%thread表示线程名，%-5level：级别从左显示5个字符宽度  
                %msg：日志消息，%n是换行符-->  
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%-5level] %c [%thread] : %msg%n</pattern>  
        </encoder>  
    </appender>  
    
    <!-- File是输出的方向通向文件的 -->  
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">  
        <encoder>  
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>  
            <charset>utf-8</charset>  
        </encoder>  
        <!--日志输出路径-->  
        <file>E:/log/company-data.log</file>  
        <!--指定日志文件拆分和压缩规则-->  
        <rollingPolicy  
                class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">  
            <!--通过指定压缩文件名称，来确定分割文件方式-->  
            <fileNamePattern>E:/log/company-data-%i-%d{yyyy-MM-dd}-.log.gz</fileNamePattern>  
            <!--文件拆分大小-->  
            <maxFileSize>1MB</maxFileSize>  
        </rollingPolicy>  
    </appender>  
    
    <!--  
        1、控制日志的输出情况：如，开启日志，取消日志  
        ALL 代表所有日志全部记录  
        OFF 代表不记录任何日志  
        debug 支持debug及其以上的日志（debug、info、warn、error）  
        warn 支持warn及其以上的日志（warn、error）  
        trace < debug < info < warn < error    
	-->    
	<root level="debug">  
        <appender-ref ref="CONSOLE"/>  
        <appender-ref ref="FILE"/>  
    </root>  
</configuration>
```
