# Overview Screen
Overview Screen 是一个系统级的 UI，列出了最新使用的 activities 和 tasks。你可以从中选择一个进入其前台，或者把它移除。
在 Android 5.0 中，同一 activity 可以有多个实例，包含不同文档，都在 overview screen 中。

## 向 Overview Screen 中添加 Tasks
### 使用 Intent 标志添加 task
使用 ActivityManager.AppTask 类的 startActivity() ，为 activity 创建一个文档。为了让系统把 activity 当作一个新的 task 放在 
overview screen 中，可以使用 FLAG_ACTIVITY_NEW_DOCUMENT 标志作为 addFlags() 的参数。如果同时设置了 FLAG_ACTIVITY_MULTIPLE_TASK 
标志，系统总是会为 activity 创建一个新的 task。

### 使用 activity 属性添加 task
manifest 文件中的 <activity> ，属性为 android:documentLaunchMode，值为：

"intoExisting": activity 重用已经存在的 task，与设置 FLAG_ACTIVITY_NEW_DOCUMENT 但是没有设置 FLAG_ACTIVITY_MULTIPLE_TASK 行为一致
"always" ：即使文档已经打开，也要为文档创建一个新任务，与设置 FLAG_ACTIVITY_NEW_DOCUMENT 并且设置 FLAG_ACTIVITY_MULTIPLE_TASK 行为一致
"none": activity 不会为文档创建新的 task, 只会显示此应用的唯一 task，回到上一次调用时的 activity 中
"never": activity 不会为文档创建新的 task，设置此值会覆盖 FLAG_ACTIVITY_NEW_DOCUMENT 及 FLAG_ACTIVITY_MULTIPLE_TASK


