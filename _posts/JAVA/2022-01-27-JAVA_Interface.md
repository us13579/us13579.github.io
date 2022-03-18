---
layout: single
title:  "JAVA_Interface ( 인터페이스 )"
categories: 
    - JAVA
tags: 
    - [2022-01, JAVA, STUDY]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">JAVA</a>

<center>
<img width="90%" src="./../../images/java.png">
</center>
<br>

# 📚 <a style="color:#00adb5">Interface ( 인터페이스 )</a>

## <a style="color:#00adb5">Interface ( 인터페이스 )</a> 란 무엇인가 ?
### <a style="color:#00adb5"><b>인터페이스 개념</b></a>
인터페이스란 사전적 정의로는 서로 다른 두 시스템, 장치, 소프트웨어 따위를 서로 이어주는 부분 또는 그런 장치이다.<br>
자바에서는 <a style="color:red"><b>극단적으로 동일한 목적 하에 동일한 기능을 수행하게끔 강제하는 것이 인터페이스의 역할이자 개념이다. </b></a><br>

### <a style="color:#00adb5"><b>인터페이스 작성</b></a>
인터페이스는 키워드 <a style="color:red"><b>'interface'</b></a> 키워드로 선언할 수 있다.<br>
인터페이스는 최고 수준의 추상화 단계이다. 그래서 모든 메서드가 <a style="color:red"><b>'abstarct'</b></a>형태를 하고 있다.<br>
JAVA8 이전가지는 상수, 추상메서드만 선언이 가능했는데 JAVA8부터 디폴트메서드(default), 정적메서드(static)가 추가되었다.<br>
<a style="color:red"><b>=> 상수, 추상메서드, 디폴트메서드, 정적메서드 만 사용 가능</b></a><br>
그만큼 전에는 강제성이 강했고 이제 강제성 안에 유연함을 심었다고 생각하면 된다.<br>
인터페이스의 선언은 클래스와 유사하다.<br>
모든 멤버변수는 <a style="color:red"><b>public static final</b></a> 이며 생략 가능하다.<br>
모든 메서드는 <a style="color:red"><b>public abstract</b></a> 이며 생략 가능하다.<br>
인터페이스는 <a style="color:red"><b>'extends'</b></a> 키워드를 통해 상속이 가능하다.<br>
클래스와 다른 점은 다중 상속이 가능하다는 점이다.<br>
<a style="color:red"><b>'implements'</b></a> 키워드로 일반 클래스에서 인터페이스를 구현할 수 있다.<br>
implements 한 클래스는 <a style="color:red"><b>모든 abstract 메서드를 override해서 구현</b></a> 하거나 <br>
<a style="color:red"><b>구현하지 않을 경우 abstract 클래스로 표시</b></a>해야 한다.<br>
여러개의 interface implements 가 가능하다.<br>

### <a style="color:#00adb5"><b>Default Method ( 디폴트 메서드 )</b></a>
인터페이스에 선언된 구현부가 있는 메서드. 접근 제한자는 public으로 한정<br><br>
필요성<br>
- 기존에 interface 기반으로 동작하는 라이브러리의 interface에 추가해야 하는 기능이 발생<br>
- 기존 방식으로라면 모든 구현체들이 추가되는 메서드를 override 해야함 -> 많은 인력과 시간 소요<br> 
- default 메서드는 abstract가 아니므로 반드시 구현해야 할 필요는 없어짐<br>

### <a style="color:#00adb5"><b>Static Method ( 정적 메서드 )</b></a>
일반 static 메서드와 마찬가지로 별도의 객체가 필요 없다.<br>
구현체 클래스 없이 바로 인터페이스 이름으로 메서드에 접근해서 사용가능<br>
-> 객체 생성 없이 바로 사용 <br>

## 인터페이스를 사용하는 이유?
구현의 강제로 일관되고 정형화된 개발을 위한 표준화 가능 ( 대규모 프로젝트 개발 시 더 빛을 발휘한다 )<br>
인터페이스를 통한 간접적인 클래스 사용으로 손쉬운 모듈 교체 지원<br>
서로 상속의 관계가 없는 클래스들에게 인터페이스를 통한 관계 부여로 다형성 확장<br>
모듈 간 독립적 프로그래밍 가능 -> 개발 시간 단축<br>
클래스를 통한 다중 상속이 불가능하므로, 인터페이스는 가능<br>

<a style="color:red"><b>자바의 다형성을 이용하여 개발코드 수정을 줄이고 유지보수성을 높인다 !</b></a>


## 인터페이스 실습 해보즈아 !
### <a style="color:#00adb5"><b>interface 구조</b></a>

```java
public interface face{
    // 상수
    public static final 타입 상수명 = 값;

    // 추상 메서드
    public abstract 타입 메서드명(매개변수..);

    // 디폴트 메서드
    public default 타입 메서드명(매개변수..){
        // 구현
    }

    // 정적 메서드
    public static 타입 메서드명(매개변수..){
        // 구현
    }
}
```
인터페이스에서 사용할 수 있는 것들의 구조를 적어보았다.<br>
상수는 <a style="color:red"><b>public static final</b></a><br>
추상 메서드는 <a style="color:red"><b>public abstract</b></a><br>
디폴트 메서드는 <a style="color:red"><b>public</b></a><br>
정적 메서드는 <a style="color:red"><b>public</b></a><br>
를 생략할 수 있다.
<hr>

### <a style="color:#00adb5"><b>출력 결과</b></a>
미완성!! 은행으로 해보기
<hr>

## 인터페이스 마무리
확실히 추상 클래스를 이해하고 인터페이스를 공부하니 어렵다는 생각은 하지 못했다.<br>
그리고 간단한 코딩이나 작은 프로젝트에서는 크게 못 느낄 것 같지만 규모가 있는 프로젝트를 진행하면 인터페이스의 장점을 몸소 느낄 수 있을 것 같다.<br>
나중에 프로젝트를 할 때 인터페이스를 많이 사용해 보도록 노력해야 겠다.<br>
인터페이스가 진정한 객체지향 프로그래밍을 하는게 큰 도움이 되지 않나 생각한다 🧐



<br><br><br><br>

👏 참조<br>
<a href="https://limkydev.tistory.com/197?category=957527" target=_blank>https://limkydev.tistory.com/197?category=957527</a>
<a href="http://www.tcpschool.com/java/java_polymorphism_interface" target=_blank>http://www.tcpschool.com/java/java_polymorphism_interface</a>