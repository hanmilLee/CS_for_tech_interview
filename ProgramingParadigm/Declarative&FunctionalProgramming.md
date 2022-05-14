# 선언형과 함수형 프로그래밍

{% embed url="https://velog.velcdn.com/images%2Fblackb0x%2Fpost%2F8b101ee9-7719-4dcc-be0f-fb138b713391%2Fimage.png" %}
[선언형, 명령형 프로그래밍 (velog.io)](https://velog.io/@blackb0x/%EC%84%A0%EC%96%B8%ED%98%95-%EB%AA%85%EB%A0%B9%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
{% endembed %}

## 선언형(Declarative) 프로그래밍

* 무엇을 풀어내는가에 집중하는 패러다임
* 프로그램은 함수로 이루어진 것이다 라는 명제가 담겨 있는 패러다
* How보다는 What을 설명하는 방식 (어떻게보단 무엇을)
* 알고리즘을 명시하지 않고 목표만 명시함

## 함수형(Funtional) 프로그래밍

* 순수 함수를 조합하고 공유 상태, 변경 가능한 데이터 및 부작용을 **피해** 소프트웨어를 만드는 프로세스
* '선언형' 프로그래밍으로, 애플리케이션의 상태는 순수 함수를 통해 전달된다.
* 애플리케이션의 상태가 일반적으로 공유되고 객체의 메서드와 함께 배치되는 OOP와는 대조되는 프로그래밍 방식



* 함수형 코드는 명령형 프로그래밍이나 OOP 코드보다 더 간결하고 예측가능하여 테스트하는 것이 쉽다. (하지만 익숙치 않으면 더 복잡해보이고 이해하기 어려움)
* 함수형 프로그래밍은 프로그래밍 언어나 방식을 배우는 것이 아닌, 함수로 프로그래밍하는 사고를 배우는 것이다.

> `기존의 사고방식을 전환하여 프로그래밍을 더 유연하게 문제해결 하도록 접근하는 것`

![](https://user-images.githubusercontent.com/6733004/46247710-5ce5fb00-c44a-11e8-9400-16dd44626820.png)



### 함수형 프로그래밍의 의미를 파악하기 전 꼭 알아야 할 것들

*   순수 함수 (Pure functions)

    > 입출력이 순수해야함 : 반드시 하나 이상의 인자를 받고, 받은 인자를 처리해 반드시 결과물을 돌려줘야 함. 인자 외 다른 변수 사용 금지
* 합성 함수 (Function composition)
* 공유상태 피하기 (Avoid shared state)
* 상태변화 피하기 (Avoid mutating state)
*   부작용 피하기 (Avoid side effects)

    > 프로그래머가 바꾸고자 하는 변수 외에는 변경되면 안됨. 원본 데이터는 절대 불변!

대표적인 자바스크립트 함수형 프로그래밍 함수 : map, filter, reduce



## 함수형 프로그래밍의 장점

함수형 코드는 명령형이나 객체지향 코드보다 간결하고 예측하기 쉬우며, 이에 따라 테스트가 더 쉬워진다.

### Pure functions

함수형 프로그래밍에서 중요한 핵심은 함수는 부작용이 없어야 하며, 외부의 상태에 종속되지 않아야 한다.\
즉, 함수는 입력을 받고 출력을 반환함에 있어 외부의 값에 접근하지 않아야 한다.\
다음 예제를 통해 `순수함수`와 `순수함수가 아닌 함수`에 대해 알아보겠다.

```javascript
/* pure function */
const double = num => (num * 2);

/* impure function */
const operand = 2;
const multiple = num => (num * operand);
```



`double`의 입력이 `2`라면, 해당 함수의 반환값은 항상 `4`이다.\
반면, `multiple`의 입력이 `2`로 고정되어도 함수 외부의 `operand`가 다른 `2`가 확실하지 않다면 반환 값을 `4`라고 예상하기 힘들다.



```javascript
var arr = [1, 2, 3, 4, 5];
var map = arr.map(function (x) {
  return x * 2;
}); // [2, 4, 6, 8, 10]
```

arr을 넣어서 map을 얻었음. arr을 사용했지만 값은 변하지 않았고 map이라는 결과를 내고 어떠한 부작용도 낳지 않음

이런 것이 바로 함수형 프로그래밍의 순수함수라고 말한다.\


```javascript
var arr = [1, 2, 3, 4, 5];
var condition = function (x) {
  return x % 2 === 0;
};
var ex = function (array) {
  return array.filter(condition);
};
ex(arr); // [2, 4]
```

이는 순수함수가 아니다. 이유는 ex 메소드에서 인자가 아닌 condition을 사용했기 때문.

순수함수로 고치면 아래와 같다.

```javascript
var ex = function (array, cond) {
  return array.filter(cond);
};
ex(arr, condition);
```

순수함수로 만들면, 에러를 추적하는 것이 쉬워진다. 인자에 문제가 있거나 함수 내부에 문제가 있거나 둘 중 하나일 수 밖에 없기 때문이다.

### Higher Order Functions

`HOC`(Higher Order Functions)는 다른 함수를 인자로 사용하거나 함수를 반환하는 함수, 또는 두 가지 특징을 모두 가진 함수이다.\
고차 함수는 다음과 같은 경우 주로 사용된다.\


* 콜백 함수, 프로미스, 모나드 등을 사용하여, 동작과 효과 또는 비동기 흐름 제어를 추상화하거나 격리한다.
* 다양한 데이터 유형에 대해 작동할 수 있는 유틸리티 생성한다.
* 함수를 부분적으로 인수에 적용하거나 재사용 또는 함수 조합을 위한 커리함수를 작성한다.
* 함수 목록을 가져오고, 해당 입력 함수의 조합을 반환한다.

다음은 사용 예제이다.

```javascript
const isEven = x => !(x % 2);

const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const evenNumbers = numbers.filter(isEven);

console.log(evenNumbers); // 2, 4, 6, 8, 10
```



`isEven`은 배열을 처리하는 로직이 필요 없으며, 배열을 순환하면서 재사용된다.

### Currying

커링은 여러 인자를 받는 함수를 인자 하나씩 사용하여 함수 순서를 실행할 수 있도록 변환하는 것을 말한다.\
이는 람다 표현식과 클로저를 통해 쉽게 구현할 수 있다.

```javascript
/* not curried function */
function sumOfThreeThings(x, y, z) {
  return x + y + z;
}

sumOfThreeThings(1, 2, 3); // 6

/* curried function */
const sumOfThreeThings = x =>
  y =>
    z =>
      x + y + z;
sumOfThreeThings(1)(2)(3); // 6
```



#### Auto-currying

[`lodash`](https://github.com/lodash/lodash)와 [`Ramda`](https://github.com/ramda/ramda)는 `curry`메소드를 가지고 있다. 이는 여러개의 인수를 가지는 함수를 커링된 함수로 만들어준다.

```javascript
// use lodash or ramda
const curry = _.curry || R.curry;

// given function that add 2 parameters
const add = (x, y) => x + y

// transfired function
const curriedAdd = curry(add);

// results
curriedAdd(1)(2) // 3
curriedAdd(1) // (y) => 1 + y
curriedAdd(1, 2) // 3
```



### Function composition

합성함수는 말그대로 두 가지 이상의 함수가 합성되었음을 뜻한다.\
두 함수 `f`와 `g`가 있고 `f(g(x))`와 같이 사용된다고 할 때, 이를 수식 `f ∘ g(x)`과 같이 표현할 수 있다.\
다음은 합성함수의 예시이다.

```javascript
const compose = (f, g) => x => f(g(x));

const add = x => y => x + y;
const pow = x => y => y ** x;

const add2 = add(2);
const square = pow(2);

const add2ThenSqaure = compose(square, add2);

add2ThenSquare(10); // 144
```



### Point free notation

`Point free`는 함수를 작성할 때, 매개변수를 정의하지 않는 것이다.\
이는 함수를 더욱 간결하게 해준다.\
다음은 `point free`한 함수에 대한 예이다.

```javascript
const map = fn => list => list.map(fn);
// or use lodash/fp
// imporjavt { map } from 'lodash/fp';

const add = x => y => x + y;

/* function without point-free */
const incrementAll = numbers => map(add(1))(numbers);

/* function with point-free */
const incrementAllWithPointFree = map(add(1));

incrementAll([1, 2, 3]); // [2, 3, 4]
incrementAllWithPointFree([1, 2, 3]); // [2, 3, 4]
```



불필요한 매개변수를 사용하지 않으므로 매개변수에 대한 이름들에 대해 생각하지 않아도 되며, 코드가 훨씬 간결해진다.

### Recursion

재귀 함수는 어느 조건을 만족할 때까지 자기 자신을 호출하는 함수이다.\
자바스크립트는 반복을 할 때, `for`, `while` 등의 반복문을 사용하지만, 함수형 프로그래밍에서는 반복문 대신 재귀를 사용한다.\
아래 예제는 동일한 루프 회수와 값을 얻게되는 반복문과 재귀함수이다.\
기존의 어떤 값을 수정하는 것이 아니라, 기존 값으로 새로운 값을 계산하고 이를 사용한다.

```javascript
/* sum 1..10 with loop */
let sum = 0;
for (let i = 1; i <= 10; i++) {
  sum += i + 1;
}
console.log(acc); // 55

/* sum 1..10 with recursion */
sumRange = ({ start, end }) =>
  (sum) => {
    if (start > end) {
      return sum;
    }
    return sumRange({ start: start + 1, end })(sum + start);
  };

sumRange({ start: 0, end: 10 })(0);
```



재귀는 `for`, `while` 등의 반복문을 대체할 수 있을 뿐만 아니라, 훨씬 유용하다. 특히 `분할 및 정복` 알고리즘을 구현하는 데 매우 유용하다.\
가장 대표적인 재귀 함수 사용 예는 팩토리얼(`!`)이다.

```javascript
const factorial = n =>
  n ?
    n * factorial(n - 1) :
    1;
```



**재귀의 단점**

꼬리재귀 최적화가 되어있지 않은 언어에서는 재귀 사용 시 단점들이 있다.

* 반복문에 비해 속도가 느리다.
* 스택을 사용하기 때문에 반복이 많아질 경우, 스택오버플로우가 발생될 수도 있다.

`ES2015`의 `strict mode`는 `TCO`(Tail Call Optimization)를 제공하지만, ES5는 그렇지 않다.\
따라서, ES5에서 일반 반복대신 재귀를 사용하는 것은 성능 상의 이슈를 가질 수 있다.

### Monads

`Monad`는 `of`와 `chain`이 있는 객체이다.(`chain`은 중첩된 객체를 `un-nenesting`하는 점을 제외하면, `map`과 같다.)\


```javascript
// Implementation
Array.prototype.chain = function (f) {
  return this.reduce((acc, it) => acc.concat(f(it)), []);
}

// Usage
Array.of('cat,dog', 'fish,bird').chain(e => e.split(',')); // ['cat', 'dog', 'fish', 'bird']

// Difference with map
Array.of('cat,dog', 'fish,bird').map(e => e.split(',')); // [['cat', 'dog'], ['fish', 'bird']]


```

### 참고) Java에서의 함수형 프로그래밍

Java 8이 릴리즈되면서, Java에서도 함수형 프로그래밍이 가능해졌다.

```
함수형 프로그래밍 : 부수효과를 없애고 순수 함수를 만들어 모듈화 수준을 높이는 프로그래밍 패러다임
```

부수효과 : 주어진 값 이외의 외부 변수 및 프로그래밍 실행에 영향을 끼치지 않아야 된다는 의미

최대한 순수함수를 지향하고, 숨겨진 입출력을 최대한 제거하여 코드를 순수한 입출력 관계로 사용하는 것이 함수형 프로그래밍의 목적이다.

Java의 객체 지향은 명령형 프로그래밍이고, 함수형은 선언형 프로그래밍이다.

둘의 차이는 `문제해결의 관점`

여태까지 우리는 Java에서 객체지향 프로그래밍을 할 때 '데이터를 어떻게 처리할 지에 대해 명령을 통해 해결'했다.

함수형 프로그래밍은 선언적 함수를 통해 '무엇을 풀어나가야할지 결정'하는 것이다.

**Java에서 활용할 수 있는 함수형 프로그래밍**

* 람다식
* stream api
* 함수형 인터페이스

Java 8에는 Stream API가 추가되었다.

```java
import java.util.Arrays;
import java.util.List;

public class stream {

	public static void main(String[] args) {
		List<String> myList = Arrays.asList("a", "b", "c", "d", "e");

        // 기존방식
        for(int i=0; i<myList.size(); i++){
            String s = myList.get(i);
            if(s.startsWith("c")){
                System.out.println(s.toUpperCase());
            }
        }

        // stream API를 이용한 방식
        myList.stream()
              .filter(s -> s.startsWith("c"))
              .map(String::toUpperCase)
              .forEach(System.out::println);

	}

}
```

뭐가 다른건지 크게 와닿지 않을 수 있지만, 중요한건 프로그래밍의 패러다임 변화라는 것이다.

단순히 함수를 선언해서 데이터를 내가 원하는 방향으로 처리해나가는 함수형 프로그래밍 방식을 볼 수 있다. **한눈에 보더라도 함수형 프로그래밍은 내가 무엇을 구현했는지 명확히 알 수 있다**. (무슨 함수인지 사전학습이 필요한 점이 있음)



## Reference

* [WONISM | 함수형 프로그래밍이란?](https://wonism.github.io/what-is-fp/)

##

***
