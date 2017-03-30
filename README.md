# cs502_Capstone_yxwang
https://github.com/UncleBarney/CS502-1701/issues/156

# This is my Apache Pig contributor project.
	start from: 3/24/2017
		    to: 4/7/2017

## Project: UDF to find All Regex Matches
	example: 
		input: xxx=1, yyyy=2, zzzzz=3
		Get{(1),(2),(3)} using regex: "=(\d?)\s"

## Steps:
	1. Write a Pig UDF to find All regular expression matches
	2. test
	3. create a Jira issue
	4. Assign
	5. commiter review
	6. Pass review

## Test case:

**可以加在testbuiltin里，但test case是要自己写的**

```
	test case: a = load '1.txt' as (line:chararray);
	b = foreach a generate flatten(STRING_SEARCH(line, '=\\d*\\s'));
	dump b;
```

--1.txt
a=15 b=17 c=20 and somthing else
a=18 bla bla
--
STRING_SEARCH结果: {(15),(17),(20)}, {(18)}

## Explanation from Mr.Dai
    就是一个高级的string search, 只不过你用regex表达你要search的东西, 基本上就是吧REGEX_EXTRACT_ALL改一下(改exec改写一下就行了), 要会用java regex的类和函数(https://www.tutorialspoint.com/java/java_regular_expressions.htm)

## What is different from REGEX_EXTRACT_ALL
input: 处理input根REGEX_EXTRACT_ALL基本差不多
output: output稍有不同，因为你要创建一个bag

创建bag可以参考:
https://github.com/apache/pig/blob/trunk/src/org/apache/pig/builtin/STRSPLITTOBAG.java

和REGEX_EXTRACT_ALL不一样的。
REGEX每个输出是match patten的不同部分。

eg:
flatten ( REGEX_EXTRACT_ALL(line, '(.*?) .*?\\[(.*?)\\].*&cat=(.*?)[ &].*' )，输出第一项是match pattern里第一个括号, 第二项是match pattern里第二个括号
