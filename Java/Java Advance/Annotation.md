## 注解
Java注解又称Java标注，是JDK5.0引入的一种注释机制。
Java语言中的类、方法、变量、参数和包等都可以被标注。和Javadoc不同，Java标注可以通过反射获取标注内容。在编译器生成类文件时，标注可以被嵌入到字节码中。Java虚拟机可以保留标注内容，在运行时可以获取到标注内容 。

## 内置注解
### 作用在代码的注解
- **`@Override`**  
	检查该方法是否是重写方法。如果发现其父类，或者是引用的接口中并没有该方法时，会报编译错误。
- **`@Deprecated`**  
	标记过时方法。如果使用该方法，会报编译警告。
- **`@SuppressWarnings`**  
	指示编译器去忽略注解中声明的警告。
### 元注解（作用在其他注解的注解）
- **`@Retention`**  
	标识这个注解怎么保存。
	- `RetentionPolicy.SOURCE` 注解只存在于源代码中，编译后会被丢弃。
	- `RetentionPolicy.CLASS` 字节码阶段有效。
	- `RetentionPolicy.RUNTIME` 运行阶段有效。
	若没有 `@Retention`，则默认是 `RetentionPolicy.CLASS`。
- **`@Documented`**  
	标记这些注解是否包含在用户文档中。
- **`@Target`**  
	标记这个注解应用于哪种Java成员。
	- `ElementType.TYPE` 可用于类、接口、枚举上。
	- `ElementType.FIELD` 可用于字段或枚举常量上。
	- `ElementType.METHOD` 可用于方法上。
	- `ElementType.CONSTRUCTOR` 可用于构造方法上。
	- ...
- **`@Inherited`**  
	标记这个注解是继承于哪个注解类（默认->注解并没有继承于任何子类）。

## 自定义注解
- **语法**
```java

```