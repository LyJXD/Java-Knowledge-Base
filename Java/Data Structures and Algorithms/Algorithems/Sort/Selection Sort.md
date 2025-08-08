## 选择排序
```java
//选择排序
void swap(int* a, int* b)
{
	int tem = *a;
	*a = *b;
	*b = tem;
}
void SelectSort(int* arr, int n)
{
	//保存参与单趟排序的第一个数和最后一个数的下标
	int begin = 0, end = n - 1;
	while (begin < end)
	{
		//保存最大值的下标
		int maxi = begin;
		//保存最小值的下标
		int mini = begin;
		//找出最大值和最小值的下标
		for (int i = begin; i <= end; ++i)
		{
			if (arr[i] < arr[mini])
			{
				mini = i;
			}
			if (arr[i] > arr[maxi])
			{
				maxi = i;
			}
		}
		//最小值放在序列开头
		swap(&arr[mini], &arr[begin]);
		//防止最大的数在begin位置被换走
		if (begin == maxi)
		{
			maxi = mini;
		}
		//最大值放在序列结尾
		swap(&arr[maxi], &arr[end]);
		++begin;
		--end;
	}
}
```