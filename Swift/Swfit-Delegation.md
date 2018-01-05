# Swfit-delegation

델리게이션과 콜백을 설명합니다.


## 간단한 textField 델리게이션
`textField` 개체에 델리게이션을 추가합니다.

`control + drag`로 노란원의 `ViewController`로 드래그하여 `Outlet-delegate`를 선택합니다.

![delegate](https://github.com/yuniithings/TIL/blob/master/Swift/images/Swift-delegate01.png?raw=true)

스토리보드와 연결된 `ViewController`로 돌아가 함수를 작성합니다.<br/>
`textField`에 값을 입력 시 `nil`일 경우 허용하지 않는 함수 예제입니다.

`UITextFieldDelegate`를 추가적으로 상속받아야 합니다.
```swift
func textField(textField: UITextField,
        shouldChangeCharactersInRange range: NSRange,
        replacementString string: String) -> Bool {


    print("Current text: \(textField.text)")
    print("Replacement text: \(string)")

    // return true


    let existingTextHasDecimalSeparator
        = textField.text?.rangeOfString(".")
    let replacementTextHasDecimalSeparator
        = string.rangeOfString(".")

    if existingTextHasDecimalSeparator != nil &&
        replacementTextHasDecimalSeparator != nil {
        return false
    }
    else {
        return true
    }
}

```
