# Android Wear

使用 Android Wear 为可穿戴设备设计应用与手机和平板截然不同，不同的优势和缺陷，不同的用户场景，不同的人体工程学。你需要明白
Android Wear 在全局上的体验，以及如何加强这种体验。新形式的设备需要有新的 UI 模型，Android Wear 的 UI 包含了两个重要部分，分别
是 Suggest 和 Demand。

Suggest 是Android Wear推给用户的信息，可以竖着滑动，查看不同卡片上的信息，也可以横着滑动，查看当前卡片上进一步的信息。Demand 是用户的需求，可以告诉 Google 。不同的声音指令，会启动不同的 intent，应用开发者可以让自己的应用匹配相应的 intent，这样当用户
发出相应指令时，就会启动你的应用。如果有多个应用对应同一个 intent，系统会提示用户选择。
