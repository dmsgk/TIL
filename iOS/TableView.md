## TableView, TableViewCell

### TableViewCell 간 간격 띄우기

For your require layout do below steps.

1. Add `UIView` in you `cell` `contentView` with **Leading, Top, Trailing, Bottom Constraint. Like (15, 10, 15, 10)**
2. Select that `UIView` and check `Clip to Bounds` checkmark.
3. Add your required UI inside that `UIView`.
4. Set `UIView` `cornerRadius` inside `layoutSubviews()` inside your `cell` file

And to remove UnUsed `cell` write this line your `viewDidLoad` -> `self.tblVW.tableFooterView = UIView.init(frame: .zero)`

### TableView의 구분선 없애기

```swift
tableview.separatorStyle = .none
```

