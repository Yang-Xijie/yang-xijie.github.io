# Flutter Notes

## Commands

```sh
flutter --version
flutter upgrade

# check the installation and environment
flutter doctor
```

```sh
# create a new project
flutter create <project_name>

# list connected devices
flutter devices

# run for Chrome
flutter run -d chrome
# run for Mac
flutter run -d mac
# run for iPad Simulator
open -a simulator
flutter run -d ipad
# run for iPad
flutter run -d 杨希杰

# run using release mode
flutter run --release

# build an app (subcommands: apk macos web)
flutter build <subcommand>
flutter build <subcommand> --release

# clean current project
flutter clean
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

## My principles

If flutter cannot do want you want, then go with the native development. Or just accept the fact and drop that feature.

## Targets

One app should deliver two targets with different designs:

- Desktop (with mouse and keyboard)
    - Native macOS / Windows / Linux
    - Chrome on macOS / Windows / Linux
- Mobile (with gestures)
    - Native Android / iOS / iPadOS (portrait and landscape)
    - Chrome on Android / iOS / iPadOS

For web, there should be an introduction page to lead users to desktop or mobile.

For debug usage:

- Desktop native: macOS
- Desktop web: Chrome on macOS
- Mobile native: iPadOS
- Mobile web: Safari on iPadOS
