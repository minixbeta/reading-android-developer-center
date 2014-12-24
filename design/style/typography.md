# Typography

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
