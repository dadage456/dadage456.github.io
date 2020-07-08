### Xcode的Xib、Storyboard实现所见即所得

1、需要`@IBDesignalbe` 和 `@IBInspectable`配合使用实现所见即所得

<!-- more -->

```swift
@IBDesignalbe
class MyCustomerView: UIView {
  
  private lazy var titleLabel = getTitleLabel()
  
  private lazy var nibView = getNibCustomView()
  
  @IBInspectable var radius: CGFloat = 0 {
    	didSet {
        layer.cornerRadius = radius
        /// 自定义的视图如果包含子视图，需要下面这条命令超出边界隐藏，才能实现圆角效果
        layer.masksToBounds = true	
      }
  }
  
  /// 标题文字
  IBInspectable var titleText: String = ""
  
  
  /// 代码创建对象，初始化方法
  init(frame: CGRect) {
    super.init(frame)
    
    setupSubviews()
  }
  
  /// Xib、Storyboard创建的对象，初始化方法
  required init?(coder: NSCoder) {
        super.init(coder: coder)
    		
    		setupSubviews()
    }
  
  override func layoutSubviews() {
        /// 这里可以用于设置所见即所得对象的属性 【比如UILabel的text属性】
    		titleLabel.text = titleText
    }
  
  /// 配置所有的子视图
  private func setupSubviews() {
    addSubview(titleLabel)
    addSubview(nibView)
    
    titleLabel.snp.makeConstraints {
            $0.left.top.right.equalToSuperview()
            $0.height.equalTo(50)
        }
    
    nibView.snp.makeConstraints {
            $0.left.bottom.right.equalToSuperview()
            $0.height.equalTo(100)
        }
  }
  
  
  /// 获取系统的控件
  private func getTitleLabel() -> UILabel {
    let lable = UILabel()
    lable.font = UIFont.systemFont(ofSize: 12.0)
    lable.textColor = UIColor.red
    return UILabel
  }
  
  /// 从NIB加载的视图
  private func getNibCustomView() -> MyNibCustomView {
    
    #if TARGET_INTERFACE_BUILDER
    let bundle = Bundle(for: MyNibCustomView.classForCoder())
    #else
    let bundle = Bundle.main
    #endif
    
    let nib = UINib(nibName: "MyNibCustomView", bundle: bundle)
    guard let view = nib.instantiate(withOwner: nil, options: nil).last as? MyNibCustomView else {
      fatalError("没有找到MyNibCustomView")
    }
    return view
  }
}
```



2、所见即所得，可以绘制图像的方法

```swift
class MyCustomerView: UIView {
  /// 代码创建对象，初始化方法
  init(frame: CGRect) {
    super.init(frame)
    /// 这里可以创建所见即所得的对象
  }
  
  /// Xib、Storyboard创建的对象，初始化方法
  required init?(coder: NSCoder) {
        super.init(coder: coder)
    		
    		/// 这里可以创建所见即所得的对象
    }
  
  override func layoutSubviews() {
        /// 这里可以用于设置所见即所得对象的属性 【比如UILabel的text属性】
    }
  
  override func draw(_ rect: CGRect) {
        super.draw(rect)
   			/// 这里可以绘制所见即所得的对象
    }
  
  
}
```



3、创建的UIView对象中包含Xib创建的视图

```
#if TARGET_INTERFACE_BUILDER
        NSBundle *bundle = [NSBundle bundleForClass:[self class]];
        [bundle loadNibNamed:@"BottomCommentView" owner:self options:nil];
#else
        [[NSBundle mainBundle] loadNibNamed:@"BottomCommentView" owner:self options:nil];
        
#endif
```

