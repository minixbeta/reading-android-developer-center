# 创建 Content Provider
Content Provider 管理对数据的访问。你可以把 provider 实现为一个或多个类，再加上 manifest 文件中的元素。其中一个类是 
Content Provider 的子类，这是你的 provider 和其它应用的接口。

下面的内容讲的是创建 content provider 及一系列 API 所需的基本步骤。

## 开始构建之前

在开始构建 Provider 前，你需要做的是：
