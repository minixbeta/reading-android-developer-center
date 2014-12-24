# App Structure for Android Wear

用户以前是通过点击按钮启动一个应用，在 Android Wear 中不是这样，Android Wear 的应用会在适当的时候向流中插入一个卡片。下面

* Contextual card in the stream
    - Bridged notification: 新消息提醒，可以使用标准的 Android Notification 实现 
    - Contextual notification: 与场景相关的卡片，例如在运动开始时显示一个与运动相关的卡片
* Full screen UI app
    - 2D Picker: 这是一种设计模式，可以让用户从一个项集中选择一个
    - Custom layouts: 当用户需要扩展当前的卡片/流的模式，例如呈现一个图
