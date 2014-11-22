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
* Actioins on cards(such as media controls): 有时候可以直接通过点击卡片而非点击卡片上按钮的方式来操作，但是需要注意这样做的场景
    - 直接点击卡片时，只有一种可能的结果
    - 直接点击卡片时，无需文字就能明白这样做的后果
    - 直接点击卡片时，只会导致可穿戴设备上的事情发生
    - 一个卡片上只有一个动作
    - 不要在一个卡片上放一个菜单 
* Card stacks: Card stacks 由一组相关卡片构成，开始时只会显示最上面的卡片，可以通过点击展开所有卡片
* 2D Picker: 2D Picker 组件可以通过 cur card(提示卡片) 或者动作按钮调用，用户可以使用它从一系列选项中选择一个
* Voice commands: 应用可以注册到一个声音命令，这样当用户发出声音命令时，相应的应用就会启动。如果有多个应用注册到此命令，会让用户选择并记录下用户的偏好
* Selection List: 从一个列表项中选择一个是很常见的交互方式， 使用 Selection List 模式可以创建一个简单易用的列表，它专门为小屏幕优化过

### Sytle for Android Wear

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

## TV

Design for Android TV

Android TV 用户接口为应用的大屏幕体验提供了一个启动平台，理解你的应用在主要的用户接口上是如何展示的以及如何使用户快速获取信息是非常重要的。

* Home Screen: 主屏幕是用户体验的开始，提供了搜索，内容推荐，访问应用和设置的功能
* Search: 为了将 Google 强大的搜索能力带到大屏幕上， Android TV 在内容之间建立了全新的，动态的连接。例如搜索喜欢的电影可能会发现一个新的音乐家，计划到巴黎的旅行可能会发现 YouTube 上的新内容和照片
* Recommentdations: Android TV 上的推荐内容是主屏幕上的一个主要特色，推荐的内容是根据用户最近的使用行为及频率来决定的。你的应用可以为推荐提供一些提示。推荐内容是以卡片形式出现的，可能代表一个系统或者应用动作，提醒，活动，可以执行动作的多媒体信息等等。
* Apps and Games: 应用和游戏也在主屏幕上分别占有一行的空间，反应用户最近的使用情况
* Settings: 用户可以在主屏幕的底部访问设置按钮，从这里对设备进行相关设置

### Creative Vision

* Casual Consumption: 与电脑和手机不同，电视是娱乐设备，需要对以内容为中心的活动进行优化：看电影的姿势，虚拟现实游戏。用户希望打开电视时能快速访问内容，点击一下就能切换到下一内容。
* Cinematic Experience: 为用户创建一种沉浸式的体验。在屏幕上多显示内容，少显示用户接口。使用图像，动作，声音通知用户，避免使用文字传递信息。
* Simplicity: Android TV 是简单而又令人愉悦的。尽可能地减少执行动作需要的导航步骤，要减少应用入口与内容之间可能的屏幕数目，避免用户输入文本信息，当需要用户输入时，使用声音接口。

### UI Patterns for TV

* Navigation Focus and Selection: 用户通常使用 D-Pad 来导航，用户只能上下左右移动。保证你的 App 在一个二维的格式上可以上下左右移动，最重要的时，需要清楚地表明当前焦点的位置，以便用户知道他们将会执行什么动作。
* Icons: Android TV 上的系统用户接口需要应用为图标提供额外的图片
    - Banners: 应用 Banner 代表你的应用在电视设备主屏幕的样子，用户通过它来启动应用，对 banner 图像的要求是，大小 320*180 px, 文字需要包含在图片内
    - Recommendation Icons: 推荐卡片上包含一个小图标，它被放在一个有颜色的背景上，对 recommendation 图标的要求是，大小 16*16 dp，白色图标，透明背景， PNG 格式

