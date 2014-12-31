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
为了让你可以基于设备特性来管理应用的可用性，Android 为一些不是所有设备都支持的软硬性特性定义了一些特性ID。例如，软盘传感器的是
`FEATURE_SENSOR_COMPASS`，应用挂件的是 `FEATURE_APP_WIDGETS`。

如果必要的话，你可以通过应用 Manifest 文件中的 <uses-feature> 元素来避免没有这些特性的设备安装你的应用，例如：
```
<manifest ...>
  <uses-feature android:name="android.hardware.sensor.compass"
                android:required="true" />
  ...
</manifest>
```

Google Play 会让在 Manifest 文件中声明的特性与设备特性比较，如果设备不支持的话，用户就不能安装你的应用。

如果你设备的主要功能不是这些特性，你可以把属性中的 `required` 设置为 `false`，在运行的时候通过代码来检测设备是否有这个特性，如果没有的话，禁用一些功能，例如：

```
PackageManager pm = getPackageManager();
if (!pm.hasSystemFeature(PackageManager.FEATURE_SENSOR_COMPASS)) {
  disableCompassFeature();
}
```

更多你可以通过 Google Play 进行过滤的特性，可以参考 [Filters on Google Play]() 文档。

注意：有些系统权限隐含有需要某个设备特性的意思。例如，如果你的应用请求访问蓝牙的权限，这隐含着需要 `FEATURE_BLUETOOTH` 设备特性。你可以通过将 Manifest 文件中的 <uses-feature> 标签中的 `reuqried` 设置为 `false`，让没有这个设备特性的设备也能使用你的应用。更多关于隐含需要的设备特性，可以阅读 [Permissions that Imply Feature Requirements]()

### Platform version
不同的设备可能运行在不同的 Android 平台上，例如 Android 4.0 或者 Android 4.4。每一个后继版本都提供了一些新的 API，这些新 API 在之前的版本中是不能用的。为了表明平台支持哪个的 API 集合，平台都会指定一个 API Level. 例如，Android 1.0 是 API Level 1，Android 4.4 是 API Level 19。

API Level 可以让你声明应用兼容的最小版本，通过 Manifest 文件中 <uses-sdk> 标签的 minSdkVersion 属性来指定。

例如，[calendar Provider APIs]() 是在 Android 4.0(API level 14) 中被添加进去的。如果你的应用没有它们就不能用，那么你需要这样声明：

```
<manifest ...>
  <uses-sdk android:minSdkVersion="14" android:targetSdkVersion="19"/>
  
  ...
</manifest>
```

minSdkVersion 属性指定你的应用支持的最小 API 版本， targetSdkVersion 属性指定你的应用优化过的最高版本。

每个后继版本的 API 都对之前的版本兼容，所以要想让你的应用在后面的版本中还能用，就要使用那些文档中规定的 API。

注意： targetSdkVersion 并不意味着你的应用不能在更高的版本上运行，但是指定它仍然是非常重要的，因为它可以告诉系统你的应用是否应该继承对新版本中行为的改变。如果你不把 targetSdkVersion 设定为最新版本，应用在最新版本上运行时，就会假设你的应用需要一些向后兼容的行为。例如，在 Android 4.4 中，使用 AlarmManger API 创建的警告，默认会不精确，这样系统可以把应用的警告集中起来，这样可以省电。但是如果你把应用的 targetSdkVersion 设置成小于 19，那么系统会保留之前的行为。

如果你的应用使用最新的 API，但是并不是应用最主要的功能，你可以在运行时检查 API Level，如果等级太低，可以禁用应用的一些特性。这就是说，你要把 minSdkVersion 设置成应用主要功能需要的最小值，然后与当前系统的 API Level 进行比较（SDK_INIT):

```
if (Build.VERSION.SDK_INT < Build.VERSION_CODES.HONEYCOMB) {
disableDragAndDrop();
}
```

### Screen configuration
Android 运行在手机，平板，电视等各种设备上。为了给设备屏幕分类，Android 在两个方面给出分类依据：屏幕大小，屏幕密度：

* 四种大小：small, normal, large 以及 xlarge
* 四种密度：mdpi(medium), hdpi(high), xhdpi(extra-high), xxhdpi(extra-extra-high) 以及其它

默认情况下，你的应用是和所有屏幕大小和密度都兼容的，因为系统会根据你的 UI 以及图片资源进行调整。但是，为了给用户更好的体验，你还是要给每种屏幕配置都提供不同的布局和图片资源。

更多关于如何为不同屏幕配置创建不同资源以及如何在必要时限制你的应用适用的屏幕大小的信息，可以阅读 [Supporting Different Screens].

## Controlling Your App's Availabilit for Business Reasons
除了基于设备限制应用的可用性，你还可能需要根据商业上或者法律原因限制应用的可用性。
