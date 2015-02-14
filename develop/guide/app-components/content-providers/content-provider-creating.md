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
Content URI 标识 provider 中的数据。它包含两部分，authority 标识整个 provider，path 指向表或者文件。

### 设计 autority
一般使用包名作为前缀，例如：`com.example.<appname>.provider`

### 设计 path 结构
path 以 autority 为前缀，加上表名，例如 `com.example.<appname>.provider/table1`

### 处理 content URI IDs
按照惯例，provider 访问表中一行时，都使用 content URI 再加上 ID 值。这个 ID 匹配表中的 _ID 列。

### Content URI 模式
使用 UriMatcher，再加上 `*` 和 `#` 两个通配符，可以将 Content URI 对应一个数字，这样就可以使用 switch 对不同的 Content URI 
进行处理，例如：

```
private static final UriMatcher sUriMatcher;

sUriMatcher.addURI("com.example.app.provider", "table3", 1);

sUriMatcher.addURI("com.example.app.provider", "table3/#", 2);

...

switch(sUriMatcher.match(uri)) {
  case 1:
    // 处理对应 table3 的 URI
  case 2:
    // 处理对应 table3 下某一行
}
```

## 实现 ContentProvider 类
ContentProvider 实例通过处理来自其它应用的请求，来管理对结构化数据的访问。所有形式的请求最终都会调用 ContentResolver，进而调用 ContentProvider 对应的方法。

### 需要实现的方法

query()：从 provider 中获取数据。
insert(): 向 provider 中插入数据。
update(): 更新 provider 中的数据。
delete(): 删除 provider 中的数据。
getType(): 返回 content URI 对应的 MIME 类型。
onCreate(): 初始化 provider。

这些方法与 ContentResolver 中的方法名字是一样的。

需要注意的是：
* 除了 onCreate() 其它方法都要保证线程安全。
* 避免在 onCreate() 中做过多的工作，把初始化工作推迟到真正需要的时候。
* 虽然你必须实现这些方法，但是你什么都不做也可以，但是要返回要求的类型的数据。

### 实现 query() 方法
ContentProvider.query() 方法要返回 Cursor 对象，如果失败了，抛出 Exception。如果你使用 SQLite 数据库，可以返回 SQLiteDatabase 类 query() 方法的返回值。

如果不用 SQLite 数据库，要使用 Cursor 的子类，例如 MatrixCursor 类。

注意 Android 要跨进程传递Exception，在处理请求错误时，下面两个类可能会有用：

* IllegalArgumentException
* NullPointerException

### 实现 insert() 方法
insert() 方法使用 ContentValues 参数，向表中添加一行。返回对应新添加行的 content URI

### 实现 delete() 方法
delete() 方法没必要真的在物理上把一行从数据存储中删除。如果你对 provider 使用了 sync adapter，你应该考虑使用 `delete` 标志
标记被删除的行。

### 实现 update() 方法
update() 方法使用 ContentValues 作为参数。

### 实现 onCreate() 方法
Android 系统会在启动 provider 的时候调用 onCreate()，这个方法里应该只做一些快速初始化的任务，把数据库创建，数据载入推迟到真正
接收到数据请求时。

例如，如果你使用 SQLite 数据库，你可以在 ContentProvider.onCreate() 中创建 SQLiteOpenHelper 对象，第一次打开数据库时，创建 SQL 表，你第一次调用 getWritableDatabase() 时，自动调用 SQLiteOpenHelper.onCreate() 方法。

## 实现 ContentProvider MIME 类型
ContentProvider 类有两个方法，返回 MIME 类型。

getType(): 对任何 provider 来说，都必须要实现
getStreamTypes(): 如果 provider 提供文件，要实现这个方法

tables 的 MIME 类型
getType() 返回的是 MIME 类型的字符串，描述 content URI 参数返回的数据类型。

