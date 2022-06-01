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
위와 같은 문제들을 해결하기 위해, **객체 지향 프로그래밍(object-oriented programming)**이라는 개념이 등장했다. 그렇게 해서 사용된 것이 `Class`이다.
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
#### 생성자
- Kotlin은 JavaScript와 같이 constructor 라는 키워드를 통해 생성자를 선언한다.
  ```kotlin
   class Player {
       constructor (name: String, age: Int, position: String) {
           this.name = name
           this.age = age
           this.position = position
       }
       var name: String = ""
       var age: Int = 0
       var position: String = ""
   }
   ```
- `constructor` 키워드를 클래스 이름 옆에 선언할 수 있다.
  ```Kotlin
  class Player constructor (name: String, age: Int, position: String) {
      var name: String = name
      var age: Int = age
      var position: String = position
  }
  ```
- `constructor` 키워드를 생략할 수 있다.
  ```kotlin
  class Player (name: String, age: Int) {
      var name: String = name
      var age: Int = age
      var position: String = position
  }
  ```
- `constructor` 키워드를 통한 생성자 오버로드로 특정 property에 대해 default 값을 선언할 수 있다.
  ```kotlin
  class Player (name: String, age: Int, position: String) {
      constructor(name: String) {
          this.name = name
          this.age = age
          this.position = "MF" //position 속성의 default 값을 "MF"로 설정
      }
      var name: String = name
      var age: Int = age
      var position: String = position
  }
  ```
  위와 같이 선언해도 되지만,
  ```kotlin
  class Player (var name: String = "anonymous", var age: Int = 20, var position: String = "MF")
  ```
  이렇게 한 줄의 코드로 작성할 수도 있다. parameter dafault value를 사용함으로써 Boilerplate Code(상용구 코드)가 사라진 것을 알 수 있다.
  이제 여러 객체들을 생성해보며, 어떻게 작동하는지 알아보자.
  ```kotlin
  val playerOne = Player() //{ name: "anonymous", age: 20, position: "MF" }
  val playerTwo = Player("Son") //{ name: "Son", age: 20, position: "MF" }
  val playerThree = Player("Son", 29) //{ name: "Son", age: 29, position: "MF" }
  val playerfour = Player(age=29, name="Son", position="FW") //{ name: "Son", age: 29, position: "FW" }
  ```
  Java와 달리 `new` 키워드를 사용할 필요가 없고, parameter로 속성을 명시함으로써 순서가 달라져도 상관없다.
