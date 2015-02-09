# 创建 Content Provider
Content Provider 管理对数据的访问。你可以把 provider 实现为一个或多个类，再加上 manifest 文件中的元素。其中一个类是 
Content Provider 的子类，这是你的 provider 和其它应用的接口。

下面的内容讲的是创建 content provider 及一系列 API 所需的基本步骤。

## 开始构建之前

在开始构建 Provider 前，你需要做的是：

1. 决定是否需要一个 content provider
2. 如果你还没读过 Content Provider Basics，需要读一下

下一步，跟着下面的步骤创建 provider

1. 定义数据存储方式
2. 定义 ContentProvider 子类的实现
3. 定义 provider 的 authority 字符串，content URI，列名。
4. 添加其它信息，例如示例数据或者 AbstractThreadedSyncAdapter 的实现 

## 设计数据存储
Android 中的数据存储技术有：

* SQLite 数据库 API, Android 中自带面向表的的 providers 都使用他们实现。SQLiteOpenHelper 可以创建数据库，SQLiteDatabase 可以访问数据库。记住虽然 provider 外在表现为表，关系型数据库，但是内部实现没必要用 SQLite API 实现
* 存储文本数据，可以使用 Android 提供的面向文件的 API
* 处理基于网络的数据，可以使用 java.net 或者 android.net

### 数据设计要点
* 基于表的数据需要有主键，最好使用 BaseColumns._ID
* 如果你想提供 bitmap 图片或者其它基于文件的非常大的数据，把他们存储在文件中，而不要直接存储在表中
* 使用 Binary Large OBject(BLOB) 数据类型存储大小或者结构可变的数据

## 设计 Content URIs
