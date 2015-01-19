# Tasks and Back Stack
Activity 在启动时，进入 Back Stack。在 Activity A 中可以启动另一个 Activity B，B 可能是当前应用中的，也可能是其它应用中的。启动 B 时，A 的状态会被保留，但会进入 stopped 状态，用户看不到它，B 在前台与用户交互。此时，A, B 构成一个 Task。如果此时按返回按钮，B 会出栈并被销毁，A 进入 resumed 状态，与用户交互。如果在一个任务中时，返回到主屏幕，那么这个任务进入后台。可以从主屏幕启动其它任务。

## 保存 Activity 状态
Activity 进入 stopped 状态后，系统可能在内存不够的时候销毁它，所以你需要在 onSaveInstancesState() 中保存相关状态信息。注意，
虽然被销毁了，但是系统仍然知道这个 Activity 在栈中的位置，当这个 Activity 需要来到前台与用户交互时，如果没有被销毁，那会调用 
onResume()，但是如果销毁了，就会重新创建这个 Activity 了，如果是前一种状态，你不保存相关内容也行，但是万一是后一种状态，Activity
的状态就会消失了。所以，为了保证健壮性还是需要自己保存状态的。

## 管理 Tasks
