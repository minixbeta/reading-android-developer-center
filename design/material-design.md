# Material Design

Android 为 Material Design 提供了：

* 新主题
* 为复杂视图提供的新控件
* 为定制阴影和动画提供的新API

## Material Theme

包含了一暗一亮两种主题，系统控件会自带一些动画效果。

## List Cards

提供了一种新的控件，RecyclerView，比ListView支持更多的布局类型，并提高了性能。另外一种控件 CardView，是一种卡片式的风格，
可以将重要信息放在卡片内，多个卡片可以拥有一致的风格。

## View Shadows

现在不仅有 X, Y 轴了，还有了 Z 轴，Z 轴数值大的，会有更多阴影，并且处于其它控件之上。

## Animations

可以自己定义点击控件时的动画效果，视图的隐藏显示切换的动画

## Drawable

Drawable 的新特性可以帮助我们设计出符合 Material Design 的应用：

* Vector drawables: 向量形式的控件，不会随着放大失真
* Drawable tinting：定义图片的 alpha mask，使用 tint 属性调整色调
* Color extraction：从控件中提取颜色
