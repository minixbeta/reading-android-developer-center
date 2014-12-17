# Widgets

挂件是主屏幕定制的一个基本方式。你可以把他们想像成，在用户主屏幕上瞟一眼就能看到应用最重要的数据，使用其功能。用户可以在主屏幕
面板上移动挂件，如果支持的话，也可以调整他们的大小，以便按照他们的喜好定制挂件内的信息量。

## Widget types
在你为挂件做计划时，要想好你想要的是哪种挂件。挂件通常分成下面这几类：

### Information widgets
信息类的挂件通常显示少量最重要的信息元素，他们对用户来说非常重要，并且需要跟踪信息随时间的改变。信息类挂件的一个好的例子是天气
挂件，钟表挂件或者比赛比分记录。点击挂件上的信息通常会启动相关的应用，打开挂件中信息的详情。

### Collection widgets
从名字就可以看出，集合类挂件会显示同种类别的多个元素，例如图片浏览应用中的多个图片，新闻应用中多篇文章或者交流用的应用中多个邮件
或者消息。集合类挂件通常聚焦于两个方面，浏览集合，并且打开 其中一个元素的详情。集合类挂件可以在纵向滑动。

### Control widgets
控制类挂件的主要目的是显示那些常用的功能，让用户可以直接在主屏幕上打开，而不用打开应用。把他们当成对应用的远程控制。控制类挂件的
一个典型的例子是音乐类应用挂件，可以让用户在应用外就可以播放，暂停，或者跳过音乐。
与控制类挂件的交互可能会与详情界面相关，也可能不相关，这个依赖于控制类控件是否会产生一个数据集合，例如搜索类控件。

### Hybrid widgets
虽然所有挂件都倾向于属于上述的三种类型之一，但是许多挂件属于混合类型，将不同类型的元素组合在一起。

根据你对挂件的计划，将你的挂件围绕基本类型设计，如果有必要的话，再添加其它元素。

音乐播放器挂件主要是一个控制挂件，但是会告诉用户正在播放的是哪首音乐。它将控制挂件与信息类挂件结合在一起。

## Widget limitations
虽然挂件可以被理解成“微型应用”，但是在你开始着手设计你的挂件之前，仍然有一些限制，理解他们是非常重要的：

### Gestures
由于挂件在主屏幕上，他们必须和建立在那里的导航共存。与完整的应用相比，这限制了挂件支持的手势操作。例如支持 view pager 的应用可以让用户在屏幕上通过侧滑导航，但是在主屏幕上，侧滑已经被设置成在主屏幕面板之前切换。
挂件支持的手势只有：
* 触摸
* 纵向滑动

### Elements
在上面的交互限制下，一些需要使用限制手势的 UI 构建块块在挂件中就无法使用了。一个完整的构建块列表以及更多的布局限制信息，请参考 [App Widgest]() API 指南中的 “创建应用挂件布局”。

## Design guidelines
### Widget content
挂件是通过“广告”的形式，使用新鲜有趣的内容来吸引用户的良好的机制。
正如报纸上的“悬疑式”广告一样，挂件需要对应用的信息进行加强，并且提供通向应用内详情的链接；换句话说，挂件挂件是信息中的“点心”，
而应用是“正餐”。底线是，保证应用显示的详情比挂件已经显示的要多。

### Widget navigation
除了纯粹的信息内容之外，你应该考虑让你的挂件提供通向应用内最常用信息所在区域的链接。这让用户可以快速完成任务，同时将应用内的功能延伸到了主屏幕上。
挂件上可以使用的一些好的导航链接如下：
* 打开应用的顶层界面：点击一个信息元素通常会让用户进入低层的详情信息界面。提供通向顶层的渠道可以使得导航更灵活，并且可以替代用户在主屏幕上建立的，用于进入应用的快捷方式。万一你要显示的数据是模棱两可的，可以使用应用的图标来进行自我解释可以让你的控件有一个清晰的标识。

### Widget resizing
自 3.1 版本开始，Android 就向平台中引入了可变大小的挂件。用户可以在主屏幕面板的限制下调整挂件的高度的宽度。你可以决定挂件是否可以自由地调整，或者对高度和宽度大小改变作出限制。如果挂件是固定大小的，你可以不支持对大小的改变。
让用户可以改变挂件大小有以下好处：
* 他们可以调整自己想看到的挂件中的信息量
* 他们可以很好地调整主屏幕上挂件和快捷方式的布局

调整大小的策略取决于你创建的挂件的类型。列表或者格子类型的集合类挂件是显而易见的，因为调整他们的大小只是简单地扩大或者缩小纵向可滑动区域。无论挂件多大，用户都可以通过滑动查看视图内的所有信息元素。另一方面，信息类的挂件需要更多的郭雪芙，因为他们是不可以滑动的，所有的内容都在给定的大小内。你可以根据用户调整后的挂件大小 ，动态地调整挂件的内容和布局。

在上面的这个简单的例子中，用户可以在水平方向上调整天气挂件的大小，通过4个步骤，展示出与天气相关的更多的信息。

对每个挂件来说，大小决定了应用内有多少信息浮现出来。如果挂件很小，可以展示最重要的信息，随着挂件变大，可以加入更多与情境相关的信息。

### Layout considerations
根据你使用的设备或者开发用的设备的尺寸去调整挂件大小是非常吸引人的。在你为挂件设置布局时，记得下面这些：
* 设备与设备之前，格子的个数，大小及空间都是不同的，因此，灵活的挂件是非常重要的，他们可能比预计的容纳下或多或少的空间。
* 实际上，随着用户对挂件大小的调整，系统会调整挂件可以绘制的 dp 大小的范围。调整你的挂件策略，使它根据块大小 而不是格子尺寸大小来调整，会得到更可靠的结果。

### Widget configuration
有时候挂件在使用之前需要被设置。例如一个邮件挂件，在收件箱可以显示前，你需要设置帐户。或者一个静态的图片挂件，你需要事先设置图片，之后才能显示。
Andorid 挂件在他们被放在主屏幕上时，会显示他们的配置选项。保持挂件配置信息的精简，不要多于2到3个设置。使用对话框形式而不是全屏幕的活动式的界面去显示配置选项，并且保留用户所在位置的场景，即便这样做需要显示更多的对话框。

一旦设置后，通常没有过多的理由去访问设置。因此， Andorid 挂件不会显示一个设置或者配置按钮。

## Checklist
* 在挂件上，关注于那些看一眼就能知道的信息。对你应用内的信息进行扩展。
* 根据你的目的选择正确类型的挂件 
* 对可以调整大小的挂件，计划好不同大小下要显示的内容
* 保证挂件布局可以扩大和缩小，让你的挂件独立于屏幕方向和设备