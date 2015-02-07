# Content Provider

这篇文章描述了下面的内容：

* content provider 如何工作
* 向 content provider 请求数据的 API
* 在 content provider 中插入，更新，删除数据的 API
* 其它可以更灵活使用 content provider 的 API

## 概览
Content Provider 以一个或多个表格的方式向外部提供数据。表格的行代表数据实例，列代表数据的属性，和关系型数据库差不多。

### 访问 provider
访问 provider 时，使用 ContentResolver，它提供了基本的 CRUD 函数。ContentResolver 在客户端使用，与保存有数据的 ContentProvider
进行进程间通信。

例如，你想查询数据时，可以使用 ContentResolver.query()。

```java
mCursor = getcontentResolver().query(
  userDictionary.Words.CONTENT_URI,
  mProjection,
  mSelectionClause,
  mSelectionArgs,
  mSortOrder)
```

query 的参数中，uri 表示哪个表格，projection 表示哪个列，selection 表示与列相关的查询条件，selectionArgs(查询条件中的参数值) ,sortOrder 表示对返回的数据进行排序的方式。

### Content URIs
content URI 是标识 provider 中数据的 URI，它由 authority 和 path 两部分组成，authority 表示哪个 provider，path 表示哪个表格。

例如，用户字典中的单词：

```
content://user_dictionary/words
```

## 向 Provider 请求数据
向 Provider 请求数据要做两件事：

1. 请求对 Provider 的读取权限
2. 定义向 provider 发送数据请求的代码

### 请求读取权限
对读取权限的请求不能在运行时完成，而要在 manifest 中使用 <uses-permission> 元素来请求，在安装你的应用时，会提示用户授权。

例如，用户字典 Provider 定义的权限是 `anddroid.permission.READ_USER_DICTIONARY`。

### 构造请求
请求是通过函数 query(Uri, projection, selection, selectionArgs, sortOrder) 完成的，之前已经说明过参数的意义。

### 避免恶意输入带来的危害
如果直接通过用户输入构造请求，可能造成 SQL 注入。所以，需要使用 selection, selectionArgs 共同完成请求条件。在 selection 中把
请求条件表示出来，但是参数值不是通过用户输入拼接到 selection 中，而是放入 selectionArgs 中。

### 显示请求结果
请求结果会放在 Cursor 中，Cursor 其实是多个行组成的列表，所以可以通过  SimpleCursorAdapter 与 ListView 联合使用。

当然，如果你不想用于 ListView，可以通过 cursor.moveToNext() 遍历，通过 cursor.getString(index) 获取数据。

## Content Provider 权限
provider 应用可以指定其它应用访问它时需要的权限。其它应用需要声明这个权限，在安装时，用户就知道这些程序需要这些权限。

如果 provider 应用没有指定权限，他们其它应用不能访问它，但是 provider 应用内部无须权限即可读写。

用户字典 Provider 需要 `android.permission.READ_USER_DICTIONARY` 权限进行读取操作，需要 `android.permission.WRITE_USER_DICTIONARY` 权限进行插入，更新，或者删除数据。

为了获取访问 provider 的权限，要在 manifest 文件里声明，在安装应用时，会提示用户，如果用户授权了，就安装，不授权，就取消安装。

例如：

```
<uses-permission android:name="android.permission.READ_USER_DICTIONARY">
```

## 插入，更新，删除数据
你可以使用与查询数据相同的方式，来调整数据。调用 ContentResolver 的方法，传入参数，之后这些参数会被传入 ContentProvider 的对应
方法中。provider 和 provider 客户端会自动处理安全问题。

### 插入数据
调用 ContentResolver.insert() 插入一行，返回这行的 URI。

```
ContentValues mNewValues = new ContentValues();

mNewValues.put(UserDictionary.wrods.APP_ID, "example.user");
mNewValues.put(UserDictionary.words.LOCALE, "en_US");

mNewUri = getContentResolver().insert(
  UserDictioinary.Word.CONTENT_URI,
  mnewVaues
);
```

返回的 URI 格式为：

```
content://user_dictionary/words/<id_value>
```

`<id_value>` 是插入行的 _ID ，它由系统自动维护，作为表和主键。

### 更新数据
更新数据时，使用 ContentResolver.update()，更新的值放在 ContentValues 对象里，更新的行像查询值那样，使用 selection, selectionArgs 指定。

### 删除数据
删除数据与查询数据类似，使用 ContentResolver().delete(uri, selection, selectionArgs)。需要注意防止恶意数据。

## Provider 数据类型
Content Provider 可以提供许多数据类型，除了 用户字典 Provider 中使用的文本外，还有:

* 整数(integer)
* 长整数(long integer)
* 浮点数(floating point)
* 长浮点数(double)

Provider 中每一列的数据类型一般在文档中可以查到。

Provider 还为它定义 的每个 content URI 维护了 MIME 数据类型信息。

## 访问 Provider 的其它方式
另外有三种访问 Provider 的方式非常重要：

* Batch access：使用 ContentProviderOperation 类提供的方法，创建一批访问调用，再使用 ContentResolver.applyBatch() 使用这些调用
* 异步查询：在独立的线程中进行查询，一种方式是使用 CursorLoader 对象
* Data access via intents: 虽然不能直接向 provider 发送 intent，但是可以向 provider 所在应用发送 intent

### Batch access
适用于插入大量数据，或者在同一线程调用中，在多个表格中插入行，或者将一系列跨进程动作作为一个事务。

使用方法是，创建 ContentProviderOperation 数组，用于 ContentResolver.applyBatch()，并传入 content provider 的 authority。

### 通过意图进行数据访问
意图可以对 content provider 进行间接访问。即使你的应用没有权限访问 provider 中的数据，你也通过向有权限访问
的应用发送意图，得到有 URI 权限的 result intent。有权限的应用可以在 result intent 中设置临时权限：

* 读取权限：FLAG_GRANT_READ_URI_PERMISSION
* 写权限：FLAG_GRANT_WRITE_URI_PERMISSION

provider 在 manifest 文件中为 content URI 定义 URI 权限，使用 <provider> 元素的 android:grantUriPermission 属性，或者 
<grant-uri-permission> 子元素。

例如，你想从联系人中获取数据，但是你又没有 READ_CONTACTS 权限，你可以：

1. 你的应用发送 intent，使用 ACTION_PICK 动作，CONTENT_ITEM_TYPE 作为  MIME 类型，使用 startActivityForResult()
2. 这个 intent 会与选择联系人信息的 activity 的 intent filter 匹配，这个 activity 进入前台
3. 在选择联系人信息 activity 里，用户选择一个联系人。此时，选择 activity 会调用 setResult(resultcode, intent) 设置 intent 并返回给你的应用
4. 你的应用中的 activity 回到前台，通过  onActivityResult() 得到返回的结果
5. 得到 result intent 中的 content URI，你就可以读取其中的联系人信息了。

### 使用其它应用
如果你的应用没有权限去修改数据，你可以激活一个有权限的，让用户在那里操作
