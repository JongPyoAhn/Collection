# 키보드컨트롤
## 1. 올렸다, 내렸다
- 설명은 [여기](https://github.com/JongPyoAhn/TodoList/blob/main/Explanation/TodoListViewController.md) 에 해놨음
- 참고 : inputViewBottom은 텍스트가 들어가 있는 View의 아래와의 간격(?)이 표시된 NSLayoutConstraint
```swift
 @IBOutlet weak var inputViewBottom: NSLayoutConstraint!
```

```swift
@objc private func adjustInputView(noti: Notification) {
        guard let userInfo = noti.userInfo else { return }
        guard let keyboardFrame = (userInfo[UIResponder.keyboardFrameEndUserInfoKey] as? NSValue)?.cgRectValue else {return}
        if noti.name == UIResponder.keyboardWillShowNotification {
            let adjustmentHeight = keyboardFrame.height - view.safeAreaInsets.bottom
            inputViewBottom.constant = adjustmentHeight
        }else {
            inputViewBottom.constant = 0
        }
    }
```


```swift
override func viewDidLoad() {
        super.viewDidLoad()
        
        NotificationCenter.default.addObserver(self, selector: #selector(adjustInputView), name: UIResponder.keyboardWillShowNotification, object: nil)
        NotificationCenter.default.addObserver(self, selector: #selector(adjustInputView), name: UIResponder.keyboardWillHideNotification, object: nil)
        }
```
## 2. 아무데나 클릭했을 때 키보드 내려가게 하기
 1) StoryBoard에서 TabGestureRecognizer를 전체뷰에 붙임(어디든 탭한 것을 인식 가능)
 2) IBAction으로 연결
 3) 아래코드 입력 (TextField에 관심없다, 그거안한다(?)라는 의미)
 ```swift
 @IBAction func tabBG(_ sender: Any) {
        inputTextField.resignFirstResponder()
    }
 ```
## 시뮬레이터 상에서 키보드가 안올라올 때 Command + ↑ + k 누르면 올라온다.
