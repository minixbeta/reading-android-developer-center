# 通用意图
意图可以让你通过描述动作，提供数据，启动其它应用中的组件。这一节描述了几个隐式意图，你可以用他们执行一些通用的动作。

## 警告闹钟
### 创建警告
要创建一个警告，需要使用 ACTION_SET_ALARM 动作，并通过 Extras 指定警告的详细数据，例如时间，信息。
### 创建定时器
要创建一个定时器，需要使用 ACTION_SET_TIMER 动作，并通过 Extras 指定定时器细节，例如持续时间
### 显示所有警告
为显示警告列表，使用 ACTION_SHOW_ALARMS

## 日历
### 添加日历事件
为了向用户日历中添加一个新事件，可以使用 `ACTION_INSERT` 动作，再指定数据 URI 为 `Events.CONTENT_URL`，同时可以在 Extras 中指定
事件标题，开始时间，结束时间等等。

## 摄像头
### 拍照或者录相并返回
打开摄像头应用，返回照片或者视频，可以使用 `ACTION_IMAGE_CAPTURE ` 或者 `ACTION_VIDEO_cAPTURE` 动作。可以在 Extras 中指定 EXTRA_OUTPUT 为 URI，指定存储位置。
### 启动照相机应用并保持图片模式
使用 `INTENT_ACTION_STILL_IMAGE_CAMERA` 动作
### 启动照相机应用并保持视频模式
使用 `INTENT_ACTION_VIDEO_CAMERA` 动作
