<!-- title : [Android] 비동기 처리 -->
# 동기 vs 비동기
![](https://images.velog.io/images/dorazi/post/dadf63e9-5994-4967-bc3f-ca0bc173897c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-03-31%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.29.45.png)
## 동기(Synchronous)
사전 그대로 번역하면 '동시성의' 라는 의미이다. 즉, 요청과 결과가 동시에 일어나는 작업을 동기라고 한다. 동기적으로 작성된 프로그램은 수행하는 작업이 완료될 때까지 다른 작업을 하지 않고 기다린다. 

---
## 비동기(Asynchronous)
동기와 반대로, 동시에 일어나지 않는 것을 의미한다. 그러므로 비동기적으로 작성된 프로그램은 수행하는 작업의 완료와 상관없이 계속해서 다른 작업도 수행할 수 있다. 
Android는 `UI thread`라고 불리는 메인쓰레드가 UI 작업을 관리하고 처리한다. UI thread는 사용자의 앱 사용성에 직결된 요소이기 때문에 항상 막힘없이 처리되어야 하는데, 만약 이 메인쓰레드에서 네트워크나 DB로부터 자료를 받아오는 작업을 수행한다면 어플리케이션은 `ANR`(Application Not Responding) 상태가 될 것이다. 따라서 비동기라는 개념이 중요하며, 여러 작업들을 각각의 쓰레드에 나눠서 block 없이 수행할 수 있도록 설계해야 한다.

### 안드로이드에서 비동기 처리를 위한 방법
Android에서 이런 비동기 처리를 해주기 위해 `RxJava`, `RxKotlin`, `Coroutine` 같은 방법이 존재한다. 이 포스팅에서는 모두 살펴보기 보다는 `Coroutine` 하나만 공부해보자.

---

# Coroutine
> 💡 코루틴(Coroutine)은 구글에서 공식적으로 `AsyncTask`를 deprecated 선언한 후 대체 기술로 사용할 것을 추천하고 있다.

코루틴은 비동기적으로 실행되는 코드를 간소화하기 위해 Android에서 사용할 수 있는 동시 실행 설계 패턴이다.