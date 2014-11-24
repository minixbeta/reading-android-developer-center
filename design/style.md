# Style

## Devices and Displays

使用 Android 灵活的布局系统，你可以为从平板到手机各种大小的设备优雅地创建应用。

* Be flexible: 通过扩展，压缩布局，适应各种不同的高度和宽度
* Optimize layouts: 在大的设备上，利用多余的屏幕空间，创建多个组合视图，显示更多的内容
* Assets for all: 为不同屏幕密度的设备提供资源，使应用在任何设备上看起来都不错
* Strategies: 当为不同设备作设计时，从何开始呢？一种方法是从标准大小开始，然后放大或者缩小。另一种方法是从最大的屏幕开始，
然后缩小，计算出各个UI组件在小屏幕上的大小 。

## Theme

主题是 Android 提供的一种机制，可以使应用或者Activity有一致的风格。风格指定了组成用户接口的元素的可视化属性，例如颜色，高度，字节大小等等。为了保证 Android 平台上所有应用风格的一致性，系统提供了两种默认风格：

* Holo Light
* Holo Dark

你可以以此为基础，定制自己的风格。

## Touch Feedback

使用明暗效果对用户的触摸行为作出响应，加强手势行为带来的结果，表明动作是可用的还是不可用的。

使用温和的方式对用户的触摸行为作出响应。当用户触摸应用内的区域时，让他们知道你的应用对其作出了响应，例如颜色变亮或者变暗。

* States
  - 正常状态: 灰色
  - 按下后: 颜色略微变深
  - 获得焦点: 颜色变亮
  - 不可用：正常状态 30% 亮度
  - 不可用并获得焦点：焦点状态 30% 亮度

大部分 Android 的 UI 元素已经内置了触摸反馈

* Communication

当控件需要对复杂的动作作出响应时，应该帮助用户明白动作的结果是什么，例如删除一个元素时，让颜色变暗

* Boundaries

当用户滑动到区域边界时，边缘应该高亮，告诉用户不能滑动了。Android 中很多可滑动的控件都已经支持边界反馈了，如果你要自己定制，
记得也要支持。

## Metrics and Grids

设备不仅在大小方面不同，在屏幕密度(DPI)方面也不同，为了简化问题，我们把设备按下面的规则分类：

* 按大小分为手机(小于600dp)和平板(大小等于600dp)
* 按密度分为 LDPI, MDPI< HDPI< XHDPI< XXHDPI, XXXHDPI

为不同大小的设备设计不同的布局，为不同密度的设备提供不同的图像资源，以此来优化应用的UI。由于你需要为不同密度的设备设计，实现
布局，下面的文档使用 dp 而不是 pixels 作为度量。

### 48dp Rhythm

#### Why 48dp

可以触摸的UI组件一般放在 48dp 个单位上, 48dp 换算成物理大小是大约 9mm，它处于推荐的目标大小 范围内：(7-10mm)，用户正好可以用手指精确地点上去。如果你设计的元素的长宽至少是48dp，那么可以保证：

* 你的组件不会少于可触摸的最小目标大小 7mm
* 在信息密度和可点击性之间达到一种折衷

#### Mind the gaps

UI 元素之间的空隙为 8dp

## Typography

Android 设计语言依赖于传统的排版工具，例如 scale, space, rhythm, alignment。成功使用这些工具是帮助用户快速理解屏幕中信息的
基础。为了支持这种排版，Ice Cream Sandwich 为有需要的 UI 及高分辨率屏幕引入了新的字体集 Roboto。

当前的 TextView 框架提供了各种 Roboto: thin, light, regular, bold, italic 。框架还提供了 Roboto Condensed 变种 ，支持 regular, bold, italic 。

* 默认颜色类型: Andorid UI 使用下面的默认颜色风格：textColorPrimary 和 textColorSecondary。对 light 主题，可以使用 textColorPrimaryInverse 和 textColorSecondaryInverse
* 排版大小：太多不同的字体大小会显得凌乱，Android 框架使用下面的大小集合
  - Text Size Micro: 12sp
  - Text Size Small: 14sp
  - Text Size Medium 18sp
  - Text Size Large 22sp

用户可以在系统设置应用中设置系统范围内的大小因子，为了支持这些特色，在任何可能的情况下，都要使用 sp。如果布局支持改变大小，
需要在这些设置下再次测试。
