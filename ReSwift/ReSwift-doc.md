# ReSwift-doc

ReSwift 폴더 내의 전반적인 내용과 `.md` 파일로 담기에는 짧은 내용들을 정리합니다.

## Flux의 이해

- Redux Pattern은 Flux에서 온 것이며, 이는 웹 어플리케이션 개발에서 최초로 시작된 개념. (FaceBook에서 개발함)
- [참고문헌-Flux로의 카툰 안내서](http://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/)


### 단방향 데이터 흐름 아키텍처
![Flux Architecture](https://github.com/yuniithings/TIL/blob/master/ReSwift/images/ReSwift-doc-Flux.png?raw=true)

* #### 액션 생성자 (Action Creator)

* #### 디스패처 (Dispacher)

    * Callback을 등록하는곳
    * 액션을 보낼 필요가있는 모든 Store를 가지고있다.
    * 동기적(Synchronously)으로 실행
    * Store가 특정 Action만을 구독하지 않고, 모든 Action을 받은 후 처리할지에 대해 결정함

* #### 스토어 (Store)

    * Application내의 모든 State와 그 Logic을 가지고있음
    * 모든 State에 대한 처리는 Store가 담당한다.

* #### 컨트롤러 뷰(Controller View)와 뷰(View)

    * State를 호출한다.
    * User에게 데이터를 보여줌
    * User에게 정보를 받음
    * View Rendering


## Redux를 적용하게 된 7가지 이유.

- [참고문헌-채널 iOS에 Redux를 적용하게 된 7가지 이유.](http://blog-kr.zoyi.co/channel-ios-redux/)
- ReSwift를 시작 전에 반드시 읽는것을 추천합니다.

### 친숙한 MVC 패턴

- 예제와 튜토리얼에 자주 등장한다.
- Xcode에서도 기본으로 ViewController로 생성된다.
`software architectural design pattern은 사실 MVC가 최고`

### MVC의 단점이 드러날때

- 복잡도가 높아질 경우
- 코드의 양이 많아질 경우
`위와 같은 상황에서 생선상과 가독성을 보장받지 못함`

### MVC 패턴의 문제점!?

![MVC01](https://github.com/yuniithings/TIL/blob/master/ReSwift/images/ReSwift-doc-MVC01.png?raw=true)

View -> (event) -> Controller -> (update) -> Model

Model -> (notify) -> Controller -> (render) -> View

`각각의 역할은 명확하다. 다만..`

객체간의 어떤 방향으로 커뮤니케이션 해야 하는지 강제되지 않기 때문에 파생되는 패턴들이 다양하다.

![MVC02](https://github.com/yuniithings/TIL/blob/master/ReSwift/images/ReSwift-doc-MVC02.png?raw=true)

`커뮤니케이션의 방향이 달라지는 패턴`

![MVC03](https://github.com/yuniithings/TIL/blob/master/ReSwift/images/ReSwift-doc-MVC03.png?raw=true)

`MVP, MVVM 패턴도 MVC에서 커뮤니케이션의 방향이 달라지면서 파생된 패턴이다.`

MVC 패턴으로 대규모 어플리케이션을 개발하게 된다면 특정 이벤트가 체인 형식으로 발생되고, 그 경로를 일일이 추적하는데 많은 시간이 소요되는 구조를 가지게 된다.

이 문제의 원인은 MVC 패턴의 장점인 `유연성`과 `양방향 커뮤니케이션`에서 발생하는 문제다. 그로 인해 `생산성`과 `가독성`의 저해가 발생하게 된다.

그래서 이에 대한 방안으로 Redux 패턴 도입을 고민하게 되었다.


### Redux의 3가지 법칙

- `Single source of truth` — 어플리케이션의 전체 상태(State, 또는 데이터)는 트리 형태의 하나의 저장소(Store)에 저장된다.
- `Change with pure functions` — 상태 트리를 변경하는 리듀서(Reducer) 는 순수 함수(pure function)여야 한다.
- `Read-only states` — 상태는 오직 액션(혹은 Event?)으로만 변화가 가능하다.

`Redux는 한 개의 상태 저장소를 가지고 있고 그 안에 있는 데이터만을 신뢰할 수 있으며, 저장소의 상태는 오직 순수 함수인 리듀서를 통해서만 변화가 가능하다.`


### Redux의 커뮤니케이션 Flow

![Redux](https://github.com/yuniithings/TIL/blob/master/ReSwift/images/ReSwift-doc-Redux01.png?raw=true)

1. 이벤트가 뷰에서 생성되면 그에 해당되는 액션을 통해 알림
2. 액션은 특정 리듀서에서 처리
3. 리듀서는 액션에 따라 저장소를 업데이트한다.
4. 저장소에 변화가 오면 구독하고 있는 모든 객체에 알린다.
` observable 패턴도 알아야한다!`

`나머지 내용은 해당 Post의 핵심 내용이기 때문에 직접 Post를 방문하여 보고 읽어야 합니다!`
### Redux vs. MVC
### 채널 데스크 iOS에 Redux를 적용하게 된 이유
### ReSwift 도입 시 주의 할 점

---
`작성할 항목들을 정리합니다.`
## ReSwift 의 장점

## ReSwift 의 단점

## ReSwift 를 사용하는 이유
