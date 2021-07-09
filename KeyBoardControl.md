# 키보드컨트롤
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
