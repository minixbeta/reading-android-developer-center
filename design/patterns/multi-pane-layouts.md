# Multi-pane Layouts

写 Android 程序的时候，要时刻记得 Android 设备有不同的屏幕大小和类型。针对不同的屏幕和屏幕方向，调整内容，以确保你的应用一致地
提供平衡美观的布局。

Panels 是应用达成这一目标的好方式。当水平方向有很多屏幕空间可用时，他们可以把多个视图组合成一个视图，当屏幕空间不足时，又可以
分开。

## Combining Multiple Views Into One
在小型的设备上，你的内容一般会被分割成一个大的格子或者列表，以及详情视图。点击其中一项，可以显示一个不同的屏幕，上面显示这一项的
详情。

由于平板比手机有更多的屏幕空间，你可以将相关列表和详情视图放在一个组合视图中。这样可以高效地使用屏幕空间，同时使得导航更加简单。

一般情况下，使用右边的面板显示你在左面板上选择项目的详情。确保左面板的项目是选中状态，以展示他们之间的关系。

## Compound Views and Orientation Changes
无论屏幕的方向如何，都应该提供一致的功能。如果你在一个方向上使用了组合视图，那么当用户旋转屏幕时，尽量不要把他们分割开。你可以使用下面的一些技术来调整布局，保证屏幕方向改变后，保持功能的完整性。

### Stretch/compress
调整左面板的宽度，使得两个方向上都能达到平衡

### Stack
重新安装屏幕上的面板，以匹配方向

### Expand/collapse
当屏幕旋转的时候，折叠左面板以显示最重要的信息

### Show/hide
如果旋转后屏幕无法容纳组合的空间，可以全屏显示右面板的信息。使用动作栏上的向上图标去显示父屏幕。

## Checklist
* 提前计划好你的应用在不同屏幕大小和方向下如何扩展
* 当屏幕方向改变时，选择最合适的方法去重新组织组合视图中的内容
* 寻找机会，使你的视图变成多面板组合视图
* 确保屏幕方向改变时，应用提供的功能的完整性