* Background Images: 背景图像在应用的背景中出现，提供额外的信息， v17 leanback support library 中提供的用户接口控件为背景图像提供了专门的支持，例如获取或失去焦点时更新他们，对 background 图像的要求 是，1920 * 1080 pixels，全彩。
* Audio Feedback: 使用声音为用户提供反馈。当用户执行动作或者即使是部分地参与到与屏幕的交互时，可以添加声音。另外，考虑使用声音来传递可视化的信息，例如当用户到达列表项的最后时，或者试图移动到焦点没有定义的地方时

### Style for TV

* Layouts: 在电视设备上，体验的好坏，依赖于屏幕上元素的数目，空隙，大小，虽然电视设备变得越来越大，但是用户还是希望电视设备上的体验简单，简洁。电视设备提供的额外分辨率和屏幕区域，是用于显示高质量内容的，而不是显示更多数目的内容。如果你想创建一个应用，用于显示，浏览信息，那么可以使用 v17 leanback support library，这些布局由 Android TV 的用户体验部门专门为电视设备建立。下面还有一些建议：
    - 设计 landscape 方向的布局，电视一般都是这个方向的
    - 设计资源要适用于 HD 分辨率(1920 * 1080)
    - 将导航控件放在屏幕左边或者右边，节省竖直方向的空间
    - 使用 fragment 来创建 UI 上的多个部分，使用 Grid View 而不是 List View 来更好 地使用水平方向的空间
    - 通过增加布局控件边缘大小，避免显示凌乱
* Overscan: overscan 最早描述的是电视屏幕上实际显示内容的区域，即使到了今天 ，区域之外仍然可能无法显示。边缘部分需要留出 10% 的空间，以便电视可能正确地显示内容
* Color: 与电脑和手机相比，电视上的颜色渲染会不精确， LCD 和 Plasma TV 经常使用 smoothing and sharpening 过滤器，颜色渲染可能与你在电脑上看到的不一致。微妙的明暗区别可能会消失或者加强。你需要避免在屏幕上大块的区域上使用纯白，对高饱和颜色（特别是红色，绿色和蓝色），如果你要在重要的区域上使用他们，需要对他们进行复查。你还要避免使用比较暗的颜色，电视的设置可能会导致这些颜色难以分辨。
* Typography: 文本和控件的大小应该容易阅读和导航，字体最小为 12sp，默认为 18sp，下面是推荐的一些设计准则
    - Card Titles: Rototo Condensed 16sp
    - Cars Subtext: Rototo Condensed 12sp
    - Browse Screen Title: Roboto Regular 44sp
    - Browse Category Title: Roboto Condensed 20sp
    - Details Content Titles: Roboto Regular 34sp
    - Details Subtext: Roboto Regular 14sp
* Text: 在电视应用上要小用文字，用户和电视的距离使得他们很难阅读文字，下面有些应用中使用文字的建议
    - 将文字分成小块，使用户可以快速浏览
    - 在暗背景上使用亮文字，这样在电视上更容易阅读 
    - 避免字体笔画太宽或者太紧，使用简单的 sans-serif 字体增加可读性
    - 使用相对字体大小而非绝对大小 

## Auto

Android Auto 为交通工具提供了标准的用户接口和用户交互模式

### Overview Screen

当用户第一次将 Android 设备连接到汽车时，会显示 Overview 屏幕，这个屏幕基于用户位置，时间等显示与环境相关的卡片。用户可以查看提醒，并使用声音回复。

### Audio App Lancher

在活动栏按耳机图标，用户可以看到一个列表，列有所有与声音相关的应用

### Primary App UI

用户选择与声音相关的应用后，会显示应用交互界面。默认自动显示标准的 UI，但是你也可以定制这个UI，显示你的图标，应用名，背景图片。

* User Action: 在应用主UI的多媒体控制卡片上支持四个主要动作，四个辅助动作，以及一个返回动作，你可以使用标准控件，也可以自己定制动作和图标 
* Drawer List: 由主UI向列表UI过渡后，drawer 就在中间显示出来，定制的列表UI可以显示由应用中多媒体服务提供的多媒体容器及声音文件。


### Day and Night Transitions

所有的 UI 都支持白天和晚上的颜色主题，平台提供了白天和夜晚状态，并且可以自动调整
