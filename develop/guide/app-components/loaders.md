# Loaders
Loaders 在 Android 3.0 中引入，使得在 Activity 和 Fragment 中，异步载入数据更加方便。 Loaders 有以下特性：
* 在每个 Activity 和 Fragment 中都是可用的
* 提供了异步载入数据的方式
* 监视数据来源，当内容改变时，传递新的结果
* 当配置改变后，重建时，自动重新连接最后一次 loader 的 cursor

## Loaders API 概览
在应用中使用 Loaders 涉及很多类和接口，主要有：

* LoaderManager: 管理所有 loaders
* LoaderManager.LoaderCallbacks: 回调函数接口，让客户端与 LoaderManager 交互
* Loader: 抽象类，执行异步载入数据
* AsyncTaskLoader: 抽象的 loader，提供 AsyncTask 执行任务
* CursorLoader: AsyncTaskLoader 的子类，查询 ContentResolver，返回 Cursor。实现了 Loader 协议，基于 AsyncTaskLoader 在后台线程中
执行 cursor 查询。这是从 ContentProvider 异步载入数据的最佳方式。

## 在应用中使用 Loaders

使用 Loaders 的应用通常要包含：

* 一个 Activity 或者 Fragment
* 一个 LoaderManager 实例
* 一个CursorLoader，用于从 ContentProvider 载入数据
* 一个 LoaderManager.LoaderCallbacks 实现，创建，管理 loaders
* 显示载入数据的方式，例如 SimpleCursorAdapter
* 一个数据源，例如 ContentProvider

### 启动一个 Loader

在 Activity 的 onCreate() 或者 Fragment 的 onActivityCreated() 中：

```
getLoaderManager().initLoader(0, null, this);
```

第一个参数 0 代表 Loader 的唯一 ID。
第二个可选参数，用于构造 loader 时提供支持。
第三个参数是 LoaderManager.LoaderCallbacks 的实现

initLoader() 保证初始化并激活一个 loader，它可能有两种结果：

* loader ID 已经存在，那么最后一次创建的 loader 会被复用
* loader ID 不存在，调用 LoaderManager.LoaderCallbacks 的实现中的 onCreateLoader()

### 重启 Loader
如果想要抛弃 loader 中的旧数据时。

```
getLoaderManager().restartLoader(0, null, this);
```

### 使用 LoaderManager Callbacks

LoaderManager.LoaderCallbacks 是客户端与 LoaderManager 交互的回调接口。

#### onCreateLoader
初始化，并返回一个新的 Loader，常见的方式是创建 CursorLoader 并返回，它的构造函数需要执行 ContentProvider 查询时所需要的那些参数：

* uri: 需要获取内容的 URI
* projection: 返回的列
* selection: 过滤器，声明了返回哪些行
* selectionArgs: 你可以在 selection 中包含 ?s，用 selectionArgs 中的值替换它
* sortOrder: 如何对行进行排序

#### onLoadeFinised
当之前创建的 loader 完成数据载入时会被调用。当系统不需要 loader 中的数据时，它会去释放他们，不用你手动释放，所以你用 CursorAdapter 时，用新数据替换旧数据的方式是使用 swapCursor()

```
public void onLoadFinished(Loader<Cursor> loader, Cursor data) {
  mAdapter.swapCursor(data);
}
```

#### onLoaderReset
当之前创建的 loader 需要重置时，这样里面的数据就无效了:
```
public void onLoadFinished(Loader<Cursor> loader, Cursor data) {
  mAdapter.swapCursor(null);
}
```

## 示例
之前代码的完整示例，还有两个其它示例：

* LoaderCursor
* LoaderThrottle
