# Content Providers
Content providers 管理结构化的数据。它们包装数据，并提供一些机制来定义数据安全。Content providers 是将一个进程中的数据与另
一进程中的代码连接起来的标准接口。

当你想访问 content provider 中的数据时，你需要使用 ContentResolver 对象。它与 ContentProvider 对象通信，provider 对象接收请求，
执行请求的动作，返回结果。

如果你不想分享自己应用内的数据，就不需要开发自己的 content provider。但是，如果你想要提供搜索提示或者想要让你应用内的数据可以
复制出去，你就要开发 content provider。

Android 已经提供了一些 content provider，来管理音频，视频，图像，以及联系人信息。
