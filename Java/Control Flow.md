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
switch(值)，值的取值类型可以是byte、short、int、char、string
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
- **穿透现象**  
	当一个case分支没有[[#break]]语句时，即使该case分支的条件满足，程序也会继续执行下一个case分支的代码，直到遇到break语句或switch语句结束。
- **示例**
```
Scanner sc = new Scanner(System.in);  
System.out.println("Enter date you want to check:");  
int day = sc.nextInt();  
switch (day) {  
    case 1:  
    case 2:  
    case 3:  
    case 4:  
    case 5:  
        System.out.println("今天是星期" + day + "，是工作日");  
        break;  
    case 6:  
    case 7:  
        System.out.println("今天是星期" + day + "，是休息日");  
        break;  
    default:  
        System.out.println("非法输入");
```

## 循环结构
### for循环
执行顺序:初始化循环条件->循环条件表达式->循环体->迭代部分
- **语法**  
```
for (初始化循环条件; 循环条件表达式; 迭代部分 ){  
    循环体;  
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
条件表达式返回值类型为boolean类型，只要条件表达式的结果为true,则一直执行语句块。
- **语法**
```
while (循环条件部分){  
    循环体部分;   
	迭代部分;  
}
```
- **示例**
```
double height = 8848860.0;  
double paperHeight = 0.1;  
  
int count = 0;  
while (paperHeight < height) {  
    paperHeight *= 2;  
    count++;  
}  
System.out.println("折叠了" + count + "次");  
System.out.println("最终的纸张高度为" + paperHeight + "mm");
```

### do...while循环
先执行do对应的语句块，然后再判断循环条件，只要循环条件满足，则一直执行循环体，否则结束循环。
- **语法**  
```
do {  
    循环体部分;  
    迭代部分;  
} while (循环条件部分);
```
- **示例**  
```
Scanner sc = new Scanner(System.in);  
String answer = "";  
do {  
    System.out.println("上机编写程序！");  
    System.out.print("合格了吗?(y/n)");  
    answer = sc.next();  
    System.out.println("");  
} while (!"y".equals(answer));  
  
System.out.println("恭喜你通过了测试！");
```

## 跳转关键字
### continue
用在循环中，跳过本次循环，执行下一次循环。
### break
用于在循环中，跳出循环而执行循环后面的语句。