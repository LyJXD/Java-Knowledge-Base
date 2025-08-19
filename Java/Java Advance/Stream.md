Stream是 **Java 8 引入的重要新特性**，用于对集合、数组等数据源进行声明式处理的API，支持链式调用和惰性计算。
Stream的主要作用是进行数据的转换、筛选、聚合等操作，可以极大地简化对数据的处理。使用Stream可以避免显式地使用迭代器或循环来操作集合，提高代码的可读性和简洁性。
- **特点**
	1. stream不存储数据，而是按照特定的规则对数据进行计算，一般会输出结果。
	2. stream不会改变数据源，通常情况下会产生一个新的集合或一个值。
	3. stream具有延迟执行特性，只有调用终端操作时，中间操作才会执行。

## Stream流创建
### Collection集合创建
应用中最常用的一种
```java
// 使用java.util.Collection.stream()
List<Integer> integerList = new ArrayList<>(Arrays.asList(1,2,3,4,5));  
Stream<Integer> listStream = integerList.stream();
```
### Array数组创建
```java
// 使用java.util.Arrays.stream(T[] array)
int[] array={1,3,5,6,8};
IntStream stream = Arrays.stream(array);
```
### Stream方法创建
```java
// 使用Stream的静态方法：of()、iterate()、generate()
Stream<Integer> stream1 = Stream.of(1, 2, 3, 4, 5, 6);

Stream<Integer> stream2 = Stream.iterate(1, x -> x + 2).limit(3);  
stream2.forEach(System.out::println);  // 1 3 5
  
Stream<Double> stream3 = Stream.generate(() -> Math.random() * 10).limit(5);  
stream3.forEach(System.out::println);
```

## Stream的使用
### 中间操作
- **filter（过滤）**
	`filter()` 方法接受一个谓词（一个返回 `boolean` 值的函数），并返回一个流，其中仅包含通过该谓词的元素。
```java
List<String> names = Arrays.asList("Alex", "Brian", "Charles", "David");  
List<String> collect = names.stream()  
        .filter(item -> item.length() > 4).collect(Collectors.toList());  
System.out.println(collect);    // [Brian, Charles, David]
```
- **limit（限制）**
	`limit()` 方法可以将流限制为指定的元素数。
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);  
List<Integer> collect = numbers.stream().limit(3).collect(Collectors.toList());  
System.out.println(collect);    //[1, 2, 3]
```
- **skip（跳过）**
	`skip()` 方法可跳过前N个元素。
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);  
List<Integer> collect = numbers.stream().skip(2).collect(Collectors.toList());  
System.out.println(collect);    // [3, 4, 5]
```
- **map（转换）**
	`map()` 方法可将一个流的元素转换为另一个流。它接受一个函数，该函数映射流中的每个元素转到另一个元素。
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);  
List<Integer> collect = numbers.stream()  
        .map(n -> {  
            n = n * 2;  
            return n;  
        }).collect(Collectors.toList());  
for (Integer integer : collect) {  
    System.out.println("integer = " + integer);  
}  
// 输出  
// integer = 2  
// integer = 4  
// integer = 6  
// integer = 8  
// integer = 10
```
- 
### 终止操作