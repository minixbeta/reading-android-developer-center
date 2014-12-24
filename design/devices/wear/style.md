# Sytle for Android Wear

* Screen Size: 注意屏幕的大小和形状，可穿戴设备有各种不同的形式，虽然在系统级别已经考虑了这种复杂性，但是当设计应用时，还是需要注意不同屏幕类型的影响，可以使用 Android Wear 模拟器来测试方形和圆形的设备
* Specific Assets Required: 需要根据你的卡片设计提供一些核心资源：应用图标，背景图片，动作图标 ，动作提醒动画，当然你也可以根据设计需要提供其它资源。背景图片需要 landscape 形式，至少 600px
* Peek Card Readability: 保证你的卡片在 Peek 状态下可以在主屏幕上提供有用的信息
* Low Information Density: 卡片需要设计成只看一眼就明白他要传达的信息，就像用手表看个时间一样，记得背景图片也可以传达信息的
* Separate Information into Chunks: 万一真的需要很多信息，也别把他们都放在一个卡片上，可以在卡片右边再设计一个卡片放额外信息，用户可以通过向右滑动看到这个卡片。
* Keep Notifications to a Minimum: 活动提醒只在需要及时处理时才发出，否则不要打扰用户，默默地添加到 Context Stream 即可
* User Clear, Bold Typography: 文字需要遵守推荐的大小和颜色，一般情况下，文字需要尽可能地大
* User Consistent Branding and Color: 应用图标用户标识你的应用，它是可选的，不过出现的时候都放在卡片右上方，注意不要把图标放到背景图片上，背景图片是用来传达卡片上的信息的。
* Copywrite Sparingly: 省略不必要的信息，多用词和短语，而不是句子
* Be Discreet if Necessay: 注意可穿戴设备虽然是个人设备，不过也并非完全是私有的，所以如果涉及一些敏感信息，最好不要把他们全都显示到屏幕上
* Confirmation Animations: 如果你的应用允许用户执行某个动作，那么你需要提供动作执行的反馈。可以显示一个通用的确认动画，也可以设计你自己的动画，这是一个显示应用特色的机会。确认动画的时间需要保持短暂，确认图标是向用户传达动作完成的有效方式。
