# 전략 패턴

- 객채의 행위를 바꾸고 싶은 경우 직접 수정하지 않고 전략이라고 부르는 캡슐화한 알고리즘을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴
  - ex) 물건살때 네이버페이, 카카오페이 등 다양한 방법으로 결제 하듯

* **행위를 클래스로 캡슐화해** 동적으로 행위를 자유롭게 바꿀 수 있게 해주는 패턴
* 같은 문제를 해결하는 여러 알고리즘이 클래스별로 캡슐화되어 있고 이들이 필요할 때 교체할 수 있도록 함으로써 동일한 문제를 다른 알고리즘으로 해결할 수 있게 하는 디자인 패턴
* '행위(Behavioral) 패턴'의 하나
* 즉, **전략을 쉽게 바꿀 수 있도록** 해주는 디자인 패턴이다.

### 전략이란

- 어떤 목적을 달성하기 위해 일을 수행하는 방식, 비즈니스 규칙, 문제를 해결하는 알고리즘 등
- 특히 게임 프로그래밍에서 게임 캐릭터가 자신이 처한 상황에 따라 공격이나 행동하는 방식을 바꾸고 싶을 때 스트래티지 패턴은 매우 유용하다.

### 역할이 수행하는 작업

- Strategy

  - 인터페이스나 추상 클래스로 외부에서 동일한 방식으로 알고리즘을 호출하는 방법을 명시

- ConcreteStrategy

  - 스트래티지 패턴에서 명시한 알고리즘을 실제로 구현한 클래스

- Context
  - 스트래티지 패턴을 이용하는 역할을 수행한다.
  - 필요에 따라 동적으로 구체적인 전략을 바꿀 수 있도록 setter 메서드('집약 관계')를 제공한다.

---

### Strategy pattern을 적용한 설계는 아래와 같다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F255CF641559E74AC09EFBB">

> 상속은 무분별한 소스 중복이 일어날 수 있으므로, 컴포지션을 활용한다. (인터페이스와 로직의 클래스와의 관계를 컴포지션하고, 유닛에서 상황에 맞는 로직을 쓰게끔 유도하는 것)

<br>

- ##### 미사일을 쏘는 것과 폭탄을 사용하는 것을 캡슐화하자

  ShootAction과 BombAction으로 인터페이스를 선언하고, 각자 필요한 로직을 클래스로 만들어 implement한다.

- ##### 전투기와 헬리콥터를 묶을 Unit 추상 클래스를 만들자

  Unit에는 공통적으로 사용되는 메서드들이 들어있고, 미사일과 폭탄을 선언하기 위해 variable로 인터페이스들을 선언한다.

<br>

전투기와 헬리콥터는 Unit 클래스를 상속받고, 생성자에 맞는 로직을 정의해주면 끝난다.

##### 전투기 예시

```java
class Fighter extends Unit {
    private ShootAction shootAction;
    private BombAction bombAction;

    public Fighter() {
        shootAction = new OneWayMissle();
        bombAction = new SpreadBomb();
    }
}
```

`Fighter.doAttack()`을 호출하면, OneWayMissle의 attack()이 호출될 것이다.

<br>

#### 정리

이처럼 Strategy Pattern을 활용하면 로직을 독립적으로 관리하는 것이 편해진다. 로직에 들어가는 '행동'을 클래스로 선언하고, 인터페이스와 연결하는 방식으로 구성하는 것!

<br>

<br>

##### [참고]

[링크](https://flowarc.tistory.com/entry/1-Strategy-Pattern?category=562154)

> - [https://gmlwjd9405.github.io/2018/07/06/strategy-pattern.html](https://gmlwjd9405.github.io/2018/07/06/strategy-pattern.html)
