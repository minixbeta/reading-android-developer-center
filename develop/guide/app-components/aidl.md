# Android Interface Definition Language(AIDL)
AIDL 用于定义程序接口，客户端与服务器通过进程间通信(IPC)进行交流时，需要使用这此接口。当你需要来自其它应用的客户端连接你的 
Service 时，并且想在 Service 中自己处理多线程问题时，才需要使用 AIDL。

* 本地进程发起的调用，就在当前线程中执行。如果这是主线程，那么线程继续执行 AIDL 接口，如果是另外的线程，那么这是在服务中执行
你的代码的那个线程。也就是说，如果是本地线程访问服务，那么你可以完全控制哪个线程来执行。（不过如果是这样的话，你不应该使用 AIDL）
* 从远程进程发起的调用在一个线程池中被分发，这个线程池由平台在你自己的进程中维护。你必须为来自未知线程的调用做好准备，并且多个
调用可能同时发生，也就是说你必须保证线程安全。
* oneway 关键词可以改变远程线程调用的行为。当使用它时，远程调用不会阻塞，它仅仅发送事务数据，然后马上返回。

## 定义 AIDI 接口

1. 创建 .aidi 文件
这个文件定义了程序接口

2. 实现接口
Android SDK 工程会基于 .aidi 文件，使用 Java 语言生成接口，这个接口有一个名为 Stub 的抽象类，继承了 Binder。你必须继承 Stub 类
然后实现方法

3. 把接口导出给客户端
实现 Service，覆盖 onBind()，返回你实现的 Stub 类

### 1. 创建 .aidi 文件
.aidi 文件使用 Java 语言创建，定义一个接口，并且只需要接口声明及方法标识。

默认情况下，AIDL 支持下面的数据类型：
* Java 基本数据类型
* Sting
* CharSequence
* List
* Map

其它的类型，你需要使用 import 导入

### 2. 实现接口
当你构建应用时，Android SDK 工具会根据 .aidi 文件生成 .java 文件，包含 .aidi 中描述的接口，这个接口包含一个名为 Stub 的子类，
例如 YourInterface.Stub。

为了实现从 .aidl 生成的接口，可以继承生成的 Binder 接口（YourInterface.Stub)，实现其中的方法。

需要注意的是：

* 到来的调用不保证在主线程中执行，你需要从一开始就考虑多线程的问题，保证线程安全
* 默认情况下，RPC 是同步的，如果你知道服务要运行一段时间才能完成请求，不要在主线程中调用 ，这会阻塞应用，你应该在一个独立的线程中调用 
* 异常不会传递给调用者

### 3. 向客户端导出接口
一旦你为 Service 实现了接口，你需要把他们导出给客户端，方法是在 onBind() 中返回 IBinder，这个 IBinder 就是你之前实现 Stub 的那个类的实例。

客户端在调用  bindService() 后，可以在回调函数 onServiceConnected() 中接收到这个 IBinder。

客户端必须有访问接口类的能力，所以客户端应用也需要在 src/ 下有对应的 .aidi 文件。

## 通过 IPC 传递对象
要想通过 IPC 传递对象，对象所属类需要实现 Parcelable 接口，你必须保证：

* 类实现了 Parcelable 接口
* 实现 writeToParcel，将对象当前状态写入 Parcel
* 添加名为 CREATOR 的静态域，实现了 Parcelable.Creator 接口
* 最后，创建 .aidi 文件，声明你的类

### 调用 IPC 方法
为了调用 AIDL 中定义的远程接口，需要执行下面的步骤：

1. 在项目的 src/ 下包含 .aidl 文件
2. 声明 IBinder 接口的实例（基于 AIDL 生成）
3. 实现 ServiceConnection
4. 调用 Context.bindService()，传递你的 ServiceConnection 实现
5. 在 onServiceConnected()中，你会接收到 IBinder 实例
6. 调用接口中定义的方法，捕获 DeadObjectException
7. 通过 Context.unbindService() 断开链接

