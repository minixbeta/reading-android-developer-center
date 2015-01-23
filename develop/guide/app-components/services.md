# Services
Service 是运行在后台的组件，没有 UI，适合运行长时间任务。

Service 有两种形式：

* Started: 组件通过 startService() 来启动。一旦启动，会无限期运行在后台，即使启动它的组件已经被销毁。一般他们会运行指定的动作
然后结果，比较下载一个文件。
* Bound: 组件通过 bindSerivce() 来与服务进行绑定，之后可以与 Service 以客户端-服务器模式进行交互。例如发送请求，接收结果。多个
组件可以绑定到同一服务，当所有组件都销毁时，这个服务才销毁。

Service 可以同时以两种方式工作，只要你实现 了 onStartcommand() 和 onBind() 回调函数。

## 基础
要创建一个 Service，需要定义 Service 的子类，并且实现几个关键的回调函数。

onStartCommand()
当另一组件调用  startService() 时，会调用 onStartCommand()，一旦调用完成，服务即启动

onBind()
当另一组件绑定到这个服务时，系统会调用 onBind()，你必须要提供一个接口，返回一个 IBinder，以便客户端可以与这个服务通信。

onCreate()
服务第一次被创建时调用，在 onStartCommand() 之前

onDestroy()
当服务不再被使用时调用。在这里要清理资源，如打开的线程，注册的监听器，receivers 等。

Android 系统可能在内存量太少时，结束 Service。如果这个 Service 和前台获取焦点的 Activity 绑定，那么被杀死的概率下降。如果服务
被声明为运行在前台，那么几乎不可能被杀死。

### 在 manifest 中声明 service
在 manifest 的 <application> 下，声明 <service>

```
<manifest ...>
...
  <application ...>
    <service android:name=".ExampleService"/>
  </application>
    
</manifest>
```

为了保持应用安全性，应该总是显式地启动 Service，而不要在 <service> 下加 filter。

### 创建 Service
组件在启动 Service时，使用startService()，并且给它传递一个 Intent，表明要启动的是哪个服务，给服务传递什么数据。Service 在
onStartCommand() 方法中接收到这个 Intent。

注意，Service 启动时，会在应用的主线程中，如果你有长时间运行的任务，会影响到用户在前台的交互，需要新建立一个线程。

一般情况下，你可以继承下面这两个类来实现服务：

* Service: 所有服务的基类。如果你继承了它，注意把任务放在单独的线程中。
* IntentService：Service 类的子类，如果你不需要同时处理多个请求，可以使用这个类，它已经使用了一个工作线程来处理任务，你只要实现 onHandleIntent() 方法，处理请求就行了。


### 继承 IntentService 类
IntentService 类主要完全下面的工作：
* 创建默认工作线程，执行所有传递到 onSTartCommand() 中的Intent
* 创建工作队列，一次发送一个 Intent 到 onHandleIntent()
* 所有请求处理守全，关闭服务
* 提供 onBind() 的默认实现（返回null)
* 提供 onStartCommand() 的默认实现，把 intnet 改送到工作队列，然后到 onHandleIntent()

### 继承 Service 类
如果想同时处理多个请求，可以自己继承 Service 类，实现各个回调函数，同时在多个线程中处理各个请求。

注意 onStartCommand() 返回的整数，它决定了系统杀死 Service 后如何重启。

* START_NOT_STICKY: 如果系统杀死了 Service，不重启它，除非有没处理的 intents 传递过来。
* START_STICKY：如果系统杀死了 Service，重启它，但是不传递最后一个 Intent，如果有没有处理的 intents，就传递过来处理。
* START_REDELIVER_INTENT: 如果系统杀死了 Service，重启它，并且传递最后一个 Intent，如果有没有处理的 intents，传递过来处理。

### 启动 Service
调用 startService，传递 Intent，例如

```
Intent intent = new Intent(this, HelloService.class);
startService(intent);
```

调用 startService() 后，调用  onStartCommands() 。如果这个Service没有在运行，会先调用 onCreate()，再调用 onStartCommands()

### 停止 Service
Service 要自己管理生命周期，除非内存实在不够用了，否则系统不会销毁 Service。所以 Service 要自己调用 stopSelf() 或者由其它组件
调用 stopService()。

注意为了避免浪费系统资源，当 Service 完全工作时，销毁它是非常重要的。

## 创建一个 Bound Service
如果你的应用内组件需要与 Service 交互，或者你的应用要导出一些功能，让其它应用可以通过 IPC 使用，那么可以通过 bindService() 
绑定到一个服务。这类服务，你需要实现 onBind() 回调函数，这个回调函数要返回一个 IBinder，这个 IBinder 里要实现回调函数，
客户端通过这个 IBinder 与服务交互。可以有多个客户端绑定到同一服务，不想绑定时调用 unbindService()，当所有绑定到服务的客户端
都解除绑定时，这个服务会被销毁。

## 向用户发送 Notifications
服务可以显示一个 Toast，发送 Notification。

Toast 向用户显示一个消息，过一会会自己消失。Notification 在 Status Bar 显示一个小图标，和一个消息，通常表示任务完成，你可以通过点击展开这个通知，启动一个 Activity。

## 在前台运行服务
前台服务是用户在乎的服务，当内存量低时，系统不会轻易杀死它。前台服务必须为 status bar 提供一个 notification。这个 notification 在服务没停止或者没被从前台移除时，不会消失。

例如，音乐播放器就会运行在前台，status bar 中的 notification 会显示播放的是哪首歌，你还可以与它交互。

要启动前台服务，可以使用 startForeground()，要停止前台服务，可以调用 stopForegound()，不过这个函数只是把服务移出前台，不会停止它。

## 管理 Service 的生命周期
有两种方式启动 Service

* 一个 started service: 通过 startService() 启动
* 一个 bound service: 通过 bindService() 启动

两种服务都是从 onCreate() 开始，onDestroy() 结束，只不过 started service 会调用 onStartCommand() 启动，bound service 会调用 
onBind()，返回客户端一个 IBinder，客户端解除绑定时调用  onUnbind() 

两种服务不冲突，一个 started service 也可以是一个 bound service
