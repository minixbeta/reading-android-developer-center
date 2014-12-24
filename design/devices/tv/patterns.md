# UI Patterns for TV

* Navigation Focus and Selection: 用户通常使用 D-Pad 来导航，用户只能上下左右移动。保证你的 App 在一个二维的格式上可以上下左右移动，最重要的时，需要清楚地表明当前焦点的位置，以便用户知道他们将会执行什么动作。
* Icons: Android TV 上的系统用户接口需要应用为图标提供额外的图片
    - Banners: 应用 Banner 代表你的应用在电视设备主屏幕的样子，用户通过它来启动应用，对 banner 图像的要求是，大小 320*180 px, 文字需要包含在图片内
    - Recommendation Icons: 推荐卡片上包含一个小图标，它被放在一个有颜色的背景上，对 recommendation 图标的要求是，大小 16*16 dp，白色图标，透明背景， PNG 格式
* Background Images: 背景图像在应用的背景中出现，提供额外的信息， v17 leanback support library 中提供的用户接口控件为背景图像提供了专门的支持，例如获取或失去焦点时更新他们，对 background 图像的要求 是，1920 * 1080 pixels，全彩。
* Audio Feedback: 使用声音为用户提供反馈。当用户执行动作或者即使是部分地参与到与屏幕的交互时，可以添加声音。另外，考虑使用声音来传递可视化的信息，例如当用户到达列表项的最后时，或者试图移动到焦点没有定义的地方时
