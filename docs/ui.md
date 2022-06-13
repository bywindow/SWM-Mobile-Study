<!-- title: UI : Layout -->
> 📘 **Info**
> 
> [Android developers](https://developer.android.com/guide/topics/ui?hl=ko)


# 🧨 UI?
---
**UI**는 앱의 사용자가 상호작용 할 수 있는 모든 것을 의미한다. Android에서는 **UI Components**(레이아웃 객체, UI Control)를 미리 빌드된 형태로 제공하여 앱의 그래픽 UI를 빌드하는 데에 사용한다. 또한 대화상자, 알림, 메뉴를 위한 다른 UI모듈도 제공한다.

# 📐 Layout
Android에서 UI의 구조를 정의하는 것이 레이아웃이다. 레이아웃의 모든 요소는 View와 ViewGroup 객체의 계층구조를 사용하여 빌드된다. Activity에서 setContentView() 메서드를 호출하면, Activity는 시스템으로부터 화면에 UI를 그려라 라는 명령을 받게 된다. 그때 root에 있는 ViewGroup부터 드로잉 요청을 전달하게 되고, 해당 요청을 받은 ViewGroup은 자식노드로 그것을 전달한다.![](https://developer.android.com/images/viewgroup_2x.png?hl=ko)

#### View
View는 `android.view.View` 클래스이며, UI구성요소를 위한 기본 building block을 나타낸다. 스크린의 사각영역을 점유하고 구성요소를 드로잉하거나 이벤트 핸들링을 하는 역할이다. View의 이런 점에서 Widget과의 차이점이 무엇인가가 궁금할텐데, View는 위젯의 기본 클래스(basic class)를 의미한다.
> **Widget**
> 화면에 어떤 것을 그리는 모든 행위를 하는 View들의 집합이다.
> buttons, text fields와 같이 사용자와 상호작용하는 UI 구성요소를 만들 때 사용된다.
> widget에 해당하는 클래스로는 text, editText, Button, radioButton 같은 것들이 있다.

