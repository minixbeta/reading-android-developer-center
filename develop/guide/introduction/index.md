# Introductioin to Android
Android 提供了丰富的应用程序框架，可以让你创建出具有创新性的应用与游戏。左边的导航提供了各种 Andoird API 的详细文档。

如果你是个 Android 新手，那么明白下面的这些概念是非常重要的。

## Apps provide multiple entry points
Android 应用由不同的组件组合在一起，他们可以被独立调用。例如，一个独立的 **活动** 对用户提供一个简单的屏幕，一个服务可以在后台独立地执行任务。

在一个组件中，你可以使用 **意图** 来启动另一个组件。你甚至可以在不同的应用中启动一个组件 ，例如在一个地图应用中显示一个地址。这一模式为单个应用提供了多个入口点。用户可以让任何一个程序作为某个动作的默认选择，其它应用
可以调用这个动作。

更多信息：

[应用基础]()

[意图和意图过滤]()

[活动]()

## Apps adapt to different devices
Android 提供了一个适应性强的应用框架，你可以为不同设置提供独立的资源。例如，你可以为不同大小的屏幕设计不同 的 XML 布局文件，系统会根据设备的屏幕大小来决定加载哪个布局。
如果应用需要特别的硬件支持，例如摄像头，你可以在运行的时候查询设备特性的可用性。如果需要的话，你可以声明应用都需要哪些支持，
这样像 Google Play 这样的应用市场，就可以在没这个支持的设备上阻止安装。

更多信息：

[设备兼容性]()

[资源概览]()

[用户接口概览]()
