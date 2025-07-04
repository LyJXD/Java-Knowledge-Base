## 基本数据类型
### 整型  
- **byte** `byte b = 127;`  
	内存占位**1**字节
- **short** `short s = 32767;`  
	内存占位**2**字节
- **int** `int i = 2147483647;`
	内存占位**4**字节
- **long** `long l = 9223372036854775807L;
	内存占位**8**字节
### 浮点型
- **float** `float f = 1.1f;`  
	内存占位**4**字节
- **double** `double d - 1.2d;`  
	内存占位**8**字节
### 字符型
- **char** `char c = 'c';`  
	内存占位**2**字节
### 布尔型
- **boolean** `boolean bool = true;`  
	内存占位**1**字节

## 引用数据类型


## 类型转换
### 自动类型转换 
自动类型转换通常发生在赋值或运算时，当涉及不同类型的数据时，编译器会自动将精度小的类型转换为精度大的类型。自动类型转换没有数据丢失。
- **数据类型的精度大小顺序**
	byte -> short -> int -> long -> float -> double
	char -> int
byte、short、char类型在运算时会首先提升为int类型。
```
byte smallNum = 1; 
int bigNum = smallNum; // 触发自动类型转换

long longNum = 2L;
long sum01 = smallNum + bigNum + longNum; // 运算结果转为最大精度数据

byte num01 = 10;
byte num02 = 20;
int sum02 = num01 + num02; // byte转换为int进行运算
```
### 强制类型转换
大范围往小范围转化需要用到强制转换，转换后的值会有所损失。
```
int numA = 257; // ......1 00000001  
byte numB = (byte)numA;  
```
强制转换成byte，截取后八位，最终结果为1