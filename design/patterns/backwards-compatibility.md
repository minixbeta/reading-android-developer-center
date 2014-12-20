# Backwards Compatibility
Android 3.0 包含的重要改变有：

* 废除了导航的硬件按键（向后，菜单，搜索，主屏幕），转而支持通过虚拟控制（向后，主屏幕，最近使用）来处理导航
* 动作栏上的菜单采用了固定模式

Android 4.0 把这些改变从平板带入了手机。

## Adapting Android 4.0 to Older Hardware and Apps
### Phones with virtual navigation controls
为Android 3.0及之后的的版本在动作栏上。不适合在动作栏上显示的动作，或者没那么重要的动作会在动作栏扩展里。

用户可以通过点击动作栏来撕开动作栏扩展。

### Phones with physical navigation keys
有传统硬件键盘的手机不会在屏幕底部显示虚拟导航栏。但是动作栏扩展会在硬件按键菜单中出现。弹出菜单的风格和上一个例子是一样的，
只是是在屏幕底部显示的。

### Legacy apps on phones with virtual navigation controls
当你在一个有虚拟导航控制的手机上执行为 Android 2.3以及之前的版本构建的应用时，在虚拟导航栏的右边就会出现动作栏扩展按钮。你可以
点击那个控制按钮，这样会以传统的 Android 菜单风格显示应用的动作。
