## 正则表达式
### 基本元字符
| **元字符** | **说明**          |
| :------ | :-------------- |
| .       | 匹配任意单个字符        |
| \|      | 逻辑或操作符          |
| []      | 匹配字符集合中的一个字符    |
| [^]     | 对字符集合求非         |
| -       | 定义一个区间（例如[A-Z]） |
| \       | 对下一个字符转义        |
### 数量元字符
| **元字符** | **说明**                        |
| :------ | :---------------------------- |
| *       | 匹配前一个字符（子表达式）的零次或多次重复（默认贪婪匹配） |
| \*?     | \*的懒惰匹配版本                     |
| +       | 匹配前一个字符（子表达式）的一次或多次重复（默认贪婪匹配） |
| +?      | +的懒惰匹配版本                      |
| ?       | 匹配前一个字符（子表达式）的零次或一次重复         |
| {n}     | 匹配前一个字符（子表达式）的n次重复            |
| {m,n}   | 匹配前一个字符（子表达式）至少m次且至多n次重复      |
| {n,}    | 匹配前一个字符（子表达式）n次或更多次重复         |
| {n,}?   | {n, }的懒惰匹配版本                  |
### 位置元字符
| **元字符** | **说明**        |
| :------ | :------------ |
| ^       | 匹配字符串的开头      |
| \A      | 匹配字符串的开头      |
| $       | 匹配字符串的结束      |
| \Z      | 匹配字符串的结束      |
| \\<     | 匹配单词的开头       |
| \\>     | 匹配单词的结束       |
| \b      | 匹配单词边界(开头和结束) |
| \B      | \b的反义         |
### 特殊字符元字符
| **元字符**  | **说明**           |
| :------- | :--------------- |
| [\b]<br> | 退格字符             |
| \c       | 匹配一个控制字符         |
| \d       | 匹配任意数字字符         |
| \D       | \d的反义            |
| \f       | 换页符              |
| \n       | 换行符              |
| \r       | 回车符              |
| \s       | 匹配一个空白字符         |
| \t       | 制表符（Tab字符）       |
| \v       | 垂直制表符            |
| \w       | 匹配任意字母数字字符或下划线字符 |
| \W       | \w的反义            |
| \x       | 匹配一个十六进制数字       |
| \0       | 匹配一个八进制数字        |
### 案例
- **复杂邮箱验证**
    - 编写正则表达式验证以下邮箱规则：
        - 用户名部分：4-20位，可包含字母、数字、下划线、点、横线
        - 域名部分：2-20位字母数字和横线
        - 顶级域名：2-10位字母
        - 可选子域名：最多两级
```java
return email.matches("^[A-Za-z0-9._-]{4,20}@" +  
            "[A-Za-z0-9-]{2,20}" +  
            "(\\.[A-Za-z0-9-]{2,20})?" +  
            "\\.[A-Za-z]{2,10}$");
```
- **正则替换应用**
    - 使用正则表达式将字符串中的手机号中间4位替换为`****`：
        `String input = "我的电话是13812345678，备用电话是15987654321"`
    - 期望输出：
	    `我的电话是138****5678，备用电话是159****4321` 
```java
public static void main(String[] args) {  
	String input = "我的电话是13812345678, 备用电话是15987654321";  
	String regex = "(\\d{3})\\d{4}(\\d{4})";  
	String result = input.replaceAll(regex, "$1****$2");    // $ -> 捕获（）分组  
	System.out.println(result);  
}
```
- **正则切割复杂字符串**
    - 使用正则表达式切割以下字符串为单词数组（考虑连字符和撇号）：
        String input = "It's a test-string, with:some;punctuation!";  
        // 期望输出: \["It's", "a", "test-string", "with", "some", "punctuation"]  
```java
public static void main(String[] args) {  
	String input = "It's a test-string, with:some;punctuation!";  
	String[] result = input.split("[^\\w'-]+");  
	System.out.println(Arrays.toString(result));  
}
```
- **日志分析系统**
- 从以下格式的日志中提取 IP、时间
	`String log = "192.168.1.1 - - [10/Oct/2023:13:55:36 +0800] \"GET /api/user HTTP/1.1\" 200 1234";`
- 使用正则表达式提取后，按状态码分组统计次数
```java
public static void main(String[] args) {
    String log = "192.168.1.1 - - [10/Oct/2023:13:55:36 +0800] \"GET /api/user HTTP/1.1\" 200 1234";
    String regexIp = "\\d{3}.\\d{3}.\\d.\\d";
    String regexTime = "(0[1-9]|[1-2][0-9]|3[0-1])/[A-Za-z]{3}/\\d{4}:([0-1][0-9]|2[0-3]):([0-5][0-9]):([0-5][0-9]) \\+\\d{4}";
    Pattern patternIp = Pattern.compile(regexIp);
    Pattern patternTime = Pattern.compile(regexTime);
    Matcher matchIp = patternIp.matcher(log);
    Matcher matchTime = patternTime.matcher(log);
    while (matchIp.find()) {
        System.out.println(matchIp.group());
    }
    while (matchTime.find()) {
        System.out.println(matchTime.group());
    }
}
```
- **数据清洗工具**
	- 设计一个方法，接收字符串和正则表达式数组：
	    - 依次应用每个正则表达式进行替换
	    - 返回最终清洗后的字符串
```java
public static void main(String[] args) {
    String input = "用户电话: 138-1234-5678, 邮箱: user@example.com";
    String[] regexes = {"\\d{4}", "\\w+@"};
    String[] replacements = {"****", "***@"};
    String result = replaceByRegex(input, regexes, replacements);
    System.out.println(result);
}

public static String replaceByRegex(String input, String[] regexes, String[] replacements) {
    for (int i = 0; i < regexes.length; i++) {
        input = input.replaceAll(regexes[i], replacements[i]);
    }
    return input;
}
```