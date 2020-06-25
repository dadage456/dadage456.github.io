# UIStackView的属性笔记

做iOS开发8年了吧，对于一些技术还是有点模糊。也没有学笔记的习惯，有些问题虽然解决了，但是头脑中没有一个清晰的思路。以至于后来遇到同样的问题，还是需要摸索摸索。

这里主要记录一下： 

* UIStackView的属性的理解

* UIStackView在 **确定了大小约束** 和  **没有确定大小约束** 两种情况下，子视图的布局的不同。



### 一、UIStackView的基本属性

> 首先了解一下主轴、纵轴的概念：
>
> 主轴: UIStackView的布局方向【布局方向是水平，主轴就是水平】
>
> 纵轴：UIStackView的布局的另一个方向 【布局方向是水平，主轴是垂直】



UIStackView主要依靠`axis`、`distribution`、`alignment`、`spacing`属性进行子视图的布局。

<img src="https://docs-assets.developer.apple.com/published/82128953f6/uistack_hero_2x_04e50947-5aa0-4403-825b-26ba4c1662bd.png" alt="官网给的图" style="zoom:50%;" />



* axis: 子视图的布局方向，水平和垂直
* distribution: 子视图的主轴的布局方式
* alignment：子视图的纵轴的对齐方式
* spacing：子视图之间的间距



### 二、distribution属性

> **对于Fill类型的布局**：
>
> - StackView大小不确定：通过指定子元素大小，确定StackView的大小
> - StackView大小确定：子元素填充StackView的空间



* `UIStackViewDistributionFill`

  > 子元素填满主轴方向StackView空间。

  * StackView大小约束确定：设置其他子元素的高度，留下一个子元素的高度自适应填充StackView空间
    <img src="http://qaan37d6g.bkt.clouddn.com/ios_stack_destribute_fill.png" alt="StackView大小约束确定" style="zoom:50%;" />
    
    
    
  * StackView大小约束不确定： 所有的子元素指定高度
    <img src="http://qaan37d6g.bkt.clouddn.com/ios_stack_destribute_fill_2.png" alt="StackView大小约束不确定" style="zoom:50%;" />
    
    
  
* `UIStackViewDistributionFillEqually`

  > 自动调整子元素在主轴方向的大小，使他们大小一致，填满整个StackView空间。

  * StackView的大小约束确定：子元素自动调整高度。
    <img src="http://qaan37d6g.bkt.clouddn.com/ios_stackview_distribute_fill_equally.png" alt="StackView大小约束确定" style="zoom:50%;" />
    
    
    
    * StackView的大小约束不确定：指定一个子元素的高度，其他的子元素自动调整相同高度
      <img src="http://qaan37d6g.bkt.clouddn.com/ios_stackview_distribute_fill_equally_2.png" alt="StackView的大小约束不确定" style="zoom:50%;" />
  
  
  
* `UIStackViewDistributionFillProportionally`

  > 子元素根据自身Frame中的主轴大小，确定占用StackView空间的百分比。
  >
  > StackView大小约束确定：子元素会等比例适配
  >
  > StackView大小不确定：StackView的大小会根据子元素在主轴上大小，自定适配。

    <img src="http://qaan37d6g.bkt.clouddn.com/ios_stack_destribute_propertion_frame.png" alt="StackView的大小约束不确定" style="zoom:50%;" />

  

* `UIStackViewDistributionEqualSpacing`： **StackView的大小约束确定的情况下使用**

  <img src="https://docs-assets.developer.apple.com/published/82128953f6/distribute_equalspacing_2x_6668568b-a445-402c-94ae-f5e85b0b10bd.png" alt="UIStackViewDistributionEqualSpacing" style="zoom:50%;" />

* `UIStackViewDistributionEqualCentering`： **StackView的大小约束确定的情况下使用

  <img src="https://docs-assets.developer.apple.com/published/82128953f6/distribute_equalcentering_2x_7089d0d3-f161-452b-ab3e-9885c7b6101e.png" alt="UIStackViewDistributionEqualCentering" style="zoom:50%;" />

  