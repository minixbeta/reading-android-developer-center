# Tasks and Back Stack
Activity 在启动时，进入 Back Stack。在 Activity A 中可以启动另一个 Activity B，B 可能是当前应用中的，也可能是其它应用中的。启动 B 时，A 的状态会被保留，但会进入 stopped 状态，用户看不到它，B 在前台与用户交互。此时，A, B 构成一个 Task。如果此时按返回按钮，B 会出栈并被销毁，A 进入 resumed 状态，与用户交互。如果在一个任务中时，返回到主屏幕，那么这个任务进入后台。可以从主屏幕启动其它任务。

