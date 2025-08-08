## 二分查找
```java
//二分查找，递归版本
public static int binarySearch(int array[], int value, int low, int high)
{
    if(low>high){
        return -1;
    }
    
    int mid = low+(high-low)/2;
    
    if(array[mid] == value)
        return mid;
    if(array[mid] > value)
        return binarySearch(array, value, low, mid - 1);
    if(array[mid] < value)
        return binarySearch(array, value, mid + 1, high);
}
 
//二分查找，非递归版本
public static int binarySearch2(int[] array, int key) {
    int low = 0;
    int high = array.length - 1;
    while (low <= high) {
        //防止数组越界，且位运算比除法运算快
        int mid = low + ((high - low) >> 1);
        if (key == array[mid]) {
            return mid;
        }
        if (key > array[mid]) {
            low = mid + 1;
        }
        if (key < array[mid]) {
            high = mid - 1;
        }
    }
    return -1;
}
```