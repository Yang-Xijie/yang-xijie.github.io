---
title: Flutter Notes
---

# Flutter Notes

## Commands

```sh
flutter --version
flutter upgrade

# 查看安装情况
flutter doctor
```

```sh
# 新建项目
flutter create <project_name>

# 查看当前连接的设备
flutter devices

# 在 Chrome 中运行应用
flutter run -d chrome
# 在 Mac 上运行应用
flutter run -d mac
# 在 iPad Simulator 上运行应用
open -a simulator
flutter run -d ipad
# 在自己的 iPad 上运行应用
flutter run -d 杨希杰

# 用 release 模式运行
flutter run --release

# subcommands: apk macos web
flutter build <subcommand>
flutter build <subcommand> --release
```

## Learning materials

### Get started

- [Write Your First Flutter App, part 1](https://codelabs.developers.google.com/codelabs/first-flutter-app-pt1/#0)
- [Dart overview](https://dart.dev/overview)
- [Introduction to widgets](https://docs.flutter.dev/development/ui/widgets-intro)
- [Building a web application with Flutter](https://docs.flutter.dev/get-started/web)

### Advanced

- [Flutter for iOS developers](https://docs.flutter.dev/get-started/flutter-for/ios-devs)
- [Write Your First Flutter App, part 2](https://codelabs.developers.google.com/codelabs/first-flutter-app-pt2#0)
- `Development` part under [docs.flutter.dev](https://docs.flutter.dev)

### Deployment

- [Build and release an Android app](https://docs.flutter.dev/deployment/android)
- [Build and release an iOS app](https://docs.flutter.dev/deployment/ios)
- [Build and release a macOS app](https://docs.flutter.dev/deployment/macos)
- [Build and release a web app](https://docs.flutter.dev/deployment/web)

## Principles

- Chrome(web) to debug
- Mac(desktop) to test desktop
- iPad(mobile) to test gestures
- If flutter cannot do want you want, then go with the native development. Or just accept the fact and drop that feature.
