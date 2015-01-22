# Services
Service 是运行在后台的组件，没有 UI，适合运行长时间任务。

Service 有两种形式：

* Started: 组件通过 startService() 来启动。一旦启动，会无限期运行在后台，即使启动它的组件已经被销毁。一般他们会运行指定的动作
然后结果，比较下载一个文件。
* Bound: 组件通过 bindSerivce() 来与服务进行绑定，之后可以与 Service 以客户端-服务器模式进行交互。例如发送请求，接收结果。多个
组件可以绑定到同一服务，当所有组件都销毁时，这个服务才销毁。

Service 可以同时以两种方式工作，只要你实现 了 onStartcommand() 和 onBind() 回调函数。

