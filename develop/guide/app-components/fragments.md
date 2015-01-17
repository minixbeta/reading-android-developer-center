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

## 管理 Fragments
为了管理 activity 中的 fragments，你需要使用 FragmentManager，在 activity 中使用 getFragmentManager() 可以得到它，它可以用来：
* 获取活动中存在的 fragments，使用 findFragmentById() 或者 findFragmentByTag()
* 从返回栈中弹出 fragments，使用 popBackStack()
* 为返回栈的变化注册监听函数，使用 addOnBackStackChangedListener()

## 执行 Fragment 事务
执行 Fragment 事务需要用到 FragmentTransaction，它可以这样得到：

```
FragmentManager fragmentManager = getFragmentManager();
FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
```

可以使用 FragmentTransaction 执行一系列动作，包括 add(), remove(), 和 replace() ，最后使用 commit() 进行提交。

在 commit 之前，可以调用 addToBackStack()，将当前 fragment 状态添加到返回栈中，这样 commit 之后，可以通过返回按钮返回之前的状态。 

## 与 Activity 交流
Fragment 可以通过 getActivity() 得到它所在的 activity。

为了在 fragment 与其所在的 activity 之间共享事件，可以在 fragment 内定义一个接口，让其所在的 activity 实现这个接口。在 fragment 的 onAttach 函数中，将参数 activity 转化成这个接口，保存为 fragment 的私有变量。 然后， 当特定事件发生时， 使用这个私有变量调用接口内的函数。 这样，当 fragment 内有事件发生时，就能告诉 activity，activity 就知道怎么处理这个事，比如
改变其它 fragment 的状态。
 
### 向 Action Bar 中添加项目
可以通过在 fragment 中实现 onCreateOptionsMenu() 来向 Action Bar 中添加项目，但是需要在 onCreate() 中调用 setHasOptionsMenu() 函数，以表明这个 fragment 会在 Action Bar 中添加可选菜单。

当其中的菜单项被单击时，会调用 fragment 中的 onOptionsItemSelected() 函数，所以你需要实现这个函数。

同样，你可以在 fragment 的布局中，注册一个视图，来提供 context 菜单，这可以通过 registerForContextMenu() 来实现 。当用户打开 context 菜单时，会调用 fragment 的 onCreateContextMenu()，当用户选择一个项时，要调用 fragment 的 onContextItemSelected()。

## 处理 Fragment 生命周期
Fragment 生命周期管理与 Activity 很像，它们都有三个状态：

* Resumed
* Paused
* Stopped

二者生命周期最大的不同是，Activity 压入返回栈是由系统决定的，而 Fragment 压入返回栈需要显式调用 addToBackStack()

### 与 Activity 生命周期的配合
Activity 的生命周期直接影响 Fragment 的生命周期。

Fragment 与 Activity 生命周期相比，多了几个回调函数：

* onAttach(): 当 fragment 与 activity 关联时
* onActivityCreated(): 当 activity 的 onCreate() 调用返回时
* onDestroyView(): 当与 fragment 的层级相关的视图销毁时
* onDetach(): 当 fragment 与 activity 解除关联时

除此之外，当 activity 调用 onPause() 等时，fragment() 也调用相应的函数。当 activity 处于 resumed 状态时，可以对 fragment 进行
添加，替换，移除。

## 示例
