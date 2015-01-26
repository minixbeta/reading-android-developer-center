# Bound Services
bound service 是 客户端-服务器 接口中的服务端。bound service 可以被其它组件绑定，发送请求，收取回复，甚至执行进程间通信。

这篇文档讲的是如何创建 bound service，包括如何从其它应用组件绑定服务。

## 基础
bound service 是 Service 类的一个实现，可以让其它应用绑定到它，与它通信。你需要实现 onBind() 回调函数，返回 IBinder 对象，IBinder 定义了程序接口，客户端可以通过这个接口与服务端通信。

客户端可以通过调用 bindService() 来绑定服务。但客户端必须要提供一个 ServiceConnection 的实现，监视与服务端的连接。bindService()
调用后会立即返回，但是没有返回值。当 Android 系统创建客户端与服务端的连接时，会在 ServiceConnection 上调用 onServiceConnected() 函数，并把 IBinder 传递给它。

多个客户端可以连接到同一服务端，但是只有第一次连接的时候会调用 onBind() 生成 IBinder，之后的连接都使用第一次生成的 IBinder。当最后一个客户端与服务端解除绑定时，系统会销毁 service。
