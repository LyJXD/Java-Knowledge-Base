## 方法
Java方法是语句的集合，它们在一起执行一个功能。
- 方法是解决一类问题的步骤的有序组合。
- 方法包含于类或对象中。
- 方法在程序中被创建，在其他地方被引用。
- **优点**  
	1. 使程序变得更简短而清晰。
	2. 有利于程序维护。
	3. 可以提高程序开发的效率。
	4. 提高了代码的重用性。

### 方法的定义
- **语法** 
```
修饰符 返回值类型 方法名(参数类型 参数名){
    ...
    方法体
    ...
    return 返回值;
}
```
- **修饰符**  
	修饰符，这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。
- **返回值类型**  
	方法可能会返回值。returnValueType是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下，returnValueType是关键字void。
- **方法名**  
	是方法的实际名称。方法名和参数表共同构成方法签名。
- **参数类型**  
	参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。
- **方法体**  
	方法体包含具体的语句，定义该方法的功能。
- **示例**  
```
/** 返回两个整型变量数据的较大值 */
public static int max(int num1, int num2) {
   int result;
   if (num1 > num2)
      result = num1;
   else
      result = num2;
 
   return result; 
}
```
### 方法的调用
Java支持两种调用方法的方式，根据方法是否返回值来选择。
当程序调用一个方法时，程序的控制权交给了被调用的方法。当被调用方法的返回语句执行或者到达方法体闭括号时候交还控制权给程序。
当方法返回一个值的时候，方法调用通常被当做一个值。
- **示例** 
```
public class MethodDemo {    
	public static void main(String[] args) {  
	    int i = 5;  
	    int j = 2;  
	    int k = max(i, j);  
	    System.out.println( i + " 和 " + j + " 比较，最大值是：" + k);  
	}
	
    public static int max(int num1, int num2) {  
        int result;  
        if (num1 > num2) {  
            result = num1;  
        } else {  
            result = num2;  
        }  
        return result;  
    }  
}
```
如果方法返回值是void，方法调用一定是一条语句。
- **示例**  
```
public class MethodDemo {  
    public static void main(String[] args) {  
        print();  
    }  
    
    public static void print() {  
        System.out.println("hello world");  
    }  
}
```