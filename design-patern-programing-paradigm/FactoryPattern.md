# 팩토리 패턴

### Factory Method 패턴

- 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴
- 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정

  - ex) 라뗴 레시피, 아메리카노 레시피, 우유 레시피라는 구체적인 내용이 들어 있는 하위 클래스가 컨베이어 벨트를 통해 전달되고, 상위 클래스인 바리스타 공장에서 이 레시피를 토대로 우유 등을 생산하는 생산 공정

    {% embed url="https://github.com/wnghdcjfe/csnote/blob/main/ch1/5.js" %}

    - Coffe tree라는 상위 클래스가 중요한 뼈대를 결정하고 하위 클래스인 LatteFactory가 구체적인 내용 결정
    - 의존성 주입이라고 볼수도 있다. (CoffeFactory에서 LatteFactory의 인스턴스를 생성하는게 아닌, LatteFactory에서 생성한 인스턴스를 CoffeFactory에 주입하고 있기에)

- 상위 클래스와 하위 클래스가 분리되기 때문에 느슨한 결합을 가지며, 상위 클래스에서는 인스턴스 생성 방식에 대해 전혀 알 필요하가 없다. => 더 많은 유연성
- **객체 생성 처리를 서브 클래스로 분리** 해 처리하도록 캡슐화하는 패턴
- 즉, 객체의 생성 코드를 별도의 클래스/메서드로 분리함으로써 객체 생성의 변화에 대비하는 데 유용하다.

---

> Robot (추상 클래스)
>
> ​ ㄴ SuperRobot
>
> ​ ㄴ PowerRobot
>
> RobotFactory (추상 클래스)
>
> ​ ㄴ SuperRobotFactory
>
> ​ ㄴ ModifiedSuperRobotFactory

즉 Robot이라는 클래스를 RobotFactory에서 생성함.

### RobotFactory 클래스 생성

```java
public abstract class RobotFactory {
	abstract Robot createRobot(String name);
}
```

### SuperRobotFactory 클래스 생성

```java
public class SuperRobotFactory extends RobotFactory {
	@Override
	Robot createRobot(String name) {
		switch(name) {
		case "super" :
			return new SuperRobot();
		case "power" :
			return new PowerRobot();
		}
		return null;
	}
}
```

- 생성하는 클래스를 따로 만듬

- 그 클래스는 factory 클래스를 상속하고 있기 때문에, 반드시 createRobot을 선언

- name으로 건너오는 값에 따라서, 생성되는 Robot이 다르게 설계됨.

=> 정리하면, 생성하는 객체를 별도로 둔다. 그리고, 그 객체에 넘어오는 값에 따라서, 다른 로봇 (피자)를 만들어 낸다.

---

### 특정 기능의 구현은 개별 클래스를 통해 제공되는 것이 바람직한 설계다.

- 기능의 변경이나 상황에 따른 기능의 선택은 해당 객체를 생성하는 코드의 변경을 초래한다.
- 상황에 따라 적절한 객체를 생성하는 코드는 자주 중복될 수 있다.
- 객체 생성 방식의 변화는 해당되는 모든 코드 부분을 변경해야 하는 문제가 발생한다.
- [스트래티지 패턴](https://gmlwjd9405.github.io/2018/07/06/strategy-pattern.html), [싱글턴 패턴](https://gmlwjd9405.github.io/2018/07/06/singleton-pattern.html), [템플릿 메서드 패턴](https://gmlwjd9405.github.io/2018/07/13/template-method-pattern.html)을 사용한다.
- '생성(Creational) 패턴'의 하나

![](https://gmlwjd9405.github.io/images/design-pattern-factory-method/factory-method-pattern.png)

## 역할이 수행하는 작업

- Product
  - 팩토리 메서드로 생성될 객체의 공통 인터페이스
- ConcreteProduct
  - 구체적으로 객체가 생성되는 클래스
- Creator
  - 팩토리 메서드를 갖는 클래스
- ConcreteCreator
  - 팩토리 메서드를 구현하는 클래스로 ConcreteProduct 객체를 생성
- 팩토리 메서드 패턴의 개념과 적용 방법
  1. 객체 생성을 전담하는 별도의 **Factory 클래스 이용**
     - 스트래티지 패턴과 싱글턴 패턴을 이용한다.
     - 해당 Post에서는 이 방법을 기준으로 팩토리 메서드 패턴을 적용한다.
  2. **상속 이용**: 하위 클래스에서 적합한 클래스의 객체를 생성
     - 스트래티지 패턴, 싱글턴 패턴과 템플릿 메서드 패턴을 이용한다.
     - 해당 Post의 맨 하단에 '다른 방법으로 팩토리 메서드 패턴 적용하기'를 확인한다.
- 예시
  - 여러 가지 방식의 엘리베이터 스케줄링 방법 지원하기

## Reference

> - [JAVA 객체지향 디자인 패턴, 한빛미디어](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788968480911&orderClick=JAj)
> - [https://gmlwjd9405.github.io/2018/08/07/factory-method-pattern.html](https://gmlwjd9405.github.io/2018/08/07/factory-method-pattern.html)
