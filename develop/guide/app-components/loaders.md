# Loaders
Loaders 在 Android 3.0 中引入，使得在 Activity 和 Fragment 中，异步载入数据更加方便。 Loaders 有以下特性：
* 在每个 Activity 和 Fragment 中都是可用的
* 提供了异步载入数据的方式
* 监视数据来源，当内容改变时，传递新的结果
* 当配置改变后，重建时，自动重新连接最后一次 loader 的 cursor

## Loaders 总结
在应用中使用 Loaders 涉及很多类和接口，主要有：

* LoaderManager: 管理所有 loaders
* LoaderManager.LoaderCallbacks: 回调函数接口，让客户端与 LoaderManager 交互
* Loader: 抽象类，执行异步载入数据
* AsyncTaskLoader: 抽象的 loader，提供 AsyncTask 执行任务
* CursorLoader: AsyncTaskLoader 的子类，查询 ContentResolver，返回 Cursor。实现了 Loader 协议，基于 AsyncTaskLoader 在后台线程中
执行 cursor 查询。这是从 ContentProvider 异步载入数据的最佳方式。
