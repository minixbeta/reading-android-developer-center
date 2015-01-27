# Bound Services
bound service 是 客户端-服务器 接口中的服务端。bound service 可以被其它组件绑定，发送请求，收取回复，甚至执行进程间通信。

这篇文档讲的是如何创建 bound service，包括如何从其它应用组件绑定服务。

## 基础
bound service 是 Service 类的一个实现，可以让其它应用绑定到它，与它通信。你需要实现 onBind() 回调函数，返回 IBinder 对象，IBinder 定义了程序接口，客户端可以通过这个接口与服务端通信。

客户端可以通过调用 bindService() 来绑定服务。但客户端必须要提供一个 ServiceConnection 的实现，监视与服务端的连接。bindService()
调用后会立即返回，但是没有返回值。当 Android 系统创建客户端与服务端的连接时，会在 ServiceConnection 上调用 onServiceConnected() 函数，并把 IBinder 传递给它。

多个客户端可以连接到同一服务端，但是只有第一次连接的时候会调用 onBind() 生成 IBinder，之后的连接都使用第一次生成的 IBinder。当最后一个客户端与服务端解除绑定时，系统会销毁 service。

## 创建 Bound Service
创建 Bound Service 的关键是返回 IBinder 对象，下面是实现 IBinder 的三种方式：

* 扩展 Binder 类：如果你的服务只在你的应用中使用，可以使用这种方式
* 使用 Messenger: 如果你想让接口跨越不同的进程，由于消息队列在同一线程中，你不需要考虑线程安全问题
* 使用 AIDL：如果你的服务要同时处理多个请求

注意：多数应用不需要使用 AIDL，因为多线程会导致复杂的实现。

### 扩展 Binder 类
使用方式是：
1. 在 service 中，创建 Binder 的实例，并且 Binder 满足下面条件：
  - 包含客户端可以调用的 public 方法
  - 返回当前 service 的实例，实例包含客户端可以调用的方法
  - 返回另一个类的实例，包含客户端可以调用的方法，service包含这个实例
2. 在 onBinder() 回调函数中返回这个 Binder 实例
3. 在客户端，通过 onServiceConnected() 回调方法接收 Binder 实例


### 使用 Messenger

下面是如何使用 Messenger 的总结：

对 service 来说，

* service 实现 Handler，客户端的每次调用都会调用 Handler 中的回调函数
* Handler 用于创建 Messenger
* Messager 创建 IBinder，service 会在 onBind() 中把这个 IBinder 返回
* 客户端使用 IBinder 实例化 Messenger，向 service 发送
* service 在 Handler 的 handleMessage() 中接收 Message

对客户端来说，使用 IBinder 创建 Messenger，然后可以使用这个 Messenger 的 send 函数发送 Message

## 绑定到 Service

要绑定到一个 service ，你必须：

1. 实现 ServiceConnection: 覆盖 onServiceConnected()，系统会通过调用这个函数传递 IBinder; 覆盖 onServiceDisconnected()，当到 service 的连接意外中断时调用
2. 调用 bindService()，传递 ServiceConnection 的实现
3. 当系统调用 onServiceConnected() 回调函数时，你可以开始调用 service
4. 要断开到 service 的连接，使用 unbindService()

### 注意
* 你必须捕获 DeadObjectException 异常，当连接中断时抛出
* 对象在进程间通过引用计数
* 需要注意 绑定-解绑定 成对出现:
  - 如果你只想在客户端可见时与 service 交互，可以在 onStart() 中绑定，在 onStop() 中解绑定
  - 如果你想让 activity 在后台仍然可以接收 service 的响应，可以在 onCreate() 中绑定，onDestroy() 中解绑定

另外，不要在 onResume() 和 onPause() 中绑定和解绑定，它们可能被频繁调用，并且由于调用次序的原因可能会出错。

## 管理 Bound Service 生命周期
如果是 bound service ，一般不用显式地管理生命周期，Android 会在所有客户端都解绑定时销毁。
