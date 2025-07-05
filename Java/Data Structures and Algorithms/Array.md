## 数组
数组是一种数据结构，用于存储多个相同类型的数据。
### 声明数组
- **语法**  
```
dataType[] arrayName;
```
- **dataType**  
	它可以是基本数据类型[[Datatype]]，也可以是Java对象。
- **arrayName**  
	它是一个标识符
### 初始化数组
- **静态创建**  
```
int[] array = new int[5]{1, 2, 3, 4, 5};
```
一旦定义了数组的长度，就不能在程序中对其进行更改。
- **动态创建**  
```
Scanner sc = new Scanner(System.in);  

int[] arr = new int[5];  // 未初始化则默认值为0
for (int i = 0; i < arr.length; i++){  
    int num = sc.nextInt();  
    arr[i] = num;  
}
```
### 数组访问
- **数组索引**  
	 在Java中，数组中的每个元素都与一个数字相关联。这个数字称为数组索引。我们可以使用这些索引来访问数组的元素。索引值从0开始。
- **示例**  
```
//创建一个长度为5的数组  
int[] age = new int[5];  
  
//使用for循环访问元素  
for (int i = 0; i < 5; ++i) {  
    System.out.println(age[i]);  
}
```
