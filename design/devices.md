# Devices

这一部分以设备为中心，讲述与其相关的设计准则。

## Phones & Tablets 

Android 系统提供了UI框架帮助我们构建应用，无论是手机，平板，手表，还是其它形式的设备。我们的应用在提供为 Android 平台提供统一
的用户体验上扮演着重要角色。这一部分的内容可以帮助我们达成这一目标。

* Home screen: 主屏幕上包含了最常用的应用的快捷方式
* All apps screen: 所有应用屏幕上包含了已经安装到手机上的应用
* Recents screen: Recents 屏幕可以帮助我们在最近使用的应用之间快速切换

## System Bar

System Bar 通常情况下会和应用一起显示，除非应用全屏。它包含状态栏，导航栏。

* Status Bar: 就是屏幕最上方的一栏，显示电量，信号，或者通知
* Navigation Bar：一般在手机屏幕下方，有三个虚拟键，分别是返回，主屏，显示最近应用

## Notifications

Notification 可以提供更新，提醒或者信息，它们是重要的，但又没重要到需要打断用户。可以通过下拉 Status Bar 来查看通知。

## Common App UI

很多应用都有一些公有的部分，包括 

* Action Bar: 就是应用上面的动作栏，上面有应用图标，设置按钮
* Navigation Drawer: 侧栏，一般通过滑动屏幕左边缘拉出
* Content Area: 内容区，应用的主要部分就在这个区域显示