对通用的数据类型，例如 文本，HTML, JPEG, getType() 返回标准 MIME 类型，可以在 IANA MIME Media Types 网站上看到。

对指向表格中数据 的一行，或者多行，getType() 返回 Android vendor-specific MIME 格式：

* 类型部分：vnd
* 字类型部分：
  - 如果是单行：android.cursor.item/
  - 如果是多行：android.cursor.dir
* Provider 相关的部分：vnd.<name>.<type>

如果 provider 的 authority 是 com.example.app.provider，它导出的表名为 table1, 那么 table1 中多行的 MIME 类型为：

```
vnd.android.cursor.dir/vnd.com.example.provider.table1
```

如果是单行：

```
vnd.android.cursor.item/vnd.com.example.provider.table1
```

### 文件的 MIME 类型
getStreamTypes() 返回字符串数组，表示 provider 可以返回的文件类型。

如果 provider 提供了照片类型的文件，格式为 .jpg, .png, .gif，那么如果 向 ContentResolver.getStreamTypes() 传入 "image/*" 作为 过滤，返回的 MIME 类型为：

```
{ "image/jpeg", "image/png", "image/gif" }
```

如果过滤字符串为 `*\/jpeg`，返回类型为：

```
{ "image/jpeg" }
```

## 实现 Contract 类
contract 类是一个 public final 类，包含 URIs, 列名，MIME 类型，其它与 provider 相关的元数据的常量定义。这个类其实是 provider 类和其它使用 provider 的应用之间的协议，有了这个类，即使 URIs，列名等等的真实值改变了，也不影响对 provider 的使用。

## 实现 Content Provider 权限
[Data Storage]() 主题描述 了不同类型的存储的安全性和权限，简而言之，最重要的几个点是：
* 默认情况下，数据文件存储在设备内部存储中，对你的应用和provider来说，是私有的
* SQLiteDatabase 数据库对你的应用和provider来说，是私有的
* 默认情况下，存储在外部存储中的数据文件是 public 的，谁都能读
* 用于在设备内部存储中，打开或者创建文件，数据库的方法，可能会给其它应用读和写权限。

## 实现权限
所有应用都可以对你的 provider 进行读写，因为默认情况下，你的 provider 没有权限集。你需要在 manifest 中，设置 <provider> 元素的属性或者子元素。

下面描述了 provider 权限的范围，粒度逐渐变小：

* provider 级别的单一读-写权限
* provider 级别的读权限或者写权限
* 路径权限 ：provider 中的 content URI 的读，写，或者读-写权限
* 临时权限：即使应用没有访问 provider 的权限，也可以临时给它一个权限。它减少了 manifest 中需要定义的权限。

## <provider> 元素
和 Activity 和 Service 一样，Provider 也需要在 manifest 中定义，使用的元素为 <provider>。Android 系统从这个元素中获取下面的
信息：

Authority(android:autorities): 标识整个 provider 的符号 名
Provider 类名(android:name): 实现 ContentProvider 的类
权限：
  * android:grantUriPermissions: 临时权限
  * android:permission: 单一的读-写权限
  * android:readPermission: 读权限 
  * android:writePermission: 写权限
  
启动和控制属性：
  * android:enabled: 允许系统启动 provider
  * android:exported: 允许其它应用使用 provider
  * android:initOrder: provider 启动次序
  * android:multiProcess: 允许系统在与调用的客户端同一进程内启动 provider
  * android:process: provider 所在进程名
  * android:syncable: provider 的数据会和服务端数据同步

信息属性：
  * android:icon: provider 对应图标，在 设置->应用->所有 中
  * android:label: 描述 provider 或者其中数据的信息，在 设置->应用->所有 中

## Intent 与数据访问
应用可以使用 Intent 间接访问 provider。Intent 会启动一个 Activity，这个 Activity 一般与 provider 在同一应用内，这样
可以提供一种对 provider 进行访问，修改的统一方式。
