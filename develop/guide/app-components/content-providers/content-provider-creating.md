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
