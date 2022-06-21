<!-- title : [Android] MVVM -->
# 아키텍처
<!-- <blockquote class="callout callout_default" style="background: #7B9CCF; color: black; padding: 10px">
  <h6>💡 본 내용은 SWM 멘토링을 기반으로 작성</h6>
</blockquote> -->
`Architecture`란, 말 그대로 설계도이다. 일반적인 안드로이드 앱에는 Activity, Fragment, Service, Contents Provider, Broadcast Receiver를 비롯하여 여러가지의 App Component가 포함된다. 사용자는 내가 만든 앱만 사용하는 것이 아니다. 예를 들어 카카오톡을 하던 중에 네이버에 검색을 할 수 있고, 유튜브로 동영상을 시청할 수도 있다. 이렇게 사용자가 짧은 시간동안 여러 앱과 상호작용할 수 있는 점을 고려하여, 앱은 사용자 중심의 다양한 워크플로 및 작업에 맞게 조정될 수 있어야한다.
더 자세한 내용은 추후에 `Clean Architecture`를 공부할 때 더 알아보도록 하고, 오늘은 MVVM 및 아키텍처 변천사를 둘러보는 시간이다.
그럼 먼저, View와 ViewModel에 대해서 알아보자.

# View