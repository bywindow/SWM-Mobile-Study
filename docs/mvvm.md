<!-- title : [Android] MVVM -->
# **아키텍처**
<!-- <blockquote class="callout callout_default" style="background: #7B9CCF; color: black; padding: 10px">
  <h6>💡 본 내용은 SWM 멘토링을 기반으로 작성</h6>
</blockquote> -->
`Architecture`란, 말 그대로 설계도이다. 일반적인 안드로이드 앱에는 Activity, Fragment, Service, Contents Provider, Broadcast Receiver를 비롯하여 여러가지의 App Component가 포함된다. 사용자는 내가 만든 앱만 사용하는 것이 아니다. 예를 들어 카카오톡을 하던 중에 네이버에 검색을 할 수 있고, 유튜브로 동영상을 시청할 수도 있다. 이렇게 사용자가 짧은 시간동안 여러 앱과 상호작용할 수 있는 점을 고려하여, 앱은 사용자 중심의 다양한 워크플로 및 작업에 맞게 조정될 수 있어야한다.
더 자세한 내용은 추후에 `Clean Architecture`를 공부할 때 더 알아보도록 하고, 오늘은 MVVM 및 아키텍처 변천사를 둘러보는 시간이다.
그럼 먼저, View와 ViewModel에 대해서 알아보자.

---
# View
view는 이전에 Layout에 대해 공부할 때 알아봤으므로, UI 요소를 표시하며 사용자가 발생한 이벤트를 받는 역할을 한다는 정도만 정리하고 넘어간다.

---

# ViewModel
`ViewModel` 클래스는 수명주기를 고려하여 UI 관련 데이터를 저장하고 관리하도록 설계된 것이다. 따라서 화면 회전과 같이 구성을 변경해야 될 때도 데이터를 유지할 수 있다. UI Controler(Activity, Fragment)는 UI 데이터를 표시하거나, 사용자 작업에 반응하거나, 권한 요청과 같은 운영체제 커뮤니케이션을 처리하는 역할을 하는데 이러한 UI Controler에 네트워크로부터의 데이터로드 같은 작업까지 맡기게 된다면 클래스 하나가 너무 팽창해버려서 테스트 작업도 어려워진다. 따라서 ViewModel 클래스를 통해 UI Controler 로직에서 View 데이터 소유권을 분리하는 방법이 효율적이다.
## ViewModel 구현
- viewmodel 디렉토리를 만든다.
- `ViewModel` 클래스를 상속 받는 클래스를 만든다.
- Activity나 Fragment 대신 데이터를 보관하도록 책임을 할당한다.
- `ViewModel` 객체가 보유한 데이터는 다음 Activity나 Fragment 인스턴스에서 바로 사용가능.
```kotlin
@HiltViewModel
class GardenPlantingListViewModel @Inject internal constructor(
    gardenPlantingRepository: GardenPlantingRepository
) : ViewModel() {
    val plantAndGardenPlantings: LiveData<List<PlantAndGardenPlantings>> =
        gardenPlantingRepository.getPlantedGardens().asLiveData()
}
```
- Activity에서는 위에서 정의한 클래스형의 객체를 생성하여 사용한다.
- sunflower 코드 중 일부이며, 사용자가 `Add Plant`한 데이터를 보관했다가 사용한다.
- 실제로 Log를 찍어보면, result에 해당 데이터가 담겨있는 것을 확인할 수 있다.
```kotlin 
class GardenFragment : Fragment() {
    private lateinit var binding: FragmentGardenBinding
    private val viewModel: GardenPlantingListViewModel by viewModels()
    ...
    private fun subscribeUi(adapter: GardenPlantingAdapter, binding: FragmentGardenBinding) {
        viewModel.plantAndGardenPlantings.observe(viewLifecycleOwner) { result ->
            binding.hasPlantings = result.isNotEmpty()
            adapter.submitList(result) {
                // At this point, the content should be drawn
                activity?.reportFullyDrawn()
            }
        }
    }
    ...
}
```
## ViewModel 수명 주기
ViewModel 객체의 범위는 ViewModel을 가져올 때 ViewModelProvider에 전달되는 Lifecycle로 지정된다. Activity가 끝날 때까지, Fragment가 분리될 때까지 메모리에 남아있다.
![](https://developer.android.com/images/topic/libraries/architecture/viewmodel-lifecycle.png?hl=ko)

---

# 아키텍처 변천사
## MVC
처음에는 AOS와 iOS에 MVC를 적용했다.
한 클래스가 모든 로직을 갖고 있다. 컨트롤러는 사용자 작업을 적용해야 할 뷰와 모델을 알고 있고, input이 발생할 때 변동되어야 할 것이 무엇인지 알려준다.
### MVC의 단점
- 뷰의 로직과 컨트롤러의 로직이 하나의 액티비티 안에 모두 존재하므로 **유지보수가 어렵다**
- 뷰와 모델 사이의 강한 결합, 즉 **커플링**이 발생한다
- 한 클래스에서 M-V-C 모두를 처리하게 된다
![](https://magi82.github.io/images/2017-2-24-android-mvc-mvp-mvvm/mvc.png)

클래스의 의존성을 떨어뜨리기 위한 노력이 제기되었고, 그렇게 해서 나온 아키텍처가 MVP이다.
## MVP
모델과 뷰가 서로를 모르는 구조이다.
사용자 입력을 뷰에서 받고, 모델과 뷰는 각각 프레젠터와 상호작용한다.
> **Presenter**
> 프레젠테이션 로직 : View에 실제로 변화를 발생시키는 트리거 역할
> 비즈니스 로직 : 서버에 리퀘스트를 보내고, 그것을 후처리하는 트리거 역할

뷰와 프레젠터가 일대일 관계인 것이 한계가 되어 MVVM 패턴이 나오게 되었다. Activity에 코드를 늘리지 않고 Observer 패턴을 이용해서 데이터를 갖고 있다가 xml에서 직접 데이터를 바꿔주는 `데이터바인딩` 패턴이 필요해졌다.

### MVP 단점
- View-Presenter 간의 의존성이 강해서 하나의 뷰에 계속 기능이 붙으면 프레젠터에 로직이 계속 추가된다
- 매번 Presenter를 만들어야해서 필요한 클래스 개수가 많아진다
![](https://magi82.github.io/images/2017-2-24-android-mvc-mvp-mvvm/mvp.png)

## MVVM
하나의 ViewModel에 여러개의 View가 붙는 구조이다.
모양은 다르지만, 기능은 똑같이 작용하는 비즈니스 로직을 가졌다면 MVVM 패턴이 효과적이다.
View와 ViewModel간에 의존성이 전혀 없다. view에 사용자의 입력이 들어오면 그것을 view가 viewmodel에 명령을 내리게 되고, viewmodel은 필요한 데이터를 model에 요청한 후 그것을 받아 가공하여 저장한다. 이렇게 변수의 값을 할당하면, 옵저버 패턴을 통해 view에 자동적으로 데이터가 갱신된다.
### MVVM 단점
- viewmodel을 재사용하기 위해 설계하는 것이 어렵다
- 옵저버 패턴에서 메모리 누수가 나기 쉽다
  - 홈버튼 작용 시 시스템 메모리가 다른 프로그램을 위해 가비지컬렉션으로 메모리를 정리해야되는데 메모리를 계속 잡아먹고 있는다
- 혹시라도 RxJava를 쓰게 된다면 타임아웃에 신경을 써서, 서버의 요청을 받은 후 기다리고 있는 것을 모두 클린시켜야 한다.

![](https://magi82.github.io/images/2017-2-24-android-mvc-mvp-mvvm/mvvm.png)