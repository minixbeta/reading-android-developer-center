# Devices

这一部分以设备为中心，讲述与其相关的设计准则。

## Phones & Tablets 

Android 系统提供了UI框架帮助我们构建应用，无论是手机，平板，手表，还是其它形式的设备。我们的应用在提供为 Android 平台提供统一
的用户体验上扮演着重要角色。这一部分的内容可以帮助我们达成这一目标。

* Home screen: 主屏幕上包含了最常用的应用的快捷方式
* All apps screen: 所有应用屏幕上包含了已经安装到手机上的应用
* Recents screen: Recents 屏幕可以帮助我们在最近使用的应用之间快速切换

### System Bar

System Bar 通常情况下会和应用一起显示，除非应用全屏。它包含状态栏，导航栏。

* Status Bar: 就是屏幕最上方的一栏，显示电量，信号，或者通知
* Navigation Bar：一般在手机屏幕下方，有三个虚拟键，分别是返回，主屏，显示最近应用

### Notifications

Notification 可以提供更新，提醒或者信息，它们是重要的，但又没重要到需要打断用户。可以通过下拉 Status Bar 来查看通知。

### Common App UI

很多应用都有一些公有的部分，包括 

* Action Bar: 就是应用上面的动作栏，上面有应用图标，设置按钮
* Navigation Drawer: 侧栏，一般通过滑动屏幕左边缘拉出
* Content Area: 内容区，应用的主要部分就在这个区域显示

## Wear

使用 Android Wear 为可穿戴设备设计应用与手机和平板截然不同，不同的优势和缺陷，不同的用户场景，不同的人体工程学。你需要明白
Android Wear 在全局上的体验，以及如何加强这种体验。新形式的设备需要有新的 UI 模型，Android Wear 的 UI 包含了两个重要部分，分别
是 Suggest 和 Demand。

Suggest 是Android Wear推给用户的信息，可以竖着滑动，查看不同卡片上的信息，也可以横着滑动，查看当前卡片上进一步的信息。Demand 是用户的需求，可以告诉 Google 。不同的声音指令，会启动不同的 intent，应用开发者可以让自己的应用匹配相应的 intent，这样当用户
发出相应指令时，就会启动你的应用。如果有多个应用对应同一个 intent，系统会提示用户选择。

### Creative Vision

Android Wear 设备会在正确的时间提供正确的信息。它会根据环境的变化自动启动应用；它会像传统手表那样，你使用的时候看一眼就好，你
使用软件的时间越少，专注于眼前事务的时间就越长；它像个人助理，知道你的喜好，只在必要的时候打断你；它专注于简单的交互，只在必要
的时候才需要你输入信息，并且大部分信息都是通过滑动或者声音来输入的。

### Design Principles

* Focues on not stopping the user and all ese will follow: 手表比较适用于这种场景：用户在做事情的时候偶尔看一下，例如做饭，吃东西，跑步等等
* Design for big gestures: 用户会在各种场景下使用手表应用，不要让用户因为使用你的应用而影响他们正在做的事
* Think about stream cards first: 最佳的体验是当用户正好需要的时候，你的应用恰好出现在那里。如果你实在不知道用户什么时候需要，可以通过声音或者触摸来实现
* Do one thing, really fast: 如果用户一次使用你的应用时间只有几秒，那么他们在一天之中就可能更多地使用你的应用
* Design for the corner of the eye: 用户盯着你的应用的时间越长，他们就离现实世界越远
* Don't be a constant shoulder tapper: 手表是用户的贴身物品，可别让你的应用像在手机上那样不断发出振动
* 

### App Structure for Android Wear

用户以前是通过点击按钮启动一个应用，在 Android Wear 中不是这样，Android Wear 的应用会在适当的时候向流中插入一个卡片。下面

* Contextual card in the stream
    - Bridged notification: 新消息提醒，可以使用标准的 Android Notification 实现 
    - Contextual notification: 与场景相关的卡片，例如在运动开始时显示一个与运动相关的卡片
* Full screen UI app
    - 2D Picker: 这是一种设计模式，可以让用户从一个项集中选择一个
    - Custom layouts: 当用户需要扩展当前的卡片/流的模式，例如呈现一个图

### UI Patterns for Android Wear

Android Wear 主要用户微交互的场景，所以遵从用户已经适应的设计模式是至关重要的。

* Cards: 流上的卡片可以有几种不同的形式，例如提醒显示的标准卡片，单一动作控件（开始/暂停)，多个叠加在一起的卡片
* App icons: 应用图标出现在卡片右上方的固定位置，图标只出现在最左边的卡片上，没必要在每个 page 上都加上图标
* Pages: Pages 是对流上卡片的补充信息
* Dismissing cards: 从左向右滑动可以使一个卡片消失
* Action buttons: 当用户需要对提醒中的信息执行动作时，你的应用可以提供一个动作按钮，目前一个卡片最多只能有三个按钮
* Action countdown and confirmation: 按一个按钮后，可能会出现下列事件
    - 动作马上执行完了，结果立即显示
    - 动作在执行过程中，一个 countdown 动画会显示，用户可以在此时取消这个动作
    - 需要一个确认步骤
    - 显示一个提示卡片，继续显示下一个动作
* Continuing activities on phone: 开发者需要尽可能在可穿戴设备上执行动作，如果一定需要使用手机，可以在手表上的动作按钮被按下，手机上启动一个活动时，显示一段通用的动画。
