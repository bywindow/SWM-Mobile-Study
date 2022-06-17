<!-- title: UI : view, widget, layout -->
> 📘 **Info**
> 
> [Android developers](https://developer.android.com/guide/topics/ui?hl=ko)


# 🧨 UI?
---
**UI**는 앱의 사용자가 상호작용 할 수 있는 모든 것을 의미한다. Android에서는 **UI Components**(레이아웃 객체, UI Control)를 미리 빌드된 형태로 제공하여 앱의 그래픽 UI를 빌드하는 데에 사용한다. 또한 대화상자, 알림, 메뉴를 위한 다른 UI모듈도 제공한다.

# 📐 Layout
Android에서 UI의 구조를 정의하는 것이 레이아웃이다. 레이아웃의 모든 요소는 View와 ViewGroup 객체의 계층구조를 사용하여 빌드된다. Activity에서 setContentView() 메서드를 호출하면, Activity는 시스템으로부터 화면에 UI를 그려라 라는 명령을 받게 된다. 그때 root에 있는 ViewGroup부터 드로잉 요청을 전달하게 되고, 해당 요청을 받은 ViewGroup은 자식노드로 그것을 전달한다.![](https://developer.android.com/images/viewgroup_2x.png?hl=ko)

## View
View는 `android.view.View` 클래스이며, UI구성요소를 위한 기본 building block을 나타낸다. 스크린의 사각영역을 점유하고 구성요소를 드로잉하거나 이벤트 핸들링을 하는 역할이다. View의 이런 점에서 Widget과의 차이점이 무엇인가가 궁금할텐데, View는 `Widget`과 `Layout`으로 나뉘고 View는 이러한 Widget의 기본 클래스(basic class)를 의미한다.
### Widget
화면에 어떤 것을 그리는 모든 행위를 하는 View들의 집합이다. View 중에서 일반적으로 컨트롤의 역할을 한다. buttons, text fields와 같이 사용자와 상호작용하는 UI 구성요소를 만들 때 사용된다.
widget에 해당하는 클래스로는 text, editText, Button, radioButton 같은 것들이 있다
#### 위젯이 사용되는 과정
1. 레이아웃에 사용하고자하는 위젯을 배치한다.
2. Activity가 실행되면 화면이 구성되고, 화면에 배치된 모든 View(위젯, 레이아웃)들은 객체로 생성된다.
3. 객체로 생성된 View 중에 필요한 위젯의 주소값을 가져와 코드로 이들을 통제한다.
    > 예전에는 findViewById를 사용했지만, 지금은 view Binding 기법을 많이 사용한다.
4. 이벤트가 필요하다면 추가적으로 코드를 구성하여 사용한다.
### Layout
앞서 말한 위젯이 눈에 보이는 View를 말하는 것이었다면, `Layout`은 눈에 보이지 않지만 화면의 틀을 잡아주는 역할을 한다. Android는 화면을 구성하기 위해 먼저 레이아웃을 배치하고 그 위에 다른 View들을 배치하게 된다. 또한 가장 밑에서 해당 화면의 전체적인 구조를 잡아주는 레이아웃을 `Parent`라고 하고, 그 위에 배치되는 View들을 `Child`라고 한다.

#### `<layout></layout>`
`<layout>`은 이번에 새롭게 안드로이드를 공부하면서 알게 된 태그이다.
데이터바인딩을 하기 위해 꼭 해당 레이아웃 파일의 root 태그로 적어야 하고, 그 뒤에 `<data>`와 View 태그를 위치시켜야한다.

#### Layout 종류
- ConstraintLayout
  - 부모나 다른 View와의 관계를 설정하여 위치를 결정하는 레이아웃 구조이다.
  - 실선제약조건(좌표로 거리 설정), 스프링제약조건(비율로 거리 설정)의 방법을 사용한다.
  - 구글에서 많이 쓰라고 권장하는 레이아웃이다 : 오버드로잉을 줄여주기 때문..!
  - RelativeLayout을 보다 유연하게 만든 레이아웃이다.
- LinearLayout
  - Box 모델이다.
  - 방향속성을 설정하여 한쪽 방향으로 차례로 View를 추가하면 화면을 구성한다.
  - 주로 깔끔하게 View를 정렬하거나 직관적인 화면구조를 그릴 때 사용한다.
- RelativeLayout
  - 부모나 다른 View와의 관계를 설정하여 배치한다.
  - ConstraintLayout을 사용하면서 더이상 권장하지 않는 레이아웃이다.
- FrameLayout
  - Single 모델이며, 가장 위에 있는 View나 ViewGroup을 보여준다.
  - 여러 View를 중첩한 다음, 사용자의 인터렉션으로 밑의 View를 보여줘야 할 때 사용한다.
- TableLayout
  - 격자모양의 배열을 사용해서 화면을 구성한다.
- ScrollView
  - View나 ViewGroup을 아이템으로 넣을 수 있다.
  - View의 배치보다는 View를 담고 있는 ViewGroup의 역할을 한다.