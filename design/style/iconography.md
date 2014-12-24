# Iconography

图标是占据屏幕一小块空间的图片，代表动作，状态或者应用。当为应用设计图标时，需要记住你的应用可能会被安装在各种不同的设备上，它们有着不同的屏幕密度。你可以通过提供各种不同大小的图标，使得你的应用在各种设备上都能很好地展示。当你的应用运行时，Android 会检测设备屏幕，并且为你的应用加载与屏幕密度对应的资源。

所以，为了为不同密度的设备创建图标，你需要为五种不同的密度设计 2:3:4:6:8 的图标，五种密度分别为 (medium, high, x-high, xx-high, xxx-high)。例如，如果启动图标是 `48*48` dp, 这意味着基准资源(MDPI)大小为 `48*48`。 这样，HDPI 资源就是 1.5x，即 `72*72` dp. 

## Launcher

启动图标在主屏幕上代表你的启用，因为用户可能会改变背景，所以你需要保证在任何背景下，你的启动图标都可以正常显示。

* Sizes & scale: 启动图标必须是 `48*48` dp, 在 Google Play 上显示的启动图标必须是 `515*512` pxiels
* Proportioins: 整个图标 48*48 dp
* Style: 使用不同的轮廓

## Action Bar

动作栏的图标代表用户在你的应用内使用的最重要的动作，每个图标都需要让用户看一眼就知道它是干什么的。

预定义的 glyphs 应该被用于一些通用的动作，例如，刷新，分享。下面的链接提供了适用于不同 屏幕密度的图标包。

[Download the Action Bar Icon Pack](http://developer.android.com/downloads/design/Android_Design_Icons_20131106.zip)

* Sizes & scale: 手机的动作栏上的图标应该是 `32*32` dp
* Focal area & proportions: 整个图标 `32*32` dp, 图标的内容区 `24*24` dp
* Style: 扁平，没有过多细节，有平滑的边缘或者尖锐的形状。如果图片太细了，可以向左或者向右旋转 45 度。笔画细的地方最小是 2dp
* Colors: 颜色有两种 
    - Colors:#333333, Enabled: 60% opacity, Disabled: 30% opacity
    - Colors:#FFFFFF, Enabled: 60% opacity, Disabled: 30% opacity

## 小图标/场景相关图标

在应用内，可以把小图标放在动作上，或者表示指定项目的状态，例如， Gmail 使用小星星图标表示邮件是重要的。

* Sizes & scale: 小图标应该是 `16*16` dp
* Focal  proportions: 整个图标 `16*16` dp, 图标的内容区 `12*12` dp
* Style: 浅色，扁平，简单。填充的形状比细笔画更容易识别。使用简单的视觉隐喻，让用户一看到就明白这代表什么。
* Color: 少用非浅色系，如果用的话，要有特别的目的。例如 Gmail 使用黄色代表收藏消息。如果一个图标有动作，需要选择对比强烈的颜色作为背景。

## 通知栏图标

如果你的应用会产生通知，需要提供一个系统可以显示的图标，当有新消息时，在状态栏显示。

* Sizes & scale: 通知图标必须是 `24*24` dp
* Focal area & proportions: 整个图标 `24*24` dp, 内容区 `22*22` dp
* Style: 保持扁平，简单
* Colors: 通知图标必须全是白色的，系统可能会缩小或者使通知图标变暗

## Design Tips

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
