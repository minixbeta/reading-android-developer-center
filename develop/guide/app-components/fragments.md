# Fragments
Fragments 是活动的一部分，可以把多个片段组合在同一活动内，同一片段可以方便的复用。Fragments 有自己的生命周期，可以把它理解为子
活动。

## 设计哲学
Fragments 是在 Android 3.0 (API level 11) 中引入的，主要是为了在为大屏幕设计 UI 时，可以有更多的灵活性。 Fragment独立处理自己的事件，有自己的布局。为平板设计 UI 时，
可以设计多个独立的 Fragment，再组合起来。如果是为手机设计，只用一个主要的 Fragment 就行，其它
Fragment 放在其它活动里。这样，Fragment 就实现了复用。也使得多屏幕适配的开发变得容易。

## 创建 Fragment
为了创建一个 Fragment，需要创建 Fragment 的子类，实现几个回调函数：

* onCreate(): 初始化组件
* onCreatView(): 加载布局，创建 UI
* onPause(): 用户要离开这个 Fragment 了，可以在这保存 Fragment 中的数据

### 添加用户接口
为 Fragment 创建一个 XML 布局文件，在 onCreateView() 中，使用 inflater.inflate() 加载布局，并返回得到的 View。

将 Fragment 添加到 Activity 有两种方式，一种是在 Activity 布局文件中使用 <fragment> 标签，并指定相应的 Fragment 类名。另一种是
使用代码添加，使用 FragmentManager 得到一个FragmentTransaction，再使用 FragmentTransaction 的 add, commit 函数添加。

### 添加无 UI 的 Fragment
Fragment 也可以没有 UI，在后台运行，这时候就不用在 onCreateView() 中加载布局了。
