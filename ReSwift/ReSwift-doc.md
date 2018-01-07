# ReSwift-doc

ReSwift 폴더 내의 전반적인 내용과 `.md` 파일로 담기에는 짧은 내용들을 정리합니다.

## Flux의 이해

- Redux Pattern은 Flux에서 온 것이며, 이는 웹 어플리케이션 개발에서 최초로 시작된 개념. (FaceBook에서 개발함)
- [참고문헌-Flux로의 카툰 안내서](http://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/)


### 단방향 데이터 흐름 아키텍처
![Flux Architecture](https://github.com/yuniithings/TIL/blob/master/ReSwift/images/ReSwift-Flux.png?raw=true)

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



---
`작성할 항목들을 정리합니다.`
## ReSwift 의 장점

## ReSwift 의 단점

## ReSwift 를 사용하는 이유
