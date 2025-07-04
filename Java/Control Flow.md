## 顺序结构
顺序结构是程序中最简单最基本的流程控制，没有特定的语法结构，按照代码的先后顺序，依次执行，程序中大多数的代码都是这样执行的。
总的来说：程序按照从上到下的顺序执行。
## 分支结构
### if分支语句
所有的条件表达式结果都是boolean类型。
#### 单分支语句
- **语法**  
```
if(条件表达式) {
	语句块;
}
```
- **示例**
```
Scanner sc = new Scanner(System.in);  
int a = sc.nextInt();  
int b = sc.nextInt();  
  
if(a > b) {  
    System.out.println("a 大于 b");  
}
```

#### 双分支语句
- **语法**  
```
if(条件表达式){
	语句块A;
}else{
	语句块B;
}
```
- **示例**
```
Scanner sc = new Scanner(System.in);
int num = sc.nextInt();  
  
if(num % 2 == 0) {  
    System.out.println(num + " is even");  
}else {  
    System.out.println(num + " is odd");  
}
```

#### 多分支语句
- **语法**  
```
if(条件表达式A) {
	语句块A;
}else if(条件表达式B) {
	语句块B;
}
...
else if(条件表达式N) {
	语句块N;
}else {
	语句块N+1
}
```
- **示例**
```
Scanner sc = new Scanner(System.in);
int score = sc.nextInt();  
  
if ( score >= 90 ) {  
    System.out.println("优秀");  
} else if (score >= 80 ) {  
    System.out.println("良好");  
} else if (score >= 60 ) {  
    System.out.println("中等");  
} else {  
    System.out.println("不及格");  
}
```
### switch分支语句
- **语法**  
```
switch(表达式) {
	case 值1:
		语句块1;
		break;
	...
	case 值N:
		语句块N;
		break;
	default:
		语句块default;
} 
```       
- **示例**
```
Scanner sc = new Scanner(System.in);  
System.out.println("只能输入1,2,3：");  
int a = sc.nextInt();  
switch(a) {  
    case 1:  
        System.out.println("one");  
        break;  
    case 2:  
        System.out.println("two");  
        break;  
    case 3:  
        System.out.println("three");  
        break;  
    default:  
        System.out.println("输入错误,请重新输入");
```
## 循环结构
### for循环
- **语法**  
```
for (初始化循环条件; 循环条件表达式; 迭代部分 ){  
    循环操作(循环体);  
}
```
- **示例**  
```
int sum = 0;  
for (int x = 0; x < 10; x++) {  
    sum += x;  
}  
System.out.println(sum);
```
### while循环

### do...while循环