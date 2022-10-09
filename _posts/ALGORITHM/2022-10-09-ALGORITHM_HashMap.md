---
layout: single
title: "ALGORITHM_HashMap"
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

# 📚 <a style="color:#00adb5">HashMap</a>

## <a style="color:#00adb5">HashMap</a>

HashMap은 Map 인터페이스를 구현한 대표적인 Map 컬렉션이다.<br>
Map의 성질을 그대로 가지고 있다.<br>
<a style="color:red"><strong>Key 값과 Value 값으로 구성된 Entity 객체를 저장하는 구조를 가진 자료구조</strong></a><br>
Key값은 중복이 허용되지 않지만 Value값은 중복이 허용된다.<br>
<a style="color:red"><strong>많은 양의 데이터를 검색하는데 있어 뛰어난 성능을 보인다.</strong></a>
많은 양의 데이터 중에 특정 데이터를 검색할 때 유리함


## <a style="color:#00adb5">HashMap 주요 메서드</a>

### HashMap 선언

```java
    // key : String, value : Integer
    HashMap<String, Integer> map = HashMap<String, Integer>();
```

### HashMap 값 추가

- map.put(key값, value값);

```java
    // put(key값, value값)
    map.put("a",123);
    map.put("b",234);
```

### HashMap 값 수정

- map.put(key값, value값);
- 데이터를 추가할 때 'Key값'이 같으면 나중에 입력한 값이 저장된다.

```java
    // 기존의 값을 덮어쓴다.
    map.put("a",555);
```

### HashMap 값 삭제

- map.remove(key값);
- 'Key값'이 같은 자료를 찾아 삭제한다.
- 반환값 : 삭제한 자료의 value 값

```java
    int value = map.remove("a");
    // value = 555

```

### HashMap 값 읽기

- map.get(key값);
- 반환값 : key값과 짝이 되는 value 값

```java
    int value = map.get("b");
    // value = 234
```

### 값이 존재하는지 여부 메서드

- map에 Key값이 존재하면 True, 아니면 False
    - map.containsKey(key값);
- map에 Value값이 존재하면 True, 아니면 False
    - map.containsValue(value값);
- 반환값 : boolean

```java
    boolean check = map.containsKey("b");
    // check = true
    boolean check_value = map.containsValue(444);
    // check_value = false
```

### 모든 데이터 읽어오기

- 모든 Key값 읽어오기
- keySet() 메서드 사용

```java
    for(String key : map.keySet()){
        // Key값을 이용해서 value 값 구하기
       int value = map.get(key);
    }
```

<br>

- 모든 Value값 읽어오기
- values() 메서드 사용
- Key값은 알 수 없다.

```java
    for(int value : map.values()){
        // 모든 value 값 출력
        System.out.println(value);
    }
```

<br>

- 모든 Key, Value 값 가져오기
- EntrySet() 메서드 사용

```java
    for(Map.Entry<String, Integer> entry : map.entrySet()){
        // 순서대로 Key값 value값 가져오기
        String key = entry.getKey();
        int value = entry.getValue();
    }
```

### 전체 삭제

- map.clear();

```java
    map.clear();
```

### 자료가 있는지 판단

- map.isEmpty();
- 반환값 : boolean
- 없으면 True, 있으면 False

```java
    boolean check = map.isEmpty();
```


### 크기

- HashMap의 총 크기
- 반환값 : int

```java
    int size = map.size();
```