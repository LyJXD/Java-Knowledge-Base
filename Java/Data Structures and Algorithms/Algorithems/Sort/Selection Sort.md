## 选择排序
```java
public class Selection {
    public static void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
            // 交换arr[i]和arr[minIndex]
            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
    
    public static void main(String[] args) {
        int[] arr = {5, 2, 8, 3, 1, 6};
        int[] expectedArr = {1, 2, 3, 5, 6, 8};
        Selection.selectionSort(arr);
        System.out.println("arr = " + Arrays.toString(arr));
        Assertions.assertArrayEquals(expectedArr, arr);
    }
}
```