## 특징
### 캡슐화
- **접근제한자**를 통한 정보 은닉을 통해 여러가지 형태의 객체를 디자인한다. ex) [singletone](https://kotlinworld.com/166)
- public > protected | internal > private
  |접근제한자|같은 class|같은 module|다른 module|제한없음|
  |:-------:|:--------:|:---------:|:--------:|:-----:|
  |public| O | O | O | O |
  |protected| O | 상속 받았을 때만 가능 | 상속 받았을 때만 가능 | X |
  |internal| O | O | X | X |
  |private| O | X | X | X |
  >🎈 **용어 정리**
  >**project** : 최상위 개념. 여러 module을 가질 수 있음
  >**module** : 여러 package를 가질 수 있음
  >**package** : 여러 member, function, class를 가질 수 있음
  >**class** : member, function을 가질 수 있음
#### public
`public`은 기본 접근 제한자이며, 모든 곳에서 접근할 수 있다.
#### protected
`protected`는 같은 class 안에서는 언제든지 접근 가능하지만, 같은 module의 다른 class 안에서는 상속을 받았을 때만 접근 가능하다.
```kotlin
// Kotlin에서 open 키워드는 상속 가능한 class라는 것을 명시하는 키워드이다. 기본은 final이다.
open class Test {
    protected fun printTest() = println("test")
}
```
이런 class가 있을 때, 올바른 `protected` 접근법은
```kotlin
class ChildTest : Test() {
    fun main(){
        printTest()
    }
}
```
위의 코드와 같이 Test() 클래스를 상속 받은 후 접근해야한다.
```kotlin
class ChildTestError {
    val test = Test()
    fun main() {
        test.printTest()
    }
}
```
반면, 위와 같이 인스턴스를 생성해서 접근한다면, `Cannot access 'printTest': it is protected in 'Test'`라는 에러문이 뜬다.
#### internal
`internal` 키워드가 붙은 class member는 해당 클래스가 같은 모듈 안에서 인스턴스화 되었을 때만 접근가능하다.
- class `TestUtil`과 kotlin 파일 `Test.kt`가 같은 모듈(같은 패키지) 안에 있을 때
    ```kotlin
    // TestUtil
    class TestUtil {
        internal fun printInternal() = println("printInternal")
        fun printPublic() = println("printPublic")
    }
    ```
    ```kotlin
    // Test.kt
    val testUtil = TestUtil()

    fun printTest() {
        testUtil.printInternal() // 접근 가능
        testUtil.printPublic() // 접근 가능
    }
    ```
- class 앞에 `internal` 키워드가 붙고, 같은 모듈 안에서 접근할 때
    ```kotlin
    internal class TestUtil {
        internal fun printInternal() = println("printInternal")
        fun printPublic() = println("printPublic")
    }
    ```
    ```kotlin
    // Test.kt
    val testUtil = TestUtil() // 접근 불가
    internal val testUtil = TestUtil() // 접근 가능
    ```
    `internal` 접근제한자가 붙은 class를 인스턴스화 하는 변수는 `internal`이나 `private` 키워드를 가져야한다. 만약 `public`이나 `protected` 수준의 val로 접근하게 된다면 모듈의 가시성이 깨지기 때문이다.
- class `TestUtil`과 kotlin 파일 `Test.kt`가 다른 모듈에 있을 때
    ```kotlin
    // mylibrary라는 새로운 모듈안에 Test.kt가 위치할 때
    import com.example.sunflower_clone.TestUtil

    val testUtil = TestUtil()

    fun printTest() {
        testUtil.printInternal() // 접근 불가
        testUtil.printPublic() // 접근 가능
    }
    ```
    다음과 같은 상황에서는 printInternal() 멤버 함수에 접근 불가하고, `Cannot access 'printInternal': it is internal in 'TestUtil'` 에러 메시지가 나온다.
#### private
같은 `class` 또는 같은 `.kt` 파일 안에서만 접근 가능하다.



### 상속
- 자식 클래스는 부모 클래스의 properties를 상속 받을 수 있고, 추가적으로 다른 properties를 가질 수 있다.
- 키워드로는 `open`, `super`, `override`, `private`이 있다.
#### open
- 기본적으로 Kotlin에서 모든 클래스는 public인 동시에 final이므로, 상속 받기 위해서는 `open` 키워드를 사용해야한다.
#### super
- 상위 클래스의 메서드, 프로퍼티, 생성자를 사용하는 키워드이다.
- 비슷한 개념으로 `this`가 있는데, 현재 클래스의 메서드, 프로퍼티, 생성자를 사용하는 키워드이다.
#### override
- 부모 클래스의 메소드를 재정의 하는 것이다.
- 메소드의 이름, parameter, 타입이 모두 동일해야한다.
- `open` 키워드가 붙은 메소드만 override가 가능하다.
#### private
- 선언된 클래스 안에서만 접근할 수 있는 멤버를 만들 때 사용된다
```kotlin
open class Mammal {
    open var legs: Int = 0
    open var eyes: Int = 0
    private var name: String = "Mammal" // 클래스 안에서만 접근 가능

    open fun breathing() {
        println("$name is breathing") // name 변수에 접근 가능
    }

    open fun eating() {
        println("$name is eating") // name 변수에 접근 가능
    }
}

class Human(var name: String): Mammal() {
    var iq: Int = 0
    // override 키워드를 통해 부모 클래스의 변수값을 바꾼다
    override var eyes: Int = 2 
    override var legs: Int = 2
    // override 키워드를 통해 부모 클래스의 함수를 바꾼다
    override fun breathing() {
        super.breathing() // super 키워드를 통해 부모 클래스의 breathing 메서드를 호출한다
        println("Human $name is breathing")
    }
}

class TestMammal {
    val newMammal: Mammal = Mammal()
    val newHuman: Human = Human("philip")
    fun main() {
        println(newMammal.name) // error: Cannot access 'name': it is private in 'Mammal'
        newHuman.iq = 100 // public이 기본이므로 접근 가능
        newHuman.breathing() // 접근 가능
        newHuman.eating() // Human 클래스 안에는 선언되어 있지 않지만, 부모 클래스에 있으므로 접근 가능
    }
}
```
