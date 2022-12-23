# 在 macOS 上创建打开 iOS 模拟器进行调试

首先确保已安装 `Xcode`，且打开过一次。

## 打开 Simulator

在命令行使用下面的命令打开 `Simulator.app`:

```sh
$ open -a simulator
```

或者打开 `Xcode`，在菜单栏 `Xcode > Open Developer Tool > Simulator` 即可打开。

## 创建模拟器

如果之前已经创建过模拟器，那么打开 `Simulator.app` 之后会默认打开。

之前未创建过模拟器，在菜单栏 `File > New Simulator...` 打开创建页面，输入模拟器的名字，选择任意一款 iPhone 或者 iPad（最好是近年发布的机型），选择 iOS / iPadOS 系统（最好是最新的），点击 `Create` 即可。

创建好之后不会直接打开，在菜单栏 `File > Open Simulator > ` 找到刚刚创建的模拟器点击打开即可（以名字显示，可以按住 ⌥ 查看机型和系统）。

```sh
$ flutter devices
flutter devices
3 connected devices:

iPhone 13 221223 (mobile)
macOS (desktop)
Chrome (web)
```

可以看到打开之后 Flutter 已经识别到了新创建打开的模拟器，在项目目录使用下面的命令即可将应用在该设备上运行：

```sh
$ flutter run -d iphone # 输入 flutter devices 命令显示的设备名称前缀即可
```

## References

- https://docs.flutter.dev/get-started/install/macos#android-setup
