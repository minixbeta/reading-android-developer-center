# Grid Lists
格子列表是除标准列表外的另一种方式。他们适合于显示那些用图片代表的数据集。与简单列表相比，格式列表可以在水平和竖直方向上滑动。

## Generic Grids
格子列表中的项目可以安排在二维空间上，滑动内容时，其中一个方向是固定的。滑动方向决定了格子列表中项目的顺序。由于滑动方向是不确定
的，要通过切断格子中的项目来传达多余的项目在哪里，让用户容易决定滑动方向。

避免创建可以在两个方向上滑动的格子列表。

### Vertical scrolling
竖直方向的格子列表以传统的西方阅读方向进行排序：从左到右，从上到下。当显示列表时，在最底部切断项目来告诉用户可以向上滑动来显示
更多的项目。确保用户转动屏幕时，这种模式也可以正常使用。

### Horizontal scrolling
水平方向滑动列表固定格子纵轴上的项目。与竖直方向滑动相比，排序的改变仅仅是由从上到下变为从左到右。使用同样的技术在最右的列上切断
项目，在表明滑动方向。

不要使用可滑动选项卡与水平滑动格子列表混合的方式来切换视图，因为水平手势会相互冲突。如果你使用滑动选项卡来作视图导航，同时用了
格子列表，可以使用竖直方向的滑动进行列表导航。

## Grid List with Labels
使用标签来显示格子列表项目的额外信息。

### Style
使用半透明面板，放在格子列表的项目上来显示标签。这让你可以控制对比度，在内容亮度高时，仍然保证标签的可读性。