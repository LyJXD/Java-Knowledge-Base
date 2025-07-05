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
int[] array = {1, 2, 3, 4, 5};
```
- **动态创建**  
```
Scanner sc = new Scanner(System.in);  

int[] arr = new int[5];  // 未初始化则默认值为0
for (int i = 0; i < arr.length; i++){  
    int num = sc.nextInt();  
    arr[i] = num;  
}
```
### 数组遍历
