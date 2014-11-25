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

## Color

使用颜色主要是为了强调。选择颜色时，需要与你的品牌相适应，并且在可视化的组件之间有良好的对比。注意红色和绿色可能会让有色盲的
用户难以分辨。

### Palette

蓝色是 Android 调色板中的重要颜色，每种颜色都有对应的深色

## Iconography

图标是占据屏幕一小块空间的图片，代表动作，状态或者应用。当为应用设计图标时，需要记住你的应用可能会被安装在各种不同的设备上，它们有着不同的屏幕密度。你可以通过提供各种不同大小的图标，使得你的应用在各种设备上都能很好地展示。当你的应用运行时，Android 会检测设备屏幕，并且为你的应用加载与屏幕密度对应的资源。

所以，为了为不同密度的设备创建图标，你需要为五种不同的密度设计 2:3:4:6:8 的图标，五种密度分别为 (medium, high, x-high, xx-high, xxx-high)。例如，如果启动图标是 `48*48` dp, 这意味着基准资源(MDPI)大小为 `48*48`。 这样，HDPI 资源就是 1.5x，即 `72*72` dp. 

### Launcher

启动图标在主屏幕上代表你的启用，因为用户可能会改变背景，所以你需要保证在任何背景下，你的启动图标都可以正常显示。

* Sizes & scale: 启动图标必须是 `48*48` dp, 在 Google Play 上显示的启动图标必须是 `515*512` pxiels
* Proportioins: 整个图标 48*48 dp
* Style: 使用不同的轮廓

### Action Bar

动作栏的图标代表用户在你的应用内使用的最重要的动作，每个图标都需要让用户看一眼就知道它是干什么的。

预定义的 glyphs 应该被用于一些通用的动作，例如，刷新，分享。下面的链接提供了适用于不同 屏幕密度的图标包。

[Download the Action Bar Icon Pack](http://developer.android.com/downloads/design/Android_Design_Icons_20131106.zip)

* Sizes & scale: 手机的动作栏上的图标应该是 `32*32` dp
* Focal area & proportions: 整个图标 `32*32` dp, 图标的内容区 `24*24` dp
* Style: 扁平，没有过多细节，有平滑的边缘或者尖锐的形状。如果图片太细了，可以向左或者向右旋转 45 度。笔画细的地方最小是 2dp
* Colors: 颜色有两种 
    - Colors:#333333, Enabled: 60% opacity, Disabled: 30% opacity
    - Colors:#FFFFFF, Enabled: 60% opacity, Disabled: 30% opacity

### 小图标/场景相关图标

在应用内，可以把小图标放在动作上，或者表示指定项目的状态，例如， Gmail 使用小星星图标表示邮件是重要的。

* Sizes & scale: 小图标应该是 `16*16` dp
* Focal  proportions: 整个图标 `16*16` dp, 图标的内容区 `12*12` dp
* Style: 浅色，扁平，简单。填充的形状比细笔画更容易识别。使用简单的视觉隐喻，让用户一看到就明白这代表什么。
* Color: 少用非浅色系，如果用的话，要有特别的目的。例如 Gmail 使用黄色代表收藏消息。如果一个图标有动作，需要选择对比强烈的颜色作为背景。

### 通知栏图标

如果你的应用会产生通知，需要提供一个系统可以显示的图标，当有新消息时，在状态栏显示。

* Sizes & scale: 通知图标必须是 `24*24` dp
* Focal area & proportions: 整个图标 `24*24` dp, 内容区 `22*22` dp
* Style: 保持扁平，简单
* Colors: 通知图标必须全是白色的，系统可能会缩小或者使通知图标变暗

### Design Tips

这里有一些提示，如果你要创建自己的图标或者其它资源，他们可能会对你有帮助。这些提示假设你使用的是 Photoshop 或者其它类似的
基于向量的图片编辑器。

* User vector sapes where possible: 只要可能，就使用矢量图，在放大时他们不会丢失细节
* Start with large artboards: 一开始的时候尽量创建大图，这样你可以方便地把他们变成小图，从而适配各种不同的屏幕
* When scaling, redraw bitmap layers as needed: 如果你要放大一个 bitmap 图，而不是矢量图，那么你可能需要重新绘制这个图
* Use common nameing conventions for icon assets: 命名图片时，同组资源加上相同前缀，这样按字母排序时他们就会在一起

| Asset Type | Prefix | Example |
| :----------|:-------| :-----|
| Icons | ic_ | ic_star.png |
| Launcher icons | ic_launcher | ic_launcher_calendar.png |
| Menu icons and Action Bar icons | ic_menu | ic_menu_archive.png | 
| Status bar icons | ic_stat_notify | ic_stat_notify_msg.png | 
| Tab icons | ic_tab | ic_tab_recent.png |
| Dialog icons | ic_dialog | ic_dialog_info.png |

* Set up a working space that organizes files by density: 根据屏幕密度不同，组织资源目录

```
art/...
  mdpi/...
    _pre_production/...
      working_file.psd
    finished_asset.png
  hdpi/...
    ...
  xhdpi/...
    ...
  xxhdpi/...
  ...
```

* Provide an xxx-high-density lancher icon: 有些设备会把启动图标放大 25%，所以你需要在 drawable-xxxhdpi 目录下创建一个高密度的图标
* Remove unnecessary metadata from final assets: 虽然 Android SDK 会在打包时自动压缩应用程序资源，但是一个最佳实践是删除PNG资源不必要的头文件和元数据文件。 OptiPNG 或者 Pngcrush 可以保证元数据文件被清除了，并且文件大小得到优化。

## Your Branding

遵循 Android 设计规范并不意味着你的应用看起来和其它人的一样，在 Android 中，应用应该是你的品牌的延伸。

### Color 

通过使用你品牌的颜色替换 Android 默认的蓝色，例如复选框，进度条，单选按钮，滑块，tabs, scroll indicators。

使用高对比的颜色进行强调，例如动作栏或者主按钮与背景颜色的对比，但是记得不是所有动作按钮都是需要强调的。

定制颜色的时候，触摸反馈需要小心处理，比没有触摸时亮一点或者暗一点。

### Logo

应用的启动图标是放入 Logo 的关键位置，你可以把启动图标放在应用内每个页面的动作栏上

### Icons

如果你的应用在其它平台使用了一些图标，你也可以把他们用到 Android 平台上来。如果你使用了这种方式，确保你的品牌风格被用到应用中
每一个图标中。

例外：如果你已有的图标符号和 Android 平台的不一样，那么，使用 Android 平台上的样子，并加上你的风格。这样，用户根据他们在其它
Android 应用中学到的经验，很容易明白这些符号的含义。

如果你没有自己的图标集，在 Android 平台上开发的是新应用，那么，使用 Android 的标准图标，使用颜色和Logo作为品牌标识。动作栏图标集可以在这里免费[下载](http://developer.android.com/design/downloads/index.html)
