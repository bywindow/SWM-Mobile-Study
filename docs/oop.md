<!-- title: [mobile-study] week1. 객체지향 -->
# OOP 전의 프로그래밍 방식
---
### 절차적 프로그래밍 (Procedural Programming)
- 초기 프로그래밍의 방식이며, 명령형 프로그래밍의 일종이다.
- `절차적` 이라는 단어에 집중하지 말고, `Procedure` 자체에 집중해야 한다.
- 단순이 순차적인 명령 수행이 아니라, 루틴, 서브루틴, 메소드, 함수 등을 이용한 프로그래밍이다.
- Top-down 방식
- 함수호출(procedure call)을 통해서 추상화를 얻고 재사용성을 높이는 것이 목적이다.
- OOP와 반대의 개념이 아니라, 프로그래밍의 관점이 procedure에서 object로 확장된 것이다.
#### 장점
- 컴퓨터의 처리 구조와 유사하여 실행 속도가 빠르다
- 모듈화와 구조화 용이
- 같은 코드를 복사하지 않고, 다른 위치에서 호출하여 사용할 수 있다
#### 단점
- 코드가 길어지면 가독성이 떨어져 이해하기 어렵다
- 유지 및 보수가 어렵다
- 코드 수정이 어렵다 (정해진 순서대로 입력을 해야하는데 순서를 바꾸면 결과값 보장이 안된다)

#### OOP 등장 배경
- 소프트웨어의 규모가 커지고 복잡해지면서 절차 지향 프로그래밍 방식에서는 품질이 낮아졌다
- 함수는 데이터의 처리 방법을 구조화했을 뿐, 데이터 자체는 구조화하지 못했다. 그래서 데이터의 구조 방식에 대한 고민이 많아졌다.
- JavaScript 코드로 예를 들면,
  ```javascript
  const player = {
    name: "son",
    age: 29,
    position: "FW",
  }
  ```
  라는 객체를 만든다고 했을 때, 위와 같은 코드를 작성할 수 있다.
  오직 한 명의 `player`만 만든다고 할 때는 이렇게 해도 문제가 없지만, 만약 player 수가 많아진다고 한다면...?
  ```javascript
  const playerOne = {
    name: "son",
    age: 29,
    position: "FW",
  }

  const playerTwo = {
    name: "kane",
    age: 28,
    position: "FW",
  }

  const playerThree = {
    name: "Lloris",
    age: 35,
    position: "GK",
  }
  ```
  이런 형태로, 같은 속성(property)을 가지지만 데이터만 다른 여러 개체들이 생겨날 것이다. 실수로 `position`을 postion으로 잘못 작성했다면 해당 부분을 찾아 일일이 수정하는 과정을 거쳐야 한다. 고로 매우 비효율적인 코드이다. 또한 데이터의 구조에 대한 고민이 없다.

# OOP
---
위와 같은 문제들을 해결하기 위해, **객체 지향 프로그래밍(object-oriented programming)**이라는 개념이 등장했고, 그렇게 해서 사용된 것이 `Class`이다.
## Class
- 객체(object)를 위한 팩토리 같은 것이다.
- 같은 속성을 갖고 있지만 데이터가 다를 경우에 일종의 구조(설계도)를 만들어준다.
- **Kotlin**에서는 다음과 같이 사용된다.
  ```kotlin
  class Example {
      companion object {
          fun main(args: Array<String>) {
              // TODO
          }
      }
  }
  ```
  >**Kotlin은 Java의 `static` 키워드를 지원하지 않는다.**
  >그 대신 pakage 수준의 최상위 함수와 객체 선언을 통해 `static` 메서드 역할을 대신한다.
  >위의 코드에서는 `companion object` 키워드를 통해 class 안의 private 멤버에 접근할 수 있는 static 메서드를 선언한 것이다.
  
- 이렇게 `class`를 사용하면 이전과 같이 코드를 무수히 많이 복사할 필요가 없다!

그럼, kotlin에서 class가 어떻게 사용되는지 알아보자.

### Kotlin에서의 Class
