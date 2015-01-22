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

