## 数组
数组是一种数据结构，用于存储多个相同类型的数据。
- **特点**
	1. 元素在内存中连续存储，支持随机访问，访问速度快（时间复杂度 O(1)）
	2. 长度固定，一旦创建不可改变。
	3. 插入、删除效率较低（需要移动大量元素）。
	4. 按索引访问方便，但扩容需要重新分配和复制数据。
### 声明数组
- **语法**  
```java
dataType[] arrayName;
```
- **dataType**  
	它可以是基本数据类型[[Datatype]]，也可以是Java对象。
- **arrayName**  
	它是一个标识符
### 初始化数组
- **静态初始化**  
```java
int[] array1 = new int[]{1, 2, 3, 4, 5};
int[] array2 = {1, 2, 3};
```
- **动态初始化**  
```java
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
```java
//创建一个长度为5的数组  
int[] age = new int[5];  
  
//使用for循环访问元素  
for (int i = 0; i < age.length - 1; ++i) {  
    System.out.println(age[i]);  
}
```
