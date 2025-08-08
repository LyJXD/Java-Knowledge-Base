## Lambda表达式
又称闭包，它是推动 Java 8 发布的最重要新特性。
Lambda表达式是一个匿名函数，是匿名函数的简写形式，我们可以把Lambda表达式理解为是一段可以传递的代码（将代码像数据一样进行传递），可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使Java的语言表达能力得到了提升。
- **特点**  
	Lambda表达式不是万能的，他需要函数式接口的支持。
	函数式接口就是一个有且仅有一个抽象方法，但是可以有多个非抽象方法的接口。
- **语法**
```java
实现的这个接口中的抽象方法中的形参列表 -> 抽象方法的处理
```
- **示例**
```java
public class Test {
    public static void main(String[] args) {
        Integer[] ints = {98, 243, 35, 13, 57, 243};
        List<Integer> list = Arrays.asList(ints);
        
        list.sort(new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2-o1;
            }
        });
        System.out.println(list);
        //[243, 243, 98, 57, 35, 13]
        
        //使用Lambda表达式
        list.sort((o1,o2)->(o1-o2));
        System.out.println(list);
        //[13, 35, 57, 98, 243, 243]
    }
}
```

## 方法引用
方法引用是**Lambda 表达式的一种简化写法**，当Lambda体中只是调用一个已经存在的方法时，可以用方法引用替代，从而使代码更简洁、可读性更高。  
方法引用本质上依旧是**函数式接口的实现**。
### 静态方法引用
- **语法**
```java
 类名称::静态方法名
```
- **示例**
```java
public class Cook {
	// 静态方法，通过类名称进行调用
	public static void makeFood(String food) {
		System.out.println("将" + food + "做成可口饭菜");
	}
}

// 保姆接口
@FunctionalInterface
public interface Sitter {
	// 工作，将食材做为熟饭
	public abstract void work(String food);
}

public class Lambda {
	public static void main(String[] args) {
		// 使用Lambda
		hireSitter(food -> System.out.println("将" + food + "做成可口饭菜"));
		// 方法引用，简化Lambda
		hireSitter(Cook::makeFood);
	}
	// 雇佣一个保姆去做饭
	public static void hireSitter(Sitter sitter) {
		sitter.work("白菜");
	}
}
```
### 实例方法引用
- **语法**
```java
对象名::成员方法名
```
- **示例**
```java
public class Cook {
	// 成员方法
	public void makeFood(String food) {
		System.out.println("将" + food + "做成可口的饭菜");
	}
}

public interface Sitter {
	public abstract void work(String food);
}

public class MethodRef {
	public static void main(String[] args) {
		// Lambda
		method(food -> System.out.println("将" + food + "做成可口的饭菜"));
		
		// 方法引用，引用了cook对象当中的成员方法makeFood
		Cook cook  = new Cook();
		method(cook::makeFood);
	}
	
	public static void method(Sitter sitter) {
		sitter.work("土豆");
	}
}

```
### 特定类型的方法引用
- **语法**
```java
特定类型::方法
```
- **示例**
```java
 String[] s = new String[]{"James","Vence","Jordan","Queen","moving","Hello","aaa","Sss","bbb","jack"};
 
//忽略大小首字母排序
Arrays.sort(s , new Comparator<String>() {
	@Override
	public int compare(String o1, String o2) {
		return o1.compareToIgnoreCase(o2);
	}
});
//lambda
Arrays.sort(s , ( o1, o2) -> o1.compareToIgnoreCase(o2));

//方法引用
Arrays.sort(s , String::compareToIgnoreCase);
System.out.println(Arrays.toString(s));
```
### 构造方法引用
- **语法**
```java
类名::new
```
- **示例**
```

```