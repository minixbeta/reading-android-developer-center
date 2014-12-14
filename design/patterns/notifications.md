# Notifications
通知系统可以让用户从你的应用中及时得到通知，例如朋友发来一条聊天信息或者一个日历提醒。可以把通知当成一个消息通道，用来提醒用户
重要的事件发生了，或者记录下用户没注意到的事件发生的历史，并且可以在所有 Android 设备上同步。

### New in Android 5.0
在 Android 5.0 中，通知系统在结构，视觉以及功能上有了重要更新：
* 通知与新的 material design 主题在视觉上保持一致
* 通知现在在设备锁屏时也可以出现，但是敏感信息仍然可以被隐藏
* 高优先级的通知现在使用一个新的格式，heads-up 通知
* 云同步通知：在一个设备上让通知消失，可以同时让它在多个设备上消失

Note: 在这一版本的 Android 系统中，通知与之前的版本有很大不同。之前版本的通知设计，可以参考 [Notifications in Android 4.4 and lower]()

## Anatomy of a Notification
这一节浏览通知的基本组成部分，以及他们是如何在不同类型的设备上出现的。

### Base layout
所有的通知都至少有下面的布局，包括：

* 通知图标。这个图标是原有应用的符号。如果应用会产生多种不同类型的通知，它也可能表示通知的类型。
* 通知标题和额外的信息
* 时间戳

通知使用在之前版本中 [Notification.Builder]() 创建，在 Android 5.0 中，也以相同的方式工作，只量有一些风格上的改变，不过系统已经
帮助你处理好了。想了解更多关于之前版本的通知，可以查看 [Notifications in Android 4.4 and lower]()

### Expanded layouts
对你的应用的通知来说，你可以选择提供信息的详细程度。他们可以显示消息的前几行或者显示一个大图的预览。额外信息部分可以向用户提供
更多的信息，在某种情况下，可以让用户阅读到整个消息。用户可以通过放大或者执行一个单手指的滑动在压缩和扩展版本之间切换。对单个
事件通知，Android 提供了三种扩展布局模板（文字，收件箱, 图片)供你在应用中使用。下面的图片显示了一个单事件的消息在手持设备上和
可穿戴设备上如何显示。

### Actions
Android 在通知的底部提供了可选的动作。在这些动作上，用户可以不必打开相应应用就能对消息执行常见的任务。这加快了交互过程，并且与
滑动消失配合，帮助用户聚焦于与他们相关的通知。

谨慎决定通知内的动作数目。动作越多，你创造的感知上的复杂度就越高。尽力保持动作数目最少，只包含最重要的和最有意义的动作。

通知内一般设置有下面这些特性的动作比较好：
* 对你显示的内容类型来说，是最本质，最经常使用，最典型的动作
* 让用户快速完成任务

避免下面这些动作：
* 模棱两可
* 与通知的默认动作一样（例如阅读或者打开）

你可以将最大动作数目设置为3， 每个都包含动作图标和名字。将动作添加到通知中，会使得通知展开，即使通知没有展开布局。由于动作只为
展开的通知显示，否则就隐藏，保证用户对通知执行的任何一个动作在应用内也都可以执行。

## Heads-up Notification