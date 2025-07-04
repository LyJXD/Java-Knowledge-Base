## 顺序结构
顺序结构是程序中最简单最基本的流程控制，没有特定的语法结构，按照代码的先后顺序，依次执行，程序中大多数的代码都是这样执行的。
总的来说：程序按照从上到下的顺序执行。
## 分支结构
### if分支语句
所有的条件表达式结果都是boolean类型。
#### 单分支语句
- **语法**
	if(条件表达式){  
		语句块;  
	}
- **示例**
```
Scanner sc = new Scanner(System.in);  
int a = sc.nextInt();
int b = sc.nextInt();

if(a > b){	
	System.out.println("a 大于 b");
}
```

#### 双分支语句
- **语法**
	if(条件表达式){  
		语句块A;  
	}else{  
		语句块B;  
	}
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
	if(条件表达式A){
		语句块A;
	}else if(条件表达式B){
		语句块B;
	}
	…
	else if(条件表达式N){
		语句块N;
	}else{
		语句块N+1
	}
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

## 循环结构