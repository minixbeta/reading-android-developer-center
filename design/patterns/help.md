# Help
我们希望保证，如果你遵循了这个网站上给出的建议，每个人都能很容易地学习和使用你的应用。令人悲伤的是事实并非如此。

你的部分用户会遇到问题和难题。他们会在**你的应用内**寻找答案，如果他们找不到，他们可能会离开，并且再也不会回来。

这一页介绍了一些设计模式，用于在你的应用内引入帮助，同时出一些为那些想要得到帮助的用户创建帮助内容的建议。

## Designing Help into Your App
### Don't show unsolicited help, except in very limited cases
通常情况下，你希望每个人都能快速学习到一些窍门，发现一些炫酷的特性，从你的应用中所获甚多。所以，当用户第一次打开你的应用时，
你可能特别想向所有用户展示一些一次性的引导幻灯片，视频，或者启动画面。或者你可能想在用户第一次使用某个特性时，显示气泡文本或者
对话框。

多数情况下，我们建议不要使用这种方式，因为：
* 他们是打断性质的。人们想要开始使用你的应用，任何你放在他们面前的东西，都会让他们感觉到是阻碍或者可能会感觉厌烦，尽管你可能是出
于好意。并且由于这不是他们的主动行为，他们可能不会过多地注意这些。
* 他们经常是没有必要的。如果你对自己的应用的可用性有所担心，不要仅仅给个帮助就算了。试着在 UI 中解决它。使用 Android 设计模式，
风格，构建块，这样会降低用户的教育成本。

采取非主动的方式向用户显示纯帮助内容的唯一理由是：教授高质量的功能，并且这个功能只能通过手势操作来使用。

* 高质量的功能: 没有它，用户就不能使用最常用的功能，来满足他们的需求
* 只能通过手势使用：由于没有菜单或者按钮，用户可能自己永远也无法发现他们。

然而，不是所有的高质量，且只能通过手势使用的功能都需要教程。例如，不用教用户怎么去滑动内容。他们已经知道了，因为这是一个基本的，
系统级的交互方式。

当需要在应用内提供帮助时，最好是让用户主动去找到这些帮助。

### Follow the standard design for navigaitng to help
在应用内的每个界面上，都在动作栏扩展中提供帮助。总是把它当成菜单栏的最后一项，并且命名为“帮助”。

我们把这建立成一个标准的设计模式，这样用户需要帮助时，就不会到处去找了（查看设计准则 [Give me tricks that work everywhere]())

### Assume that every call for help is urgent
除了帮助之外，你可能想要提供其它信息，例如版权信息，致谢，服务条款以及隐私策略。

让用户通过帮助菜单栏访问这些信息，但是需要对用户急需知道答案的问题进行工作流的优化，例如怎么做一些事情或者为什么应用内会发生
某些事情。一小部分会寻找法律条文或者应用作者名字的用户，是不会在意多执行几个步骤的。

同样的道理适用于你可能想提供的一些交流用的选项，例如联系客服或者提交反馈。提供这些选项时，不要在用户看到帮助前再执行额外的步骤。当你把帮助内容放在前面时，会增加用户自己发现他们的机率，这样反过来你自己就不需要费心提供支持了。

当有人选择“帮助”时：

* 不要：显示一个对话框，让用户在帮助以及其它选项之间选择
* 好：显示一个 web 浏览器，包含帮助信息。其它选项放在底栏。
* 更好：在应用内提供帮助界面，并且把其它选项放在动作栏。例如，你想要让用户通过动作栏上的按钮向你发送问题，提供反馈。动作栏扩展是放置用户很少需要的那种非帮助信息的理想位置。这比提供一个浏览器需要更多的开发工作，但是对用户而言是更好的体验，因为他们不需要为了获取帮助而离开你的应用，也不需要联网。

## Principles for Writing On-Screen Help Content
* Help is part of the UI: On-Screen 帮助是你应用 UI 的扩展，而不是对它的描述。从应用的核心到帮助，凡是出现在屏幕上的内容，都应该遵循 [Writing Style]() 准则中说的内容，这样可以提供端到端的无缝体验。
* Make every pixel count: 没有必要把你的应用内的每个小细节都给出文档，尤其是看到 UI 就很容易知道的，或者平台上的标准行为。只显示那些屏幕上没空间显示的关键信息，并且很容易根据内容映射到屏幕上。
* Pictures are faster than words: 在描述关键的 UI 元素，提供 step-by-step 指导时，考虑将文字与图标，屏幕截图与图例以及其它图像 。解释事物时，如果你用很少的语言，用户就能更快的理解其中的意思。
* Help me scan, not read: 用户不会从头到尾阅读帮助。他们四处浏览，寻找对他们需要的答案。不要让信息对用户负担太重，要使用友好的格式和布局，例如粗体的标题，数字或者点号列表，表格，段落间留白。如果你有大量的内容，可以使用滑块分割到多个屏幕中。
* Take me straight to the answer: 有什么比一个容易浏览的界面更好的呢？一个界面不需要浏览，因为答案就在那儿。考虑在你应用中的第个界面中都提供到帮助的导航，此帮助与当前界面对应。我们称之为情景相关帮助，它是帮助用户的圣杯。如果你使用了这种方式，保证你也提供了得到帮助其它内容的方式。
