# Xcode-tip

Xcode와 관련된 tip을 기록합니다.

## Xcode 2가지 버전 이상 설치하기
[Xcode 버전별 다운로드](https://developer.apple.com/download/more/)<br/>
위의 링크로 접속 후 원하는 버전을 검색하여 설치한다.

이후 applications 폴더로 이동 후 이름을 변경해준다.

## Xcode 옛날버전에 iOS 버전 설정하기

Xcode 구버전으로 에뮬레이터가 아닌 연결된 나의 디바이스(`최신 iOS버전`)로 코드를 빌드 시 다음과 같은 오류가 발생할 수 있습니다.

![not disk image](https://github.com/yuniithings/TIL/blob/master/Xcode/images/xcode-tip-not-disk.png?raw=true)


빌드가 안되는 상황을 해결하기 위해,<br/>
최신버전의 Xcode에서 DeviceSupport 내의 OS 서포터들을 가져옵니다.

`finder`를 실행 후 `이동-폴더로 이동(Shift + Command + G)` 메뉴를 선택합니다.

나의 로컬에 설치된 Xcode 최신버전의 경로를 입력합니다.
`/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport`

![not disk image](https://github.com/yuniithings/TIL/blob/master/Xcode/images/xcode-tip-devicesupport.png?raw=true)

이곳에서 새로운 `finder`를 실행 후 오류 메세지가 나왔던 버전의 Xcode의 DeviceSupport로 이동합니다.

`/Applications/[appname].app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport`

`[appname]`은 당신이 설치 후 변경한 Xcode의 이름입니다.<br/>
저의 경우에는 `Xcode-7.3.1 입니다.`

Xcode를 다시 실행 후 빌드를 진행하면 Process 설정이 된 후, 빌드가 시작될 것입니다.
