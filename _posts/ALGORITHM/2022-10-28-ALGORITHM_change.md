---
layout: single
title: "ALGORITHM_자료형 변환"
categories:
  - ALGORITHM
tags:
  - [2022-10, ALGORITHM, STUDY]
sidebar:
  nav: "docs"
---

# 📚 <a style="color:#00adb5">ALGORITHM</a>

<center>
<img width="90%" src="./../../images/algorithm.png">
</center>
<br>

# 📚 <a style="color:#00adb5">자료형 변환</a>

## <a style="color:#00adb5">String -> Int</a>

- Integer.parseInt(str);

```java
String str = "123";
int num = Integer.parseInt(str);
System.out.println(num);
// 123
```

- Integer.valueOf(str);

```java
String str = "123";
int num = Integer.valueOf(str);
System.out.println(num);
// 123
```

## <a style="color:#00adb5">Int -> String</a>

- String.valueOf(num);

```java
int num = 123;
String str = String.valueOf(num);
System.out.println(str);
// 123
```

- Integer.toString(num);

```java
int num = 123;
String str = Integer.toString(num);
System.out.println(str);
// 123
```

- ""+num;

```java
int num = 123;
String str = ""+num;
System.out.println(str);
// 123
```

## <a style="color:#00adb5">Char -> Int</a>

- int(ch);

```java
char ch = '9';
int num = int(ch);
System.out.println(num);
// 9
```

- ch - '0';

```java
char ch = '9';
int num = ch - '0'; // 57 - 48 = 9
System.out.println(num);
// 9
```


## <a style="color:#00adb5">Int -> Char</a>

- char(num);

```java
int num = 65;
char ch = (char)num;
System.out.println(ch);
// A
```