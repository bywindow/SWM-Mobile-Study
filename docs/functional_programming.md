---
title: [mobile-study] week1. 함수형 프로그래밍
date: 2022-06-07
---
## 🐛 순수함수
수학에서의 함수란 $y = f(x)$ 꼴로 동일한 input x에 대해서 항상 동일한 output y를 가지는 것을 말한다. 이 개념을 프로그래밍으로 옮긴 것이 **순수함수**이다. 함수의 실행이 전체 프로그램의 실행에 영향을 미치면 안된다. 즉, 함수 내부에서 외부의 값을 변경하는 것과 같은 Side Effect(부수효과)가 나면 안된다.
![image.png](https://i0.wp.com/www.techdiscuss.net/wp-content/uploads/2020/08/Pure-functions.png?fit=666%2C507&ssl=1)

## 🧊 함수형 프로그래밍의 정의
함수형 프로그래밍(Functional Programming)은 코드를 작성하는 스타일 중 하나이다. 즉, 함수형 프로그래밍으로 설계된 언어가 따로 존재하지만(Clojure, Scala), 우리가 사용하는 모든 언어에 적용할 수 있으며 프로그래밍에 발생할 수 있는 여러 문제들을 해결할 수 있다.
다시 정리하면, **함수형 프로그래밍**은 함수를 사용해서 데이터 처리의 참조 투명성을 보장하고, 상태와 가변 데이터 생성을 피하는 프로그래밍 패러다임이다. 
>객체지향은 동작하는 부분을 캡슐화해서 이해할 수 있게 하고, 함수형 프로그래밍은 동작하는 부분을 최소화해서 코드 이해를 돕는다. (마이클 페더스‘레거시 코드 활용 전략’)

![programming history](https://dinfree.com/assets/blog-img/java-fp-1.png)

## 함수형 프로그래밍의 특징
![](https://www.xenonstack.com/hubfs/xenonstack-functional-programming.png)
### 불변성 immutable
부수효과(Side Effect)는 **함수의 반환값이 아닌, 외부의 상태**에 영향을 미치는 것을 말하는데 이런 부수효과가 발생하지 않도록 함수를 작성해야 한다. **불변성**은 **상태가 변하지 않는 것**을 의미하며, 메모리에 저장된 값을 변경하는 모든 행위에 대해 적용된다. 불변성을 지킨다면, *무분별한 상태의 변경을 막을 수 있고 상태가 어디서 변경되었는지 추적하기에도 용이*하다. 실제 개발에서 불변성을 지키는 코드를 작성하기 위해서는 **전역 변수의 사용을 줄이고 객체나 배열의 값을 변경해야 할 때는 함수 내에서 해당 object와 동일한 형태를 가지는 object를 생성하여 변경**하면 된다.
아래는 순수하지 않은 함수와 부수효과가 있는 함수가 사용된 코드이다.
```kotlin
var z = 10 // 전역변수
fun impureFunction(x: Int, y: Int): Int = x + y + z //순수하지 않은 함수
fun withSideEffect(x: Int, y: Int) : Int {
    z = y
    return x + y
} // 부수효과가 있는 함수 (함수 밖의 전역변수인 z를 변경하고 있음)
```
### 참조 투명성 referential transparency
참조 투명성이란, **프로그램의 변경 없이 어떤 표현식을 값으로 대체할 수 있다**는 뜻이다. 수학의 함수로 설명하자면 순수함수 $f(x)$가 $y$를 반환한다면, $f(x)$는 $y$로 대체될 수 있는 것이다. 참조 투명성을 만족하는 코드는 예외가 사라져서 간결해지고 버그가 발생할 가능성이 낮아진다. 멀티쓰레드 코드에서도 쓰레드 안전성에 대한 고민을 덜어준다.
### 일급 함수 first-class Function
객체지향언어에서는 일급 객체(first-class object)를 지원하는데, 일급 객체는 다음 세 가지 조건을 만족시킨다.
- 객체를 함수의 매개변수로 넘길 수 있다.
```kotlin
fun objectToParam(any: Any) {...}
```
- 객체를 함수의 반환값으로 돌려 줄 수 있다.
```kotlin
fun objectToReturn(any: Any) {
    return Any()
}
```
- 객체를 변수나 자료구조에 담을 수 있다.
```kotlin
var anyList: List<Any> = listOf(Any())
```
위 일급 객체의 개념을 그래도 함수에 적용한 것이 일급 함수이다. 프로그래밍 언어가 함수를 first-class citizen 취급하는 것을 말한다. Java는 일급 함수 언어가 아니지만, Kotlin은 일급 함수 언어이다. 일급함수를 사용한다면 추사화와 재사용성을 높일 수 있다.
### 커링 Currying

### 리팩토링 Refactoring

## ⚓️ 명령형 Imperative vs 선언형 Declarative
명령형 프로그래밍과 선언형 프로그래밍도 프로그래밍 패러다임 중 하나이다. 이 둘은 서로 반대되는 개념이기 때문에 차이점을 분석하면서 공부해보자
>“**Imperative programming** is like **how** you do something, 
>and **declarative programming** is more like **what** you do, or something.”

즉, 명령형 프로그래밍은 **어떻게** 하는가에 초점을 맞췄다면, 선언형 프로그래밍은 **무엇을** 하는가에 초점을 맞춘 것이다. 그럼 이제 각각을 자세히 비교해보자

![paradigm](https://www.ionos.com/digitalguide/fileadmin/DigitalGuide/Schaubilder/programming-paradigms.png)
### 명령형 프로그래밍
절차적 프로그래밍이라고도 한다. 얻으려는 것에 대해 어떤 방법으로 접근할 것인지, 그 절차적인 방법을 작성하는 방법이다. 즉, 알고리즘을 명시하지만 목표는 명시하지 않는다. 우리가 배열 알고리즘 문제를 풀 때 반복문으로 각 인덱스에 접근하여 상태를 변경하던 것이 이 방식에 해당한다.
```kotlin
fun add(items: List<Int>) : Int {
    var result: Int = 0
    for (i in items)
        result += i
    return result
}
```