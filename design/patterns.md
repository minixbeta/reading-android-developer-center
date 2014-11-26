# Patterns

## New in Android

### Android 5.0 Lollipop

* Material design: Material design 各个设备和平台上视觉，动作，交互的综合设计准则。Android 5.0 为复杂的视图提供了新的主题，控件，
为阴影和动画提供了新的 API，帮助你在应用中实现  material design.
* Notifications: 在 Android 5.0 中，通知得到了重要更新，包含 material design 风格的视觉改变，锁屏状态下的通知，优先级通知以及云同步通知。

### Android 4.0 KitKat

* Your branding: 一致性在Android中有重要的地位，但是你仍然可以灵活地定制应用的样子，以便加强你的品牌。使用你品牌的颜色覆盖 Android
框架中默认的蓝色，例如在复选框，进度条，单选框，滑块，标签，滑动指示器。在动作栏上显示应用的启动图标及名称，让用户在应用的每个视图
中都能看到。强烈建议将品牌元素整合到应用的视觉语言中。
* Touch feedback: 在 Android KitKat 之前，Android 默认的触摸反馈是醒目的蓝色。每次触摸都会导致一个高对比度的颜色，他们可能和你
品牌的颜色不搭。在 Android KitKat 及之后，触摸反馈不易察觉，当一样东西被触摸时，默认情况下他的背景颜色略微变暗或者变亮。这带来了
两个好处: 小的反馈比突兀的反应更令人愉悦；可以更好的将你的品牌整合进来，因为无论你选择什么颜色触摸反馈都能很好地工作。
* Full screen: Android KitKat 提升了应用使用全屏的支持
* Gestures: 更新的 Gestures 页面包含了 Android KitKat 中引入的新手势指引，两点触摸及两点触摸拖拽。这些手势可以用来改变内容视图
的大小。

### Android 4.1 Jelly Bean

* Notifications: 通知在 Android 4.1 中得到了显著的增强：
  - 用户可以在 drawer 中快速对通知作出响应
  - 通知在大小和布局上更灵活
  - 一个优先级标记帮助我们将通知按重要程度排序
  - 通知可以被收缩和扩展
  
  基本的通知布局并没有改变，所以为 Jelly Beans 之前版本设计的通知是可以正常使用的。
  
* Resizable Application Widgets:  widgets 是主屏幕定制中非常重要的一个方面，可以快速浏览应用中最重要的数据和功能。Android 4.1
引入了增强的应用 widgets，可以自动调整大小 ，载入不同内容 ，它基于下面几个方面：
  - 用户把他们放在主屏幕的什么位置
  - 用户将他们放大到多大
  - 主屏幕上有多少可用空间
  
  你可以为 widgets 分别提供横屏和竖屏的布局，当屏幕方向改变时，系统会加载合适的布局
  
* Accessibility

Android 的任务之一就是组织世界上的信息，并且让他们随时随地可以访问并且有用。我们的任务适用于所有用户，包含那些有视觉障碍
或者听力丧失。新的 Accessibility 页面告诉你如何设计你的应用，使得他们可以访问到

  - 导航符合直觉
  - 使用推荐的触摸目标大小
  - 可见的UI元素要有有意义的名字
  - 超时时要提供备选方案
  - 使用标准框架控件或者对定制控件提供动作反馈
  - 自己试试
