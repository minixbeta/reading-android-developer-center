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

