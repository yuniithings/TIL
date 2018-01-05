# Swfit-View

View와 View 계층구조를 설명합니다.
더 있겠죠?


## 계층 구조를 가진 View
```swift
override func viewDidLoad() {
    super.viewDidLoad()

    let firstFrame = CGRect(x: 160, y: 240, width: 100, height: 150)
    let firstView = UIView(frame: firstFrame)
    firstView.backgroundColor = UIColor.blueColor()
    view.addSubview(firstView)

    let secondFrame = CGRect(x: 20, y: 30, width: 50, height: 50)
    let secondView = UIView(frame: secondFrame)
    secondView.backgroundColor = UIColor.greenColor()
    view.addSubview(secondView)

    // 이 코드의 유무가 secondView를 firstView의 하위 View가 되게 해준다.
    firstView.addSubview(secondView)


}
```
