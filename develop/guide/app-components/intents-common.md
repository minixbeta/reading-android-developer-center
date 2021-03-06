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

## 联系人应用
### 选择联系人
使用 `ACTION_PICK` 动作，指定 MIME 类型为 `Contacts.CONTENT_TYPE`
### 选择特定的联系人数据
如果你想要得到联系人手机号，邮件地址或者其它数据，可以使用 `ACTION_PICK ` 动作，并指定不同的 MIME 类型，例如手机号可以指定为 `CommonDataKinds.Phone.CONTENT_TYPE`
### 查看联系人
为了显示一个已知联系人的详细内容，可以使用 ACTION_VIEW 动作，并使用 content:<URI> 作为 URI 指定联系人
### 编辑联系人
`ACTION_EDIT` 作为动作，content:<URI> 指定联系人，使用 [ContactsContract.Intents.Insert]() 中的定义作为 Extras，指定特定的域。
### 插入联系人
`ACTION_INSERT` 作为动作，`Contacts.CONTENT_TYPE`作为 MIME 类型，使用 [ContactsContract.Intents.Insert]() 中的定义作为 Extras，指定特定的域。

## 电子邮件
### 编写电子邮件（附件可选）
使用下面的动作：
* ACTION_SENDTO(没附件）
* ACTION_SEND(一个附件)
* ACTION_SEND_MULTIPLE(多个附件）

MIME 中指定 `PLAIN_TEXT_TYPE` 或者 `*/*`

Extras 中指定 Email 地址，主题等等。

##　文件存储
### 获取特定类型的文件

* `ACTION_GET_CONTNET`: 选择文件并返回其引用，如果以后还需要用，要复制到你的应用管理范围内
* `ACTION_OPEN_DOCUMENT`：选择文件，可以就地修改，即使是由其它应用管理的
* `ACTION_CREATE_DOCUMENT`：创建文件

onActivityResult() 接收返回结果，如果想选择多个文件，可以将 `EXTRA_ALLOW_MULTIPLE` 设置成 true。　

## 健康
### 自行车
跟踪自行车时，使用 `ACTION_TRACK` 动作， 将 `vnd.google.fitness.activity/biking` 作为 MIME 类型，启动与停止可以使用 `EXTRA_STATUS`，启动时值为 `STATUS_ACTIVE`，停止时，值为 `STATUS_COMPLETED`。
### 跑步
与自行车一样，只是　MIME 类型中　biking 修改为　running
### 练习
与自行车一样，只是　MIME 类型中　biking 修改为　other
### 显示心率
`ACTION_VIEW` 作为动作，将`vnd.google.fitness.data_type/com.google.heart_rate.bpm` 作为　MIME 类型。
### 显示走路步数
`ACTION_VIEW` 作为动作，将`vnd.google.fitness.data_type/com.google.step_count.cumulative` 作为 MIME 类型。

## 本地动作
### 叫出租车
使用 `ACTION_RESERVE_TAXI_RESERVATION` 作为动作。

## 地图
使用 `ACTION_VIEW` 作为动作，并在数据里设置位置信息。

##  音乐或视频
使用 `ACTION_VIEW` 作为动作，并在数据里设置文件位置信息。

如果需要基于搜索结果进行播放，使用 `INTENT_ACTION_MEDIA_PLAY_FROM_SEARCH` 作为动作。同时可以使用 `EXTRA_MEDIA_FOCUS` 指定搜索
模式。

## 手机
使用 `ACTION_DIAL` 动作，在 URL 模式里指定手机号码。当播号应用打开时，会显示手机号码，但是用户必须点拨号，才拨通。如果想直接拨通，可以使用 `ACTION_CALL`。

## 搜索
使用特定应用搜索，如果在你的应用内，使用 `ACTION_SEARCH` 作为动作，如果使用 Google Now，使用 `com.google.android.gms.action.SEARCH_ACTION` 作为动作，在 Extras 中，使用 `QUERY` 作为动作。

如果想使用 Web 搜索，可以用 `ACTION_WEB_SEARCH` 作为动作。 

##  设置
为了打开系统设置中的某个界面，可以使用下面这些作为动作

* ACTION_SETTINGS
* ACTION_WIRELESS_SETTINGS
* ACTION_WIFI_SETTINGS
* ...

## 文本消息
要想发短信，可以使用下面这些作为动作，在 Extras 中指定主题，内容，手机号等内容

* ACTION_SENDTO
* ACTION_SEND
* ACTION_SEND_MULTIPLE

## Web  浏览器
如果想打开 Web 页面，可以使用 `ACTION_VIEW` 作为动作，并且在意图数据中指定 web URL。

## 使用 Android Debug Bridge 验证意图
如果你想要你的应用对意图作出响应，可以使用 adb 发起意图：

1. 将 Android 设备设置为开发者模式
2. 安装你的应用
3. 使用 adb 发起意图

```
adb shell am start -a <ACTION> -t <MIME_TYPE> -d <DATA> \
  -e <EXTRA_NAME> <EXTRA_VALUE> -n <ACTIVITY>
```
4. 如果你的应用定义了意图过滤器，那么它应该可以处理这个意图

## 使用 Google Now 发起意图
Google Now 可以识别声音命令，并发起意图。如果你的应用可以处理这些意图，那么可以通过 Google Now 启动你的应用。

