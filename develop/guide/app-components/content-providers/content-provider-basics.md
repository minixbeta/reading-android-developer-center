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

query 的参数中，uri 表示哪个表格，projection 表示哪个列，selection 表示与列相关的查询条件，selectionArgs(?) ,sortOrder 表示
对返回的数据进行排序的方式。

### Content URIs
content URI 是标识 provider 中数据的 URI，它由 authority 和 path 两部分组成，authority 表示哪个 provider，path 表示哪个表格。

例如，用户字典中的单词：

```
content://user_dictionary/words
```
