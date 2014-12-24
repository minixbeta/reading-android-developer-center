# Style for TV

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
