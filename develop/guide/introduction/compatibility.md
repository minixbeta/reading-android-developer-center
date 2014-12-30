# Device Compatibility
Android 被设计为可以在多种设备上运行，例如手机，平板，电视。作为开发者，你开发的应用也应该灵活地适配各种设备。你可以为不同配置的设备设计不同的布局，资源文件。Android 系统会根据设备不同，加载不同资源。这样你只用一个 APK 就能适配各种设备。必要的话，你还可以指定自己的应用都需要哪些特性支持，这样用户使用 Google Play 时，就可以避免让没有特定特性支持的设备安装你的应用。

## What Does "Compatibility" Mean
兼容性有两个方面的含义，一是“设备兼容性”，二是“应用兼容性”。由于 Android 是个开源项目，任何硬件厂商都可以制造支持 Android 的设备。一个设备是 “Android 兼容”的意思是它可以正确地运行为 Android 运行时环境编写的应用。Android 运行时的细节可以在 [Android compatibility program]() 中找到，每个Android兼容设备都必需通过兼容性测试集才行。

作为开发者，你没必要担心这些，因为能安装 Android 应用的设备，肯定已经是 “Android兼容”了。你需要关心的是“应用兼容性”。由于 Android 运行在大量设备上，有些特性不是所有设备都支持的。例如，有些设备是没有罗盘传感器的，如果你的应用核心功能需要罗盘传感器，那么你的应用只有在包含罗盘传感器的设备上才是兼容的。

## Controlling Your App's Availability to Devices
Android 支持许多特性，你可以通过使用平台 API 利用它们。有些特性是硬件相关的，有些是软件相关的，有些依赖于平台版本。并不是所有设备都支持所有特性，所以你需要基于应用所需的特性并控制应用的可用性。

为了让更多用户使用你的应用，你应该在同一 APK 内，尽力支持更多的设备配置。多数情况下，你可以在应用运行的时候选择禁用某些特性，或者是为不同的配置提供不同的资源。必要的话，你可以根据下面的设备特征，通过 Google Play 限制应用的可用性：
* 设备特性
* 平台版本
* 屏幕配置

### Device features

### Platform version

### Screen configuration

## Controlling Your App's Availabilit for Business Reasons
