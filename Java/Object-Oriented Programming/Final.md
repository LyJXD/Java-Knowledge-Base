## final修饰类
当final关键字修饰一个类，则该类会成为最终类，即该类不能被继承，但是该类可以有父类。
- **示例**
```
//类名为Father的类被final关键字修饰，代表其不能被继承
final class Father {
	
} 

//现在类名为Son的类想继承Father这个类，编译器会报错
class Son extends Father {
	
}
```

## final修饰变量