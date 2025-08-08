## 冒泡排序
```java
public static void  BubbleSort(int[] arr){
	//第一层for循环,用来控制冒泡的次数
	for (int i = 1; i < arr.length; i++) {  
		//第二层for循环,用来控制冒泡一层层到最后
		for (int j = 0; j < arr.length-1; j++) { 
			//如果前一个数比后一个数大,两者调换 ,意味着泡泡向上走了一层
			if (arr[j] > arr[j+1] ){
				int temp = arr[j];
				arr[j] = arr[j+1];
				arr[j+1] = temp;
			}
		}
	}
}
```
- 
```

```