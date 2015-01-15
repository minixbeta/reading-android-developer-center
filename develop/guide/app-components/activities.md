# Activitys
 活动是用于与用户交互的界面。当用户启动应用后，会处于一个主活动中，在活动中，可以启动另一个活动，点返回按钮，回到上一个活动，
 遵循栈后进先出的机制。
 活动的生命周期中，有多个状态，例如恢复，停止，销毁。状态切换时，会调用活动的回调函数，让你有机会在状态切换时执行合适的动作。
 
 ## Creating an Activity
 要创建一个活动，需要创建 Activity 的子类，子类中实现 onCreate() 函数，这个函数会在活动创建过程中被调用，函数内需要实现用户接口，主要通过定义一个界面布局文件，再在 onCreate() 中调用 setContentView() 来实现。同时，为了让系统知道这个活动的存在，需要在 Manifest 文件中定义这个活动。
 
```
<manifest ...>
 <application ...>
  <activity android:name=".ExampleActivity" />
 </application ...>
</manifest>
```

如果你的活动可以用来处理其它意图请求，可以在 Manifest 的 activity 中添加 <intent-filter>

## Starting an Activity
可以通过 startActivity 来启动活动，在参数中可以明确指出活动对应的类，显式地启动一个活动。也可以在参数中指定一个动作，隐式地启动一个活动，由系统通过 intent-filter 找到可以处理这个动作的活动。

如果想在启动活动后，返回一个结果，并对这个结果进行处理。可以使用 startActivityForResult() ，然后再定义 onActivityResult() 回调函数，在这个函数中对返回结果进行处理。

## Shutting Down an Activity
关闭活动可以调用  finish() 或者 finishActivity()，但是最好不要显式地调用这两个函数，活动的生命周期可以由系统来管理。

## Managing the Activity Lifecycle
活动生命周期是通过对各种回调函数的实现来管理的。

活动可以处于三种基本状态：

* Resumed: 活动处于前台，可与用户交互
* Paused: 另一个活动在前台，与用户交互，但是处于 Paused 状态的活动仍然是可见的，只是不是完全可见
* Stopped: 活动完全不可见

### Implementing the lifecycle callbacks

```
@Override
public void onCreate(Bundle savedInstanceState) {
 super.onCreate(savedInstanceState);
 // 活动被创建
}

@Override
protected void onStart() {
 super.onStart();
 // 活动即将可见
}

@Override
protected void onResume() {
 super.onResume();
 // 活动处于可见态 (resumed)
}

@Override
protected void onPause() {
 super.onPause();
 // 另一个活动占据了焦点，本活动处于 paused
}
 
@Override
protected void onStop() {
 super.onStop();
 // 活动不可见，处于 stopeed
}

@Override
protected void onDestroy() {
 super.onDestroy();
 // 活动即将销毁
}
```

调用 onPause(), onStop(), onDestroy() 之后，系统就可以销毁活动了，所以如果有什么东西需要保存，记得在相应回调函数内保存。

### Savring activity state
状态切换时，可能需要保存一些活动的状态信息，以免系统杀死活动后，用户又返回这个活动时，再创建新活动时，刚才的活动状态消失了。

系统会使用 onSaveInstanceState() 保存有 id 的控件的状态，并在再次创建时使用onRestoreInstanceState() 恢复，如果你还有额外的东西需要保存，也可以重新实现 onSaveInstanceState()，但是记得这函数是用来保存 UI 的状态信息的，不是用来保存持久化数据的。并且系统也不保证所有情况下都调用 onSaveInstanceState()，例如，如果是用户退出应用，系统当然就不会保存 UI 状态。

### Handling configuration changes
当配置变化时，比如屏幕方向改变时，系统可能会使用新的布局，重新创建 UI 组件，这时候，你就要保证 UI 的状态及时保存与恢复。

### Coordinating activities
如果活动A启动了活动B，那么它们的回调函数调用顺序是：

1. 活动 A 的 onPause() 函数
2. 活动 B 的 onCreate(), onStart(), onResume()
3. 如果活动 A 不可见了，那么 onStop() 会被执行
