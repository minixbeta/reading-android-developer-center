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

 
