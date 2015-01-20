# Tasks and Back Stack
Activity 在启动时，进入 Back Stack。在 Activity A 中可以启动另一个 Activity B，B 可能是当前应用中的，也可能是其它应用中的。启动 B 时，A 的状态会被保留，但会进入 stopped 状态，用户看不到它，B 在前台与用户交互。此时，A, B 构成一个 Task。如果此时按返回按钮，B 会出栈并被销毁，A 进入 resumed 状态，与用户交互。如果在一个任务中时，返回到主屏幕，那么这个任务进入后台。可以从主屏幕启动其它任务。

## 保存 Activity 状态
Activity 进入 stopped 状态后，系统可能在内存不够的时候销毁它，所以你需要在 onSaveInstancesState() 中保存相关状态信息。注意，
虽然被销毁了，但是系统仍然知道这个 Activity 在栈中的位置，当这个 Activity 需要来到前台与用户交互时，如果没有被销毁，那会调用 
onResume()，但是如果销毁了，就会重新创建这个 Activity 了，如果是前一种状态，你不保存相关内容也行，但是万一是后一种状态，Activity
的状态就会消失了。所以，为了保证健壮性还是需要自己保存状态的。

## 管理 Tasks
一般情况下，系统会为你管理好 Task，启动 Activity 时入栈，按返回按钮时出栈，后进先出。但是某些情况下，你可能会有特别的需求，例如
启动 Activity 时开一个新的 Task，而不是压入当前 Task，或者如果 Activity 已经有实例在栈中，就使用这个实例，而不是新生成一个，或者
想清空栈。那么，你可以在 Manifest 的 activity 标签下使用下面几个属性，在 startActivity 中使用一些标志：

<activity> 属性：
* taskAffinity
* launchMode
* allowTaskReparenting
* clearTaskOnLaunch
* alwaysRetainTaskState
* finishOnTaskLaunch

intent 标志：
* FLAG_ACTIVITY_NEW_TASK
* FLAG_ACTIVITY_CLEAR_TOP
* FLAG_ACTIVITY_SINGLE_TOP

注意：多数情况下你不需要自己管理 Tasks，如果真要自己定制，需要仔细测试，确保不会出现用户意料之外的现象。

### 定义启动模式
启动模式的定义影响 Activity 与 Task 的关系，定义方式有两种：使用 manifest 或者使用 Intent 标志。注意有些启动模式 **只在** manifest 中才能定义，有些 **只在** Intent 中才能定义。

### 使用 manifest 文件
在 manifest 文件的 <activity> 元素下，launchMode 属性：
* standard: 默认模式，activity 启动时，会创建新实例，activity 可多次实例化，属于不同 Task，一个 Task 可能有多个实例
* singleTop: 如果启动的 activity 在 back 栈的栈顶，那么会直接使用这个 activity，而不会实例化新实例。如果启动其它 activity，会实例化一个新的 activity，放在栈顶
* singleTask: 每个 activity 只有一次实例。如果 back 栈中是 (activity 2, activity 1)，后台 Task 中有 (activity y, activity x)，如果 activity 2 启动了 activity y，那么，back 栈会变成 (activity y, activity x, activity 2, activity 1)
* singleInstance：与 singleTask 相同，只是 一个 activity 只会是 task 的唯一成员。

### 使用 Intent 标志
可以在 startActivity() 时指定 Intent 标志，控制 activity 与 task 的关系。

* FLAG_ACTIVITY_NEW_TASK: 与 singleTask 行为一致
* FLAG_ACTIVITY_TOP: 与 singleTop 行为一致
* FLAG_ACTIVITY_CLEAR_TOP: 如果启动的 activity 已经在 back 栈中了，那么这个 activity 上面的那些 activity，都会被销毁，这个 activity 会成为栈顶元素，与用户交互。

### 处理 affinities
affinity 表示 activity 属于哪个 task。默认情况下，同一应用中的 activity 有同一 affinity，所以他们默认情况下属于同一 task。但是你也可以自己调整，让来自不同应用中的 activity 有相同的 affinity，或者让同一应用中的 activity 有不同 affinity。

可以通过 manifest 文件中的 <activity> 元素中的 taskAffinity 属性来设置 affinity。

affinity 在下面两种情况下可能有用：
* 当 intent 启动的 activity 包含 FLAG_ACTIVITY_NEW_TASK时：此时启动新 activity，会生成一个新 task，但是其实没必要这样，如果已经有一个 task 与此 activity 有相同 affinity，那么这个 activity 会进入这个 task
* 当 activity 的 allowTaskReparenting 属性被设置成 true时：在这种情况下，activity 可以从启动时的 task 移动到有相同 affinity 的那个 task 中去（当这个 task 进入前台时）

### 清除 back 栈
如果用户离开一个 task 太久，那么系统会清除 back 栈中除了栈顶外的其它所有 activity，因为时间那么久了，用户可能已经不需要那些状态了。如果你想改变这一行为，可以设置下面的属性：

* alwaysRetainTaskState: 如果设置为 "true"，那么所有 activity 都会被保存在栈中
* clearTaskOnLaunch: 如果设置为 "true"，无论用户离开多短的时间，activity都会被清除
* finishOnTaskLaunch：与 clearTaskOnLaunch相似，只不是针对单个 activity的，如果设置为 true，activity 只在当前会话中被保存，如果用户离开后再返回，就不会显示这个 activity了。

### 启动 task
可以将一个 activity 的 intent-filter 中的 action, category 分别设置为 "android.intent.action.MAIN"，"android.intent.category.LAUNCHER" ，让这个 activity 成为任务的入口点。用户可以在应用启动器上看到它。

如果 activity 设置成 "singleTask" 或者 "singleInstance" ，那么需要设置 MAIN 及 LAUNCHER，不然这些单个任务的 activity，一旦回到主屏幕，想再回到 task 中去就不行了。
