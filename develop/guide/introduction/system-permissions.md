# System Permissions

Android 每个应用都以一个独立的标识（Linux 用户ID和组ID)运行在系统中，通过这种方式使得应用之间以及应用和系统之间得到隔离。除此之
外，还有更细粒度的安全特性：通过限制特定进程上特定操作的权限机制，每个 URI 都有一个权限，用于访问特定的数据。

更多信息，可以参见 Android 开源项目中的 [Android Security OverView]()

## Security Architecture
默认情况下，任何应用都没有权限对其它应用，操作系统，以及用户执行任何操作。包括读或者写用户数据（例如联系人，邮件），读或者写应用文件，执行网络访问，保持设备处于唤醒状态等等。

由于每个 Android 应用都在进程沙箱内执行操作，应用必需显式地分享资源和数据。它们必须要声明那些基本沙箱没有提供的权限。应用静态地声明他们需要的权限 ，Android 系统会在安装应用时提醒用户授权。Android 没有动态改变权限的机制，这是由于这会使得用户体验和对安全的破坏都变的复杂。

应用沙箱并不依赖于构建应用的技术。特别是，Dalvik 虚拟机并不是安全边界，任何应用都可以在本地代码的方式运行（见 [the Android NDK]())。所有类型的应用——Java的，本地的，混合的——都以同样的方式在沙箱内运行，他们之间有相同程度的安全性。

## Application Signing
所有的 APK (.apk 文件) 都必需使用证书签名，证书私钥在开发者手中。这个证书用于鉴定应用作者身份。证书并不需要被证书机构签名。Android 应用使用自签名的证书是完全可以的。在 Android 中，认证的原因是为了区分作者。这样系统就可以接受或者拒绝应用对 [签名级别权限]() 的访问，接受或者拒绝另一个应用 [对同一Linux标识符的请求]()。

## User IDs and File Access
安装时，Android 会给每个包分配一个不同的 Linux User ID。这个标识在包的整个生命周期内不会变。同一个包在不同设备上也会有不同的标识。

由于安全措施是在进程级别起作用，所以不同的包一般不能运行在同一进程内，因为他们需要以不同的 Linux 用户运行。不过你可以在 AndroidManifest.xml 文件的 manifest 标签中，使用 sharedUserId 属性赋予他们相同的用户 ID。这样，两个包就被当作同一个应用，使用同一用户 ID，有相同的文件权限。注意，为了保证安全，只有相同签名的应用才可以被赋予相同的用户 ID。

任何被应用存储的数据都会被赋予应用的用户 ID，通常其它包不能访问。当使用 getSharedPreferences(String, int), openFileOutput(String, int), 或者 openOrCreateDatabase(String, int, SQLiteDatabase.CursorFactory) 创建文件时，你可以使用 `MODE_WORLD_READABLE` 及 `MODE_WORLD_WRITEABLE` 来允许其它包读写文件。当设置这些标志时，文件拥有者仍然是你的应用，但是可以被其它应用读写。 

## Using Permissions
基本的 Android 应用在默认情况下没有任何权限，这意味着它不会作出对用户体验和数据有害的行为。为了使用设备的一些被保护的特性，你必须在 AndroidManifest.xml 文件中包含一个或多个 <users-permissions> 标签来声明你的应用所需要的权限。

例如，如果一个应用想要监听短信到来的消息，需要这样声明：

```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
  package="com.android.app.myapp"
  <uses-permission android:name="android.permission.RECEIVE_SMS" />
  ...
</manifest>
```

在应用安装的时候，应用安装器就会基于应用声明的权限请求及用户的选择来赋予权限 。应用运行的时候，不需要再为用户检查权限。也就是说，一个应用要么在安装时被赋予相应权限，在运行时就可以使用相应特性，要么权限不被允许，任何企图使用相应特性的请求都会失败，同时不会提醒用户。

通常情况下，权限请求失败会抛出 securityException，但是并不保证在任何时候都出现。多数情况下，权限请求失败都会被打印到系统日志中。

Android 系统提供的权限可以在 [Manifest.permission]() 中找到。任何应用都可以定义自己的权限，所以列表里并不包含所有的可能。

在你的程序执行操作时，可能会在下面这些地方进行权限检查：
* 系统调用时，阻止应用执行特定函数
* 启动活动时，阻止应用从其它应用启动活动
* 发送和接收广播时，控制谁可以接收广播或者谁可以向你发送广播
* 访问及操作内容提供器时
* 绑定或者启动服务时

注意：随着 Android 版本的提升，以前不要求声明的权限，现在可以需要声明了。Android 是根据 targetSdkVersion 来决定某个权限是否需要声明的，所以你需要尽可能地把 targetSdkVersion 提升到最大值。

