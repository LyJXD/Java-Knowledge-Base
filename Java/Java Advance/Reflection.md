## 反射
反射是一种Java程序运行期间的动态技术，可以在运行时检査、修改其自身结构或行为。通过反射，程序可以访问、检测和修改它自己的类、对象、方法、属性等成员。
### 反射的作用
- **动态加载类**  
	程序可以在运行时动态地加载类库中的类。
- **动态创建对象**  
	反射可以基于类的信息，使程序在运行时，动态创建对象实例。
- **调用方法**  
	反射可以根据方法名称，使程序在运行时，动态地调用对象的方法(即使方法在编写程序时还没有定义)。
- **访问成员变量**  
	反射可以根据成员变量名称，使程序在运行时，访问和修改成员变量(反射可以访问私有成员变量)。
- **运行时类型信息**  
	反射允许程序在运行时，查询对象的类型信息，这对于编写通用的代码和库非常有用。
### 反射的工作流程
1. **获取 `Class` 对象** 首先获取目标类的 `Class` 字节码对象。
2. **获取成员信息** 通过 `Class` 对象，可以获取类的字段、方法、构造函数等信息。
3. **操作成员** 通过反射API可以读取和修改字段的值、调用方法以及创建对象。
### 反射的使用
- **获取 `Class` 对象**
```java
// 通过类字面量
Class<?> clazz = String.class;

// 通过对象实例
String str = "Hello";
Class<?> clazz = str.getClass();

// 通过 Class.forName() 方法
Class<?> clazz = Class.forName("java.lang.String");
```
- **获取构造函数**
```java
Class<?> clazz = Person.class;
Constructor<?> constructor = clazz.getConstructor(String.class, int.class);
Object obj = constructor.newInstance("John", 30);
```
- **创建对象**
```java
Class<?> clazz = Class.forName("java.lang.String");
// getDeclared...() 可以访问包括public、protected、default和private修饰的对方法应成员
// 适用于需要访问类中私有成员或受保护成员的场景
Object obj = clazz.getDeclaredConstructor().newInstance();
```
- **访问字段**
```java
Class<?> clazz = Person.class;
Field field = clazz.getDeclaredField("name");
field.setAccessible(true); // 如果字段是私有的，需要设置为可访问
Object value = field.get(personInstance); // 获取字段值
field.set(personInstance, "New Name"); // 设置字段值
```
- **调用方法**
```java
Class<?> clazz = Person.class;
Method method = clazz.getMethod("sayHello");
method.invoke(personInstance);

Method methodWithArgs = clazz.getMethod("greet", String.class);
methodWithArgs.invoke(personInstance, "World");
```
- **获取接口和父类**
```java
Class<?> clazz = Person.class;

// 获取所有接口
Class<?>[] interfaces = clazz.getInterfaces();
for (Class<?> i : interfaces) {
    System.out.println("Interface: " + i.getName());
}

// 获取父类
Class<?> superClass = clazz.getSuperclass();
System.out.println("Superclass: " + superClass.getName());
```