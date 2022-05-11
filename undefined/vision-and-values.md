---
cover: >-
  https://images.unsplash.com/photo-1509114397022-ed747cca3f65?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwzfHxjb2xvciUyMG1peHxlbnwwfHx8fDE2NTIyODQ3NjM&ixlib=rb-1.2.1&q=85
coverY: 0
---

# 디자인 패턴 개요

## 디자인 패턴이란

* 프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 '규약' 형태로 만들어 놓은 것
* 소프트웨어를 설계할 때 특정 맥락에서 자주 발생하는 고질적인 문제들이 또 발생했을 때 재사용할 할 수있는 훌륭한 해결책
* **디자인 패턴은 아이디어**임, 특정한 구현이 아님.
* 프로젝트에 항상 적용해야 하는 것은 아니지만, 추후 재사용, 호환, 유지 보수시 발생하는 **문제 해결을 예방하기 위해 패턴을 만들어 둔 것**임.



* "바퀴를 다시 발명하지 마라(Don't reinvent the wheel)"
  * 이미 만들어져서 잘 되는 것을 처음부터 다시 만들 필요가 없다는 의미이다.
* 패턴이란
  * 각기 다른 소프트웨어 모듈이나 기능을 가진 다양한 응용 소프트웨어 시스템들을 개발할 때도 서로 간에 공통되는 설계 문제가 존재하며 이를 처리하는 해결책 사이에도 공통점이 있다. 이러한 유사점을 패턴이라 한다.
  * 패턴은 공통의 언어를 만들어주며 팀원 사이의 의사 소통을 원활하게 해주는 아주 중요한 역할을 한다.



### **원칙**

**SOLID (객체지향 설계 원칙)**

(간략한 설명)

1.  **Single Responsibility Principle**

    > 하나의 클래스는 하나의 역할만 해야 함.
2.  **Open - Close Principle**

    > 확장 (상속)에는 열려있고, 수정에는 닫혀 있어야 함.
3.  **Liskov Substitution Principle**

    > 자식이 부모의 자리에 항상 교체될 수 있어야 함.
4.  **Interface Segregation Principle**

    > 인터페이스가 잘 분리되어서, 클래스가 꼭 필요한 인터페이스만 구현하도록 해야함.
5.  **Dependency Inversion Property**

    > 상위 모듈이 하위 모듈에 의존하면 안됨.
    >
    > 둘 다 추상화에 의존하며, 추상화는 세부 사항에 의존하면 안됨.

### &#x20;디자인 패턴의 종류

#### GoF 디자인 패턴

* GoF(Gang of Four)라 불리는 사람들
  * 에리히 감마(Erich Gamma), 리차드 헬름(Richard Helm), 랄프 존슨(Ralph Johnson), 존 블리시디스(John Vissides)
  * 소프트웨어 개발 영역에서 디자인 패턴을 구체화하고 체계화한 사람들
  * 23가지의 디자인 패턴을 정리하고 각각의 디자인 패턴을 생성(Creational), 구조(Structural), 행위(Behavioral) 3가지로 분류했다.

#### GoF 디자인 패턴의 분류

![](https://gmlwjd9405.github.io/images/design-pattern/types-of-designpattern.png)

`3가지 패턴의 목적을 이해하기!`

1.  생성 패턴 (Creational) : 객체의 **생성 방식** 결정

    * 객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공한다.

    Class-creational patterns, Object-creational patterns.

* 객체 생성에 관련된 패턴
* 객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공한다.

Class-creational patterns, Object-creational patterns.

1. 구조 패턴 (Structural) : 객체간의 **관계**를 조직

```
예) DBConnection을 관리하는 Instance를 하나만 만들 수 있도록 제한하여, 불필요한 연결을 막음.
```

```
예) 2개의 인터페이스가 서로 호환이 되지 않을 때, 둘을 연결해주기 위해서 새로운 클래스를 만들어서 연결시킬 수 있도록 함.

```

\


1. 행위 패턴 (Behavioral): 객체의 **행위**를 조직, 관리, 연합

\